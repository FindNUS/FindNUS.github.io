---
title: "Code Testing"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
---
# Frontend


## Backend Unit Testing
Unit testing is done extensively on backend functions. For brevity, we will highight notable unit tests that we have implemented in our Backend testing workflow.  
### Example 1: Request Preprocessing
Preprocessing of HTTP requests is done for the POST & PATCH requests. In the unit test, we load mock data that are designed to PASS (data with no issue) or FAIL (handle the problematic data by returning an appropriate response).  

We test for correctness by running each of the valid/invalid mock items in the data preprocessing function. We then check if the expected output matches what we expect.  

In this case, our pre-processing function `ParseFoundItemBody` returns a tuple `(bytes, error)`.
We check if an error was appropriately detected by the function.  
#### Valid Lost Item Testcases (Truncated)
```json
[
    {
        "Name": "Water bottle",
        "Date": "2022-05-26T08:51:48.782Z",
        "Location": "UTown Bus Stop",
        "Category": "Bottles",
        "Item_details": "Blue, Yellow, Red",
        "Contact_details": "@FindNUS",
        "Contact_method": "LiNe"
    },
    {
        "Name": "Laptop",
        "Date": "2022-01-19T01:32:06Z",
        "Location": "Techno Edge",
        "Category": "Electronics",
    },
    {
        "Name": "Mouse",
        "Date": "2022-04-16T20:02:30Z",
        "Location": "Central Library",
        "Category": "Electronics",
    },
    {
        "Name": "Tux",
        "Date": "2022-03-27T10:08:26Z",
        "Location": "COM2 Bus Stop",
        "Category": "Etc",
        "Image_base64": "iVBORw"
    }
]
```
### Invalid Lost Item Testcases
The reason for 'invalidness' of the data is tagged by its name. 
```json
[
    {
        "Name": "No Date",
        "Location": "Kent Ridge MRT",
        "Category": "Electronics",
        "Image_url": "https://imgs.xkcd.com/comics/is_it_worth_the_time_2x.png"
    },
    {
        "Name": "No Location",
        "Date": "2022-01-31T01:42:30Z",
        "Category": "Electronics",
        "Image_url": "https://imgs.xkcd.com/comics/is_it_worth_the_time_2x.png"
    },
    {
        "Name": "No Category",
        "Date": "2022-01-31T01:42:30Z",
        "Location": "Kent Ridge MRT",
        "Image_url": "https://imgs.xkcd.com/comics/is_it_worth_the_time_2x.png"
    },
    {
        "Date": "2022-01-31T01:42:30Z",
        "Location": "No Name",
        "Category": "Electronics",
        "Image_url": "https://imgs.xkcd.com/comics/is_it_worth_the_time_2x.png"
    },
    {
        "Name": "Invalid Date",
        "Date": "201:42:30Z",
        "Location": "Kent Ridge MRT",
        "Category": "Electronics",
        "Image_url": "https://imgs.xkcd.com/comics/is_it_worth_the_time_2x.png"
    },
    {
        "Name": "Invalid Category",
        "Date": "2022-01-31T01:42:30Z",
        "Location": "Kent Ridge MRT",
        "Category": "Foobar",
        "Image_url": "https://imgs.xkcd.com/comics/is_it_worth_the_time_2x.png"
    }
]
```
This is the testing code used to test for correctness. We can run this locally using golang's built-in testing function: `go test .`.
```go
func TestParseFoundItemBody(t *testing.T) {
	testdata := loadTestItems("valid_found_items.json")
	for _, item := range testdata {
		bytes, _ := json.Marshal(item)
		if _, err := ParseFoundItemBody(bytes); err != nil {
			t.Log("Found item wrongly flagged as invalid: ", item)
			t.Log("Error: ", err.Error())
			t.Fail()
		}
	}
	testdata = loadTestItems("invalid_found_items.json")
	for _, item := range testdata {
		bytes, _ := json.Marshal(item)
		if _, err := ParseFoundItemBody(bytes); err == nil {
			t.Log("Found item wrongly flagged as valid: ", item)
			t.Log(err.Error())
			t.Fail()
		}
	}
}

func TestParseLostItemBody(t *testing.T) {
	testdata := loadTestItems("valid_lost_items.json")
	for _, item := range testdata {
		bytes, _ := json.Marshal(item)
		if _, err := ParseLostItemBody(bytes); err != nil {
			t.Log("Lost item wrongly flagged as invalid: ", item)
			t.Log(err.Error())
			t.Fail()
		}
	}
	testdata = loadTestItems("invalid_lost_items.json")
	for _, item := range testdata {
		bytes, _ := json.Marshal(item)
		if _, err := ParseLostItemBody(bytes); err == nil {
			t.Log("Lost item wrongly flagged as valid: ", item)
			t.Log(err.Error())
			t.Fail()
		}
	}
}
```
### Example 2: HTTP Routing test
Certain HTTP requests. In this snippet, we mock HTTP data to test our HTTP callback handler.
In this snippet, 
```go
func TestHandleNewLostItem(t *testing.T) {
	// Test that user_id guard works
	httpwriter := httptest.NewRecorder()
	ginContext, _ := gin.CreateTestContext(httpwriter)
	body := map[string]interface{}{
		"Name":     "Laptop",
		"Date":     time.Now(),
		"Location": "Unknown",
		"Category": "Cards",
	}
	bodybytes, _ := json.Marshal(body)
	ginContext.Request, _ = http.NewRequest("POST", "", bytes.NewBuffer(bodybytes))
	HandleNewLostItem(ginContext, nil)
	if httpwriter.Code != 400 {
		t.Fatalf("Wrong code")
	}

	// Test type-senstive Category guard
	httpwriter = httptest.NewRecorder()
	ginContext, _ = gin.CreateTestContext(httpwriter)
	body = map[string]interface{}{
		"Name":     "Laptop",
		"Date":     time.Now(),
		"Location": "Unknown",
		"Category": 77,
		"User_id":  "7j0fs",
	}
	bodybytes, _ = json.Marshal(body)
	ginContext.Request, _ = http.NewRequest("POST", "", bytes.NewBuffer(bodybytes))
	HandleNewLostItem(ginContext, nil)
	if httpwriter.Code != 400 {
		t.Fatalf("Wrong code - Assertion type")
	}
}
```
### Example 3: Concurrency Test
Our message queue logic uses some concurrent/parallel programming techniques to achieve high speed. However, this sort of programming can cause a [race condition](https://www.techtarget.com/searchstorage/definition/race-condition) which can be fatal to the backend running or cause very hard to debug bugs.  

In this example, we showcase our testing logic to detect concurrency bugs.  
In this snippet, we test that our unique, incremental id generator `GetJobId` will guarantee that no matter how many concurrent calls are made to it, ALL ids generated by the function are unique.  
This is done by calling the function concurrently and doing a counting sort of the JobIds returned.   
```go
// Ensure that concurrent Read-Write for JobId is unique
func TestGetJobId(t *testing.T) {
	const numTest = 100
	ch := make(chan uint64, numTest)
	rand.Seed(time.Now().Unix())
	for i := 1; i <= numTest; i++ {
        // Concurrently launch GetJobIds calls 
		go func() {
			n := rand.Intn(10)
			time.Sleep(time.Duration(n) * time.Microsecond)
			id := GetJobId()
			ch <- id
		}()
	}
	get := 1
    // Store the values in a counting sort array
	var countSort [numTest + 1]uint64
    // Get the returned JobId values
	for val := range ch {
		countSort[val]++
		get++
        // Last value obtained - close the channel to break from the loop
		if get > numTest {
			close(ch)
		}
	}
    // Check for duplicates
	for _, res := range countSort {
		if res > 1 {
			t.Errorf("Duplicate found")
		}
	}
}
```

## Regression Testing
Regression testing is a software testing practice that ensures an application still functions as expected after any code changes, updates, or improvements.  

When we submit Pull Requests to the UAT and Production branches, a regression test is performed. All tests that we wrote to change a microservice are re-run to ensure that a change to one portion of the microservice does not affect the rest of the microservice.    

## Integration Testing
We set up a staging environment: User Acceptance Testing (UAT) that is essentially a clone of the production website, but with new features being deployed there for testing. There, we test end-to-end, with the UAT frontend site calling the UAT backend and testing for bugs and expected behaviour.  

