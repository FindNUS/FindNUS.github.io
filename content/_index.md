# FindNUS README :telescope:

**By Team Lost Engineers**

| Name     | Scope    | GitHub                            | Email                    |
| -------- | -------- | --------------------------------- | ------------------------ |
| Jin Xuan | Frontend | https://github.com/jinxuan-owyong | jinxuan.owyong@u.nus.edu |
| Nicholas | Backend  | https://github.com/nichyjt        | nicholas.yek@u.nus.edu   |

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
  - [Features & Justifications](#features--justifications)
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
In this milestone, we focussed on adding quality of life features to make the searching for lost items much more seamless and 'smart'. The [full release notes for Milestone 3 are here](/scope/#milestone-3-edge-features).    
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

![FindNUS Poster](https://github.com/FindNUS/.github/raw/main/profile/img/5014.png)

## Video

<iframe 
  src="https://drive.google.com/file/d/1nR3jcpxzYurjFBZC3bAsQacNTzcjAwro/preview" 
  width="640" 
  height="360" 
  allow="autoplay picture-in-picture" 
  allowfullscreen
></iframe>

## Features & Justifications
The full featureset is documented under our [project scope](/scope), but for visibility, this is a overview of the core features for FindNUS.   
1. **Authentication (OTP)**  
    
    Users who want to submit a lost item will need to create an account. The Loster dashboard and lost item submission pages are protected routes that will only allow access if the user has been authenticated & has an account with FindNUS.  

    This feature is important as there are certain features that only makes sense for certain user roles, such as the Loster. Thus, to properly protect these routes, the user needs to be authenticated via a login.  

2. **Item Preview on Homepage**

    Users should be able to see the latest found items on the homepage. Their item may be recently found and added to the database.  

    This feature was added as we felt that for users that just lost their item, there is a high chance that their item might be one of the most recent found items. By showing a preview of the latest found items in FindNUS, Losters may be able to find their lost item in the homepage itself. This eliminates the need to serach for the lost item in the first place, which saves the loster time and effort.  

3. **Filter Preview by Category and Date**  

    Users can filter the latest found items by category on the homepage if they are absolutely sure of their lost item category, such as Cards.   

    This feature was added based on [user feedback (#1)](technical/usertesting/#feature-requests). Users felt that if the preview was too cluttered and there are too many items on the database, there needs to be some way to preview the recent lost items in a more narrow way. By adding date and category filters, the landing page preview will be more focussed and be more useful to the user in batch-searching for their item.

4. **Creation of Lost/Found Item**

    Users are able to fill up a simple form to seamlessly submit a Lost & Found item to the database. This feature is absolutely core to FindNUS, as user-submissions are the lifeblood of FindNUS.  

5. **Loster User Dashboard**

    Losters should have a dashboard to view and edit their Lost item records and to view their various information.   

    This feature is necessary as the lost items are tagged to a user. Every Loster's state is retained on our database (for example, how many lost items they have) as well as various metadata like their User_id. To display this important information, we created a dashboard for logged in Losters so that they can manage their lost item submissions and personal profile.   

6. **Editing & Deleting details of the Lost item**  

    Users can edit and delete their lost item in their dashboard.  
    
    This feature was added to account for the case when Losters have already found their lost item or need to amend details of the item. The edit function allows detail amendment of their lost item, which may help improve the accuracy of the automated search function (Lookout Service) that FindNUS provides. This is also important if the lost item is a 'cold' case, as the user can unsubscribe from email notifications. The delete function allows users to be able to take ownership of their data and remove their item from the database.  

7. **Stupid Simple Searching (SSS)** for Found items   

    Users can intuitively just search for whatever on the searchbar. SSS is able to handle **minor typos** and knows how to handle your query. No need for joining queries or fumbling with logical AND/OR operators.  

    This feature is one of the value-added functions of FindNUS. Going through pages of items might be useful for large-scale searching, but it is not fast and can be inefficient for large amounts of items. Users should be able to quickly hone in to what they want to find. By creating a easy search system that is resistant to typos (which users often make), users can benefit from quickly finding the most relevant search esults to what keywords they know are specific to their LNF item, such as color, brand and location.   


### Edge Features 
These are additional features we developed for Milestone 3.
1. **Google Maps Integration**  
   
   Ability to specify on Google maps exactly on the Lost and Found item whereabouts. Includes embedded google maps UI as well as ability to autodetect locations in the form field.  

   The addition of Google Maps integration is a significant Quality-of-life improvement for FindNUS. This feature is significant to FindNUS as users who are looking through the Found Items page will need to know where exactly the lost item is left at (if it is not held by the founder). By pinpointing exactly where the item is located on google maps, Losters can know exactly where and how to travel to the found item's location via google maps. This saves them effort of having to search the whole vicinity for their item.   
 
2. **NLP-powered Lookout Service**  

    Let FindNUS search for you on-demand. Based on your lost item, FindNUS uses NLP and ElasticSearch magic to find found items that are possible matches for your lost item. 

    This feature was added based on [user feedback (#6)](technical/usertesting/#critical-issues). This feature is critical to FindNUS users as it automates away the 'searching' process for a lost item. The Lookout Service is called on demand when a user submits a lost item - they [can view possible item matches](technical/backend/#example-on-demand-lookout) and act on this information. This is particularly useful for Losters when there are too many items on the database to effectively search for their item manually. Losters can also skip manual searching altogether if they submit their lost item from the start and the Lookout Service finds the correct found item that exists on the database.  

3. **Subscribe to Lookout Email Notifications**
    
    Based on our lost item that you subscribed to, FindNUS will periodically search using the Lookout Service (#2 above) for possible item matches, and email you about them.  

    This feature is important to Losters using FindNUS as it is possible that the lost item has not been found and submitted to FindNUS, making any searching useless. By allowing users to subscribe to a lookout notification, this automates away the need for the users to keep checking back the website for any changes. FindNUS will automatically detect if there are any good candidates matching the loster's item and notify the loster via email. This saves the Loster much time and effort and can also give them peace of mind knowing that work is being done to help search for their lost item.  

4. **More robust preview filtering**  
    
    Some users may want to narrow down the preview filters. We added the option of filtering preview results by date and allowing larger pagination values.  

5. **Email verification**

    Users can be verified via email which will unlock more features of the website to them, such as Item Lookout Subscriptions.  

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
## [Milestone 3](https://drive.google.com/file/d/1LydHo3vu9g-AJjQfj-dHrBhfA2LPQmmF/view?usp=sharing)