# FindNUS README :telescope:
**By Team Lost Engineers**,
- [Jin Xuan](https://github.com/jinxuan-owyong) (Frontend)
- [Nicholas](https://github.com/nichyjt) (Backend)
# Foreword & Introduction
Welcome to the FindNUS **documentation** website! This is a living document showcasing our team's efforts during Summer 2022.    

We would like to take this opportunity to express our gratitude to Prof. Jin Zhao for giving us this opportunity to take up Orbital. His enthusiasm and care for the students under Orbital made the experience memorable and meaningful. We are greatly appreciative of his timely reminders and many opportunities provided to level-up our software engineering and computing skills thorugh the Mission Controls.    

We would also like to thank our mentor Ruiping Liu for taking time out of his busy schedule to mentor us for this project. His sharp insights and industry knowledge helped identify gaps in our understanding and guide us to develop a technically comprehensive project. Mentor Ruiping was truly a force multiplier in this project, as his critical appraisal helped give FindNUS the technical edge that we believe squares up to industry standards. 

To our user testers, fellow peer evaluators and our Advisor Hardik Narang, thank you for your invaluable feedback and time spent analysing our project. Your feedback helped push FindNUS' development and helped us identify issues with our project. Without it, FindNUS' development would surely be lacking. We wish the best of luck to our fellow peer evaluators for the smooth evaluation of their projects.

# Table of Contents
- [FindNUS README :telescope:](#findnus-readme-telescope)
- [Foreword & Introduction](#foreword--introduction)
- [Table of Contents](#table-of-contents)
- [Quickstart](#quickstart)
  - [Proposed Level of Achievement](#proposed-level-of-achievement)
  - [What's New? :stars:](#whats-new-stars)
  - [Deployments](#deployments)
  - [Codebase](#codebase)
  - [Poster](#poster)
  - [Video](#video)
  - [Features](#features)
    - [Edge Features](#edge-features)
- [Motivation - Why FindNUS?](#motivation---why-findnus)
- [Project Scope](#project-scope)
- [User Guide](#user-guide)
- [Developer Guide](#developer-guide)
- [Technical Documentation](#technical-documentation)
- [Project Logs](#project-logs)
  - [Milestone 1](#milestone-1)
  - [Milestone 2](#milestone-2)
  - [Milestone 3](#milestone-3)

# Quickstart
You are a...  
***User*** wondering how to navigate FindNUS? [Click here.](/userguide/)  
***Developer*** wondering how to work on FindNUS? [Click here.](/devguide/)  
***Employer*** interested in FindNUS's user research and design ? [Click here.](/problem)    
***Software Engineer*** interested in the inner workings + engineering practices of FindNUS? [Click here.](/technical/)  
***Evaluator*** for Orbital? [Start here.](#whats-new-stars)   

## Proposed Level of Achievement
FindNUS aims to achieve **Artemis** level.  

## What's New? :stars:
In this milestone, we focussed on adding quality of life features to make the searching for lost items much more seamless and 'smart'. The [full release notes are here](/scope/#milestone-3-edge-features).    
- Created an on-demand Lookout service powered by NLP to help Losters search the database for possible matches to their lost item
- Created an asynchronus Lookout service that Losters can subscribe to by email to recieve updates on any new findins
- Geolocation UI
- User dashboard interface improvements
- Better item preview functionality with more filtering options 

## Deployments
FindNUS is live @ [findnus.netlify.app](https://findnus.netlify.app). If you are here to try FindNUS out, click on the link!   
Staging (User Acceptance Testing) Environment @ [transcendent-beijinho-1ca1f9.netlify.app](https://transcendent-beijinho-1ca1f9.netlify.app) if you're interested in that instead.  

## Codebase
[Our github repository](https://github.com/FindNUS).

## Poster

## Video

## Features
The full featureset is documented under our [project scope](/scope), but for visibility, this is a brief summary of what FindNUS can do.  
1. **Authentication (OTP)**  
    
    Users who want to submit a lost item will need to create an account. The Loster dashboard and lost item submission pages are protected routes that will only allow access if the user has been authenticated & has an account with FindNUS 

2. **Item Preview on Homepage**

    Users should be able to see the latest found items on the homepage. Their item may be recently found and added to the database.  

3. **Filter Preview by Category**  

    Users can filter the latest found items by category on the homepage if they are absolutely sure of their lost item category, such as Cards.   

4. **Creation of Lost/Found Item**

    Users are able to fill up a simple form to seamlessly submit a Lost & Found item to the database. 

5. **Loster User Dashboard**

    Losters should have a dashboard to view and edit their Lost item records and to view their various information.   

6. **Editing & Deleting details of Lost item**  

    Users can edit and delete their lost item in their dashboard

7. **Stupid Simple Searching (SSS)** for Found items   

    Users can intuitively just search for whatever on the searchbar. SSS is able to handle **minor typos** and knows how to handle your query. No need for joining queries or fumbling with logical AND/OR operators.  


### Edge Features 
These are additional features we developed for Milestone 3.
1. **Google Maps Integration**  
   
   Ability to specify on Google maps exactly on the Lost and Found item whereabouts. Includes embedded google maps UI as well as ability to autodetect locations in the form field.  
 
2. **NLP-powered Lookout Service**  

    Let FindNUS search for you on-demand. Based on your lost item, FindNUS uses NLP and ElasticSearch magic to find found items that are possible matches for your lost item. 

3. **Subscribe to Lookout Email Notifications**
    
    Based on our lost item that you subscribed to, FindNUS will periodically search using the Lookout Service for possible item matches, and email you about them.  

4. **More robust preview filtering**  
    
    Some users may want to narrow down the preview filters. We added the option of filtering preview results by date and allowing larger pagination values.  

5. **Email verification**

    Users can be verified via email which will unlock more features of the webiste to them, such as Item Lookout Subscriptions.

# Motivation - Why FindNUS?
FindNUS was created because we feel that the current Lost and Found (LNF) system in NUS **sucks**.  

It is decentralized and messy. The official Lost and Found vendor that serves NUS, [RepoApp](https://secure.repoapp.com/public_items/BB20556C) and unofficial telegram groups don’t put user experience first and are generally hard to navigate.  

In our [**Problem Research Page**](/problem), We deep dive into our **project aim** and deepened our understanding of the LNF problem on campus with our  where we document our **user stories** and **LNF competitor analysis**.  

# Project Scope
In our [Project Scope](/scope), we document each Orbital milestone and what features we have accomplished and set forth to do.


# User Guide
Need a detailed guide on navigating FindNUS? [Click here for the User Guide.](/userguide)

# Developer Guide
Want to help out? [Click here for the Developer Guide.](/devguide)

# Technical Documentation
Our [Technical Documentation](/technical) covers a few areas of interest:
- **Challenges Encountered**  
The development journey for FindNUS was full of ups and downs. We document some significant issues we faced during the development of FindNUS.  
- **Architectural Overview**  
We cover key features and architectual design choices
- **User Validation & Testing**  
We cover how we get users to test our app and make changes from there
- **Software Engineering Practices**  
We document our fortnitely sprints, unit testing and more software engineering nuances in our project

# Project Logs
Click the headers to see our project logs in excel format:
## [Milestone 1](https://drive.google.com/file/d/1ZO5gxvZAkBn_qlxdPUVDZ-tJKXu3CFM2/view?usp=sharing)
## [Milestone 2](https://drive.google.com/file/d/1c3h0cu_kSZ0nxxgs7b55iV3B9jGVkwSk/view?usp=sharing)
## Milestone 3