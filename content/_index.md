# FindNUS README :telescope:
**By Team Lost Engineers**,
- [Jin Xuan](https://github.com/jinxuan-owyong) (Frontend)
- [Nicholas](https://github.com/nichyjt) (Backend)
# Foreword & Introduction
Welcome to the FindNUS **documentation** website! This is a living document showcasing our team's efforts during Summer 2022.    

We would like to take this opportunity to express our gratitude to Prof. Jin Zhao for giving us this opportunity to take up Orbital. His enthusiasm and care for the students under Orbital made the experience memorable and meaningful. We are greatly appreciative of his timely reminders and many opportunities provided to level-up our software engineering and computing skills thorugh the Mission Controls.    

We would also like to thank our mentor Ruiping Liu for taking time out of his busy schedule to mentor us for this project. His sharp insights and industry knowledge helped identify gaps in our understanding and guide us to develop a technically comprehensive project. Mentor Ruiping was truly a force multiplier in this project, as his critical appraisal helped give FindNUS the technical edge that we believe squares up to industry standards. 

To our user testers, fellow peer evaluators and our Advisor Hardik Narang, thank you. Thank you for your feedback and time spent analysing our project. Your feedback is invaluable and helped push FindNUS' development. Without it, FindNUS' development would surely be lacking. We wish the best of luck to our fellow peer evaluators for the smooth evaluation of their projects.

# Table of Contents
- [FindNUS README :telescope:](#findnus-readme-telescope)
- [Foreword & Introduction](#foreword--introduction)
- [Table of Contents](#table-of-contents)
  - [Quickstart](#quickstart)
  - [Proposed Level of Achievement](#proposed-level-of-achievement)
  - [Deployments](#deployments)
  - [Codebase](#codebase)
  - [Poster](#poster)
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

## Quickstart
You are a...  
***User*** wondering how to navigate FindNUS? [Click here.](/userguide/)  
***Developer*** wondering how to work on FindNUS? [Click here.](/devguide/)  
***Employer*** interested in FindNUS's user research and design ? [Click here.](/problem)    
***Software Engineer*** interested in the inner workings + engineering practices of FindNUS? [Click here.](/technical/)  
***Evaluator*** for Orbital? [Start here.](#project-scope)   

## Proposed Level of Achievement
FindNUS aims to achieve **Artemis** level.  

## Deployments
FindNUS is live @ [findnus.netlify.app](https://findnus.netlify.app). If you are here to try FindNUS out, click on the link!   
Staging (User Acceptance Testing) Environment @ [transcendent-beijinho-1ca1f9.netlify.app](https://transcendent-beijinho-1ca1f9.netlify.app) if you're interested in that instead.  

## Codebase
[Our github repository](https://github.com/FindNUS).

## Poster

## Features
1. **Authentication (OTP)**  
    
    Users who want to submit a lost item will need to create an account. The Loster dashboard and lost item submission pages are protected routes that will only allow access if the user has been authenticated & has an account with FindNUS 

2. **Filter Preview by Category**
3. **Creation of Lost/Found Item**
4. **Loster User Dashboard**
5. **Editing & Deleting details of Lost item**  

    Users can edit and delete their lost item in their dashboard

6. **Stupid Simple Searching (SSS)** for Found items   

    Users can intuitively just search for whatever on the searchbar. SSS is able to handle **minor typos** and knows how to handle your query. No need for joining queries or fumbling with logical AND/OR operators.  

7. **Item Preview on Homepage**

### Edge Features 
These are additional features we developed for Milestone 3.
1. **Map Display**  
   
2. **NLP-powered Lookout Service**  

    Let FindNUS search for you on-demand. Based on your lost item, FindNUS uses NLP and ElasticSearch magic to find found items that are possible matches for your lost item. 
3. **Subscribe to Lookout Email Notifications**
    
    Based on our lost item that you subscribed to, FindNUS will periodically search using the Lookout Service for possible item matches, and email you about them.  
4. **More robust preview filtering**  
    
    Some users may want to narrow down the preview filters. We added the option of filtering preview results by date and allowing larger pagination values  
5. **Email verification**

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