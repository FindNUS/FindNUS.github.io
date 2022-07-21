---
title: "Project Scope"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
emojify: true
---
# Introduction
- [Introduction](#introduction)
- [Milestone 1](#milestone-1)
  - [Frontend](#frontend)
  - [Backend](#backend)
  - [Etc](#etc)
- [Milestone 2](#milestone-2)
  - [Frontend](#frontend-1)
  - [Backend](#backend-1)
- [Milestone 3](#milestone-3)
  - [Frontend](#frontend-2)
  - [Backend](#backend-2)
- [Beyond Orbital](#beyond-orbital)


We organised the timeline into 2-week sprints.  

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
- [Frontend Architecture](/technical/frontend/#architecture) :white_check_mark:
- [Frontend Design Mockups](/technical/frontend/#frontend-design) :white_check_mark:
- App routing between home and login page :white_check_mark:
- User authentication via Firebase :white_check_mark:
- Interfacing with Backend API (GET item) :white_check_mark:
  
## Backend 
- [Backend Architecture](/technical/backend/#high-level-overview) :white_check_mark:
- Build HTTP Router to serve FindNUS RESTful API :white_check_mark:
- Authenticate requests using Firebase API :white_check_mark:
- Simple CRUD operations with MongoDB :white_check_mark:
- Dockerize :whale: the backend :white_check_mark:
- Simple CI/CD with Github actions and Using heroku's docker container registry :white_check_mark:
- [Extensive research](/technical/backend/#appendix-a-backend-design-choices) to choose the best backend stack :white_check_mark:
- [Document backend API](/technical/swe/apisample/) using OpenAPI3.0 specs 
## Etc
- Use of 'Kanban' style boards in Github Projects to manage project :white_check_mark:

# Milestone 2
In this milestone, we focussed on building the core features of FindNUS. We aimed to complete the following:  
- **End to End CRUD of lost and found items**
- **Stupidly Simple Searching (SSS) of found items**
- **Preview on homepage of recent found items**
- **CICD for frontend and backend**

## Frontend 
- Item Submission Styling :white_check_mark:
- Form field validation :white_check_mark:
- User profile styling :white_check_mark:
- Loster User Dashboard UI :white_check_mark:
- Integrate with backend to get preview of recent items :white_check_mark:
- Filter preview by category :white_check_mark:
- CircleCI integration for CICD :white_check_mark:
  
## Backend 
- Dockerize a 'Item' microservice to handle CRUD requests :white_check_mark:
- Use RabbitMQ as Message Brokering for inter-microservice communication :white_check_mark:
- Setup ElasticSearch database and query functions for ***SSS*** :white_check_mark:
- Fully implement CRUD endpoints: `POST PATCH GET DELETE` lost and found items :white_check_mark:
- Pagination logic for larger GET requests (frontend's preview) :white_check_mark:
- Integrate CRUD process with Imgur API to offload image storage and retrieval :white_check_mark:
- More rigorous Unit Testing, with tailored testcases :white_check_mark:

# Milestone 3
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
- Creation of **Lookout** smart service using NLP technology  
- Creation of Email subscription service 
- Integration of geolocation data

# Beyond Orbital
// TODO WIP     
Beyond Orbtial, we aim to launch FindNUS for actual use and see how it performs under real-world usage. If we have enough data, we can look into expanding FindNUS to do things such as detect spam :robot: from ham :meat_on_bone: in the item submission, as well as see how we can leverage QR codes around lost hotspots in campus to quickly submit items on-the-go.  
