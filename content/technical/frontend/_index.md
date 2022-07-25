---
title: "Frontend Technical Documentation"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
---

![Website](https://img.shields.io/website?down_color=red&down_message=offline&up_color=green&up_message=online&url=https%3A%2F%2Ffindnus.netlify.app%2F)

<!-- omit in toc -->
## Table of Contents
- [Overview](#overview)
- [Getting Started](#getting-started)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Launch the app](#launch-the-app)
- [Tech Stack](#tech-stack)
- [Frontend Design](#frontend-design)
  - [Identity](#identity)
  - [Styles](#styles)
  - [Colours](#colours)
- [Architecture](#architecture)
  - [Overview](#overview-1)
  - [Routing](#routing)
  - [Design Choices](#design-choices)
- [Component Tree](#component-tree)
- [App Routing](#app-routing)
- [Features](#features)
- [Continuous Integration/Continuous Delivery](#continuous-integrationcontinuous-delivery)
- [Footnotes](#footnotes)
 

## Overview

[![FindNUS Homepage](https://i.imgur.com/gaKicrb.png)](https://findnus.netlify.app)

[[Demo](https://findnus.netlify.app)] [[Docs](https://findnus.github.io/)]

FindNUS is a lost and found item management system which aims to supplement existing NUS lost and found system in National University of Singapore (NUS) by reducing the barriers for item finders to submit an item online. As such, item losters are more likely to find an item which they have lost on top of items which only make it to the security personnel. The frontend is built using React 17 and TypeScript, with emphasis on Redux for state management. Sass is also used as the CSS-preprocessor for easier management of styling.

<div align="right"><a href="#table-of-contents">Back to top</a></div>


## Getting Started

A demo of this application can be accessed at https://findnus.netlify.app

The demo backend is available at https://findnus.herokuapp.com

For more information and documentation, please visit https://findnus.github.io/

### Installation

```shell
git clone https://github.com/FindNUS/frontend.git
cd frontend
npm install
```

### Configuration

- Make a copy of [.env.example](.env.example) and rename it as `.env`
- Configure the project in the `.env` file by setting the parameters corresponding to your firebase project, and the path to API

  _Note: The backend setup must be linked to the same firebase project_ 

### Launch the app

- Run `npm start` to initialise the local server

<div align="right"><a href="#table-of-contents">Back to top</a></div>


## Tech Stack

<style>
    .tech-stack--row:not(:last-child) {
        margin-bottom: 10px;
    }
    .tech-stack--logo {
        width: 80px;
        height: auto;
        object-fit: cover;
    }
    .tech-stack--logo:not(:last-child) {
        margin-right: 10px;
    }
</style>
<div class="tech-stack">
    <div class="tech-stack--row">
        <img 
            src='https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg' 
            class="tech-stack--logo"
            title="React"
            alt="React"
        >
        <img 
            src='https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg' 
            class="tech-stack--logo"
            title="TypeScript"
            alt="TypeScript"
        >
        <img 
            src='https://cdn.jsdelivr.net/gh/devicons/devicon/icons/sass/sass-original.svg' 
            class="tech-stack--logo"
            title="Sass"
            alt="Sass"
        >
        <img 
            src='https://cdn.jsdelivr.net/gh/devicons/devicon/icons/redux/redux-original.svg' 
            class="tech-stack--logo"
            title="Redux"
            alt="Redux"
        >
        <img 
            src='https://cdn.jsdelivr.net/gh/devicons/devicon/icons/firebase/firebase-plain.svg' 
            class="tech-stack--logo"
            title="Firebase"
            alt="Firebase"
        >
    </div>
    <div class="tech-stack--row">
        <img 
            src='https://cdn.jsdelivr.net/gh/devicons/devicon/icons/googlecloud/googlecloud-original.svg' 
            class="tech-stack--logo"
            title="Google Cloud"
            alt="Google Cloud"
        >
        <img 
            src='https://symbols.getvecta.com/stencil_25/40_jest.5fde12ec22.svg' class="tech-stack--logo"
            title="Jest"    
            alt="Jest"    
        >
        <img 
            src='https://testing-library.com/img/logo-large.png' 
            class="tech-stack--logo"
            title="React Testing Library"
            alt="React Testing Library"
        >
        <img 
            src='https://avatars.githubusercontent.com/u/44036562?s=280&v=4' 
            class="tech-stack--logo"
            title="GitHub Actions"
            alt="GitHub Actions"
        >
    </div>
</div>

<div align="right"><a href="#table-of-contents">Back to top</a></div>


## Frontend Design

### Identity

<style> 
    .image-logo--rectangle {
        height: 75px;
        width: auto;
        background-colour: #333;
    }
    .image-logo--square {
        height: 100px;
        width: 100px;
        object-fit: contain;
    }
</style>

| Logo Type                    | Description                        | Image                                                                                                                     |
| ---------------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Main Logo (Green/Red)        | For use with light backgrounds     | <img src="https://raw.githubusercontent.com/FindNUS/.github/main/logos/Logo_Green_Red.png" class="image-logo--rectangle"> |
| Main Logo (White/Red)        | For use with non-white backgrounds | <img src="https://raw.githubusercontent.com/FindNUS/.github/main/logos/Logo_White_Red.png" class="image-logo--rectangle"> |
| Compressed Logo              | -                                  | <img src="https://raw.githubusercontent.com/FindNUS/.github/main/logos/Icon_Square_No_BG.png" class="image-logo--square"> |
| Compressed Logo with Backing | Also used as favicon               | <img src="https://raw.githubusercontent.com/FindNUS/.github/main/logos/Icon_Square_BG.png" class="image-logo--square">    |

### Styles

__Font:__ Dosis (https://fonts.google.com/specimen/Dosis)

__Icons:__ Material Icons (https://fonts.google.com/icons) 

### Colours

<style> 
    .colour-bubble__container {
        display: flex;
        gap: 10px;
        align-items: center;
    }
    .colour-bubble {
        height: 20px;
        width: 20px;
        border-radius: 50%;
        border: 1px solid #ccc;
    }
    .colour-bubble--xmas-green {
        background-color: #135A60;
    }
    .colour-bubble--gold {
        background-color: #C9A27C;
    }
    .colour-bubble--white {
        background-color: #FFFFFF;
    }
    .colour-bubble--xmas-red {
        background-color: #A52C49;
    }
</style>

<div class="colour-bubble__container">
    <div class="colour-bubble colour-bubble--xmas-green"></div>
    <div> 
        Christmas Green (#135A60)
    </div>
</div>
<div class="colour-bubble__container">
    <div class="colour-bubble colour-bubble--xmas-red"></div>
    <div> 
        Christmas Red (A52C49)
    </div>
</div>
<div class="colour-bubble__container">
    <div class="colour-bubble colour-bubble--gold"></div>
    <div> 
        Gold (#C9A27C)
    </div>
</div>
<div class="colour-bubble__container">
    <div class="colour-bubble colour-bubble--white"></div>
    <div> 
        White (#FFFFFF)
    </div>
</div>

<div align="right"><a href="#table-of-contents">Back to top</a></div>

## Architecture
### Overview
![Architecture Overview](https://i.imgur.com/Z1u49rf.jpg)

### Routing
![Routing](https://i.imgur.com/B8dqBJ9.png)

### Design Choices

__React__ was chosen as the frontend framework to build a single-page application, which helps reduce the loading time between pages, while reducing bandwidth as same resources are not loaded across multiple pages[^1].

__Redux__ was chosen to aid in state management, which can not only ensure immutable and predictable states[^2], but also help us to avoid lifting states through multiple components[^3], especially ones which do not require the state, giving us cleaner and manageable code.

__TypeScript__ allows us to catch errors both during development and compilation. As JavaScript being an interpreted language, type errors are likely to surface at the production stage, due to the use of loosely defined, and possibly undefined types. TypeScript enforces static typing, and performs null checking, which helps with early bug detection and saves time wasted on debugging later[^4].

__Prettier__ is used as the code formatter to ensure consistent formatting across different workspaces. It also allows for customised formatting which helps various coders better understand one another’s code.

__Sass__, a CSS pre-processor assists with writing more efficient styling. The Sass code formatting allows the coder to better manage various styles using the Block-Element-Modifier (BEM) naming convention[^5]. This standardises the naming conventions, providing us with structured CSS and ensuring code maintainability in the long term.

__ESLint__ catches and raises common errors in ECMAScript code. This helps us to reduce the use of bad practices, while writing more efficient and less redundant code.

## Component Tree

![Component Tree](https://i.imgur.com/rfV62hT.png)

## App Routing

| Route                | Page                                 | Remarks                                   |
| -------------------- | ------------------------------------ | ----------------------------------------- |
| `/`                  | Main page                            |                                           |
| `/search`            | View search results                  |                                           |
| `/view`              | View detailed information about item | Redirects from home, search and dashboard |
| `/login`             | User authentication                  |                                           |
| `/dashboard/profile` | User profile                         | Requires authentication                   |
| `/dashboard/items`   | User-uploaded items                  | Requires authentication                   |
| `/submit-item/type`  | Select submit item type              | Submit either lost or found item          |
| `/submit-item/form`  | Form to submit item                  | Query `type=lost` requires authentication |

<div align="right"><a href="#table-of-contents">Back to top</a></div>

## Features

For more details on our features, click [here](../../#features) for more information.

## Continuous Integration/Continuous Delivery

Changes to the application are continuously tested with GitHub Actions and Netlify to ensure code functionality. For more information, refer to [software engineering](../../swe/#frontend) and [unit testing](../../uiux/unittesting/#frontend)

<div align="right"><a href="#table-of-contents">Back to top</a></div>


## Footnotes

[^1]: https://www.netsolutions.com/insights/single-page-application/ 
[^2]: https://redux.js.org/introduction/getting-started 
[^3]: https://redux.js.org/faq/general#when-should-i-use-redux 
[^4]: https://radixweb.com/blog/typescript-vs-javascript#advantages 
[^5]: https://en.bem.info/methodology/naming-convention/
