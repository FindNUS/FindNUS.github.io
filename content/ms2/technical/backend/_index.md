---
title: "Backend Technical Documentation"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
---
In this page, we document:  
1. The **key technologies** used
2. The  **high-level overview** of the Backend
3. The **integration** details

Specifically, this is a deep dive into how the various technologies are interfaced with each other. 
*Why certain technologies?*[^1]

[^1]: In Milestone 1, we documented in-depth why we used certain technologies instead of another.
[Link to the document](https://drive.google.com/file/d/1X4n5IalejDChWyBY_rGtnBOd1qMa3wq_/view?usp=sharing)  

# Key Technologies
This is a list of the technologies that we have used to build the backend.  
- Golang (Language)
- [Gin-gonic](https://github.com/gin-gonic/gin) (HTTP Router)
- Docker (Runtime)
- RabbitMQ (Message Broker)[^2]
- Heroku (PaaS)
- MongoDB (Database)
- Bonsai ElasticSearch (Search Engine)
- Firebase (Authentication)
- Imgur (3rd Party API)

[^2]: A message broker is needed to communicate between docker containers. This is a heroku perculiarity as the docker containers cannot talk to each other via HTTP due to security policy. In industry, message brokers are often used to coordinate work as well.

# High-Level Overview
![Backend Arch](./backend_250622.png)

This figure shows how the backend roughly works as a whole unit to provide the backend API for FindNUS' business logic. 
As of Milestone 2, we deployed **2 microservices**, backend and item. 

Backend is in charge of routing and item is in charge of CRUD.
The next section takes a closer look into **HOW** the technologies are integrated with each other.  

# Integration Details
This section dives deep into how the technology is integrated with one another to produce a cohesive backend.
We will explain the integration through **events**.

## Recieving HTTP requests from frontend
Technologies Integrated (TI): Golang, Docker, Heroku  

The frontend needs things to be done, such as POSTing new items or GETting items from the database. This is done through the backend providing an API using the HTTP.  

These requests enter Heroku's platform and are forwarded to our **Backend** microservice. 
To actually use these requests, integration is needed between our Docker runtime and Heroku's platform.  
Heroku sends HTTP requests through a `PORT` env variable. We just need to get the port details and we can plug it into our logic to process the http requests.  

Snippet:
```go
	port := os.Getenv("PORT")
	if port == "" {
		// App is running locally
		port = "8080"
	}
```

Using Gin-gonic, we can create a HTTP router to listen to the http requests coming in via `PORT`. We can also ignore malicious/invalid requests by configuring the Cross-Origin settings.

Snippet:
```go
router := gin.Default()
	router.Use(
		cors.New(cors.Config{
			AllowAllOrigins:  true,
			AllowHeaders:     []string{"Origin", "Authorization", "Content-Type", "Access-Control-Allow-Headers"},
			AllowMethods:     []string{"GET", "POST", "PATCH", "PUT", "DELETE", "OPTIONS"},
			AllowCredentials: true,
		}),
	)
// ...Additional logic, omitted for brevity

// Listen for HTTP requests
router.Run(":" + port)  
```

## Sending messages between microservices
TI: Golang, RabbitMQ 

In the microservices architecture, business logic is seperated into different runtimes/containers based on function.  
We will need to pass information between these runtimes, for example, the **Backend Microservice** needing to get a item's detail from the **Item Microservice**.  

The microservices are blocked from using HTTP communication between one another due to Heroku policy. So, instead of HTTP, we need to leverage on a message broker with its own communication protocol, **RabbitMQ** to coordinate messages between these microservices. 

In summary, using RabbitMQ, we defined three **queues** to send our own messages.  

**Item Queue `q_item`**  
Handles one-off messages that require no return response, such as POST and DELETE.  

**Remote Proceedure Call (RPC)[^3] Queue `q_get_req, q_get_resp`**   
Handles messages that require a return response, such as GET and search queries.
[^3]: A RPC is something like a synchronous GET request. It enables two computers in seperate locations to send information to each other. [A primer if you are interested](https://www.geeksforgeeks.org/remote-procedure-call-rpc-in-operating-system/)

The below image illustrates the communciation pipelines between the 2 microservices using RabbitMQ.  

![Message Queue Overview](./mq.png)

### Ensuring Thread-safe communication
In particular, when integrating Golang with RabbitMQ to implement the RPC pattern, each RPC job needs to be given a **unique** `correlation_id` to identify which RPC call the request belongs to. This is not implemented by the golang driver provided. So we created our own thread-safe unique correlation_id generator.  

Thread safety is needed via `sync.Mutex` as the HTTP requests are processed **in-parallel**, so there is a risk that multiple RPC subroutines may have the same correlation_id, which will cause bugs.  

Further, we **DO NOT** use randomly generated numbers as there is no guarantee that the randomly generated numbers won't be the same for 2 concurrent RPCs that call the random generator.  

Snippet:
```go
// JobID Unique Job ID. Overflows are OK
type JobId struct {
	mu sync.Mutex
	id uint64
}

var rpcJobId JobId

// Thread-safe jobId implementation
func GetJobId() uint64 {
	// Force one goroutine to access jobId at a time
	// To prevent a race condition
	rpcJobId.mu.Lock()
	defer rpcJobId.mu.Unlock()
	rpcJobId.id += 1
	jobId := rpcJobId.id
	return jobId
}
```

## Creating, removing and updating, deleting Items
TI: MongoDB, Imgur, Elasticsearch

There are many moving parts and integrations in the CRUD logic. So, a diagram explaining one of the processes, POSTing a new item:  
![POST overview](./post.png) 

Updating and deleting items follow a very similar control flow, but is omitted for now due to repetition.  
The important integration details explained below:

### Image storage with Imgur  
When a new item is added with a raw base_64 string representing the user-submitted image, we store it on imgur. Imgur returns a deleteHash key for us to delete the image, as well as a link to the stored image. We store the hash and link on a Imgur reference database collection to manage our Imgur links.  
For delete item operations, the deleteHash is obtained from the Imgur collection to properly dispose of our Imgur image.

### Synchronising the Search Engine
Elasticsearch runs its own database store in order to index it properly to provide powerful searching capabilities. This means that we need to sync information between MongoDB and Elasticsearch.  

We have explored solutions such as industry-tested Logstash and open-source 'River', but they are either paid or are outdated for our version of Elasticsearch. 

**So, we settled on writing the database synchronisation logic ourselves in order to fully interface MongoDB and ElasticSearch**.  

We wrote equivalent CRUD operations on Elasticsearch for their MongoDB counterpart. If an item needs to be Added/Updated/Removed from MongoDB, a parallel and equivalent operation will be done on Elasticsearch.   

Snippet of a ElasticSearch Item Addition:
```go
// Handler for Adding Item
func ElasticAddItem(item ElasticItem) {
	// Check for item existence first as a safety catch to avoid redundant (the bad kind) copies
	if ElasticGetItem(item.Id) != (ElasticItem{}) {
		// Item already exists! This is likely an update. Delete it and re-add in.
		// Deletion rather than patching is done due to paywalled API
		log.Println("Deleting")
		ElasticDeleteItem(item.Id)
	}
	res, err := EsClient.Index().Index(IndexName).BodyJson(item).Do(context.Background())
	if err != nil {
		log.Fatal(err)
	}
	log.Println("Add item response:", res)
}
```
