---
title: "Project Scope"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
emojify: true
---
- [Milestone 1](#milestone-1)
  - [Frontend](#frontend)
  - [Backend](#backend)
  - [Etc](#etc)
- [Milestone 2](#milestone-2)
  - [Frontend](#frontend-1)
  - [Backend](#backend-1)
- [Milestone 3 (Edge Features)](#milestone-3-edge-features)
  - [Frontend](#frontend-2)
  - [Backend](#backend-2)
- [Beyond Orbital](#beyond-orbital)


# Milestone 1
In this milestone, we focussed on getting a MVP website out.  
We aimed (and managed) to get the following core features done:
- **A live webpage up and running**
- **User Authentication (Login)**
- **Retrieval of demo items from database**
- **Frontend Design Mockups**
- **Working Backend Microservice Architecture** 
- **Extensive research into FindNUS' technical design**

Divide and conquer: We categorised the tasks into Frontend, Backend and other subtasks.

## Frontend 
- [Frontend Architecture](/technical/frontend/#architecture) 
- [Frontend Design Mockups](/technical/frontend/#frontend-design) 
- App routing between home and login page 
- User authentication via Firebase 
- Interfacing with Backend API (GET item) 
  
## Backend 
- [Backend Architecture](/technical/backend/#high-level-overview) 
- Build HTTP Router to serve FindNUS RESTful API 
- Authenticate requests using Firebase API 
- Simple CRUD operations with MongoDB 
- Dockerize :whale: the backend 
- Simple CI/CD with Github actions and Using heroku's docker container registry 
- [Extensive research](/technical/backend/#appendix-a-backend-design-choices) to choose the best backend stack 
- [Document backend API](/technical/swe/apisample/) using OpenAPI3.0 specs 
## Etc
- Use of 'Kanban' style boards in Github Projects to manage project 

# Milestone 2
In this milestone, we focussed on building the core features of FindNUS. We aimed to complete the following:  
- **End to End CRUD of lost and found items**
- **Stupidly Simple Searching (SSS) of found items**
- **Preview on homepage of recent found items**
- **CICD for frontend and backend**

## Frontend 
- Item Submission Styling 
- Form field validation 
- User profile styling 
- Loster User Dashboard UI 
- Integrate with backend to get preview of recent items 
- Filter preview by category 
- CircleCI integration for CICD 
  
## Backend 
- Dockerize a 'Item' microservice to handle CRUD requests 
- Use RabbitMQ as Message Brokering for inter-microservice communication 
- Setup ElasticSearch database and synchronisation logic with MongoDB
- Create Stupid Simple Searching endpoint  
- Fully implement CRUD endpoints: `POST PATCH GET DELETE` lost and found items 
- Pagination logic for larger GET requests (frontend's preview) 
- Integrate CRUD process with Imgur API to offload image storage and retrieval 
- More rigorous Unit Testing, with tailored testcases 

# Milestone 3 (Edge Features)
In this milestone we aimed to increase the **complexity** of our project by making use of **Natural Language Procesing**, **Geolocation + Map data** and **Automated Emailing** to make FindNUS smarter :brain: and more user-centric :family:.  
- On-demand **Lookout** service *powered by NLP* to help Losters search the database for possible matches to their lost item  
- Geolocation UI
- Email **Lookout** Subscription service  
- User dashboard interface improvements 

## Frontend 
- Implement User Profile Updating (Name, email)
- Implement User information collection for new users
- Testing for SMS login
- Setup Mock Fetching for search functionality
- Item update and deletion 
- UI improvements

## Backend 
- Creation of [**Lookout** smart service](http://localhost:1313/technical/backend/#smart-lookout-service-star) using Natural Language Processing technology  
- Creation of Email subscription service as an add-on to the Lookout service
- Integration of geolocation data in database schema

# Beyond Orbital 
Beyond Orbtial, we aim to launch FindNUS for actual use and see how it performs under real-world usage. If we have enough data, we can look into expanding FindNUS to do things such as detect spam :robot: from ham :meat_on_bone: in the item submission, as well as see how we can leverage QR codes around lost hotspots in campus to quickly submit items on-the-go.  
