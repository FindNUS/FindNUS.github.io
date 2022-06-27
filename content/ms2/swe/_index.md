---
title: "Software Engineering Documentation"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
---

## Table of Contents
- [Sprint](#sprint)
  - [Code Review](#code-review)
- [Backend](#backend)
  - [API Documentation](#api-documentation)
    - [Backend Milestone 2 API Documentation](#backend-milestone-2-api-documentation)
  - [CI/CD](#cicd)
    - [Code Testing](#code-testing)
      - [Example of Passing Unit Test:](#example-of-passing-unit-test)
      - [Example of Failing Unit Test that helped us troubleshoot issues before deploying to a live environment:](#example-of-failing-unit-test-that-helped-us-troubleshoot-issues-before-deploying-to-a-live-environment)

# Sprint
We follow a sprint of two weeks, tracked via Github Projects.
This is a snapshot of the three sprints that we have done so far in the project: 
![sprint overall](sprint.png)


## Code Review
During our fortnightly meeting with our mentor, code reviews were done by the mentor and we worked on implementing changes based on the review. 

# Backend

## API Documentation
Good API documentation is good SWE practice for backend. It reduces ambiguity in API usage and is important for knowledge retention for when new developers come and old developers go. This industry standard also makes it possible for computers to know how to interface with the API. 
We documented the backend API using the [**OpenAPI3** specification](https://swagger.io/specification/). 

Snippet of how the YAML OpenAPI3 specs look like:
```yaml
paths:
  /item:
    post:
      description: |
        Add new Lost item to be put on Lookout on the database.
      parameters:
      - in: header
        name: Authorization
        description: Firebase ID token of user 
        required: true
        schema:
          type: string
          example: "Authorization: my-firebase-idToken"
      requestBody:
        description: Callback item payload
        content:
          'application/json':
            schema:
              $ref: "#/components/schemas/NewItem"
      responses:
        '200':
          description: Item registered into database
        '400':
          description: Rejected new item into database
        '401':
          description: Firebase credentials not invalid
```
This is not so human readable, so we made use of [open source openapi to markdown generator](https://github.com/openapi-contrib/openapi3-generator) to develop Human-friendly docs.

### [Backend Milestone 2 API Documentation](./apisample/)  

<div align="right"><a href="#table-of-contents">Back to top</a></div>

## CI/CD
We leveraged Github Actions to automate **testing** and **continuously deploy** our code.  
This ensures that code works properly on a proper End to End environment before it goes live to production.

CICD history snapshot:
![Backend CICD evidence](backendCICD.png)

<div align="right"><a href="#table-of-contents">Back to top</a></div>

### Code Testing
Code testing is covered in depth under the [code test section](../uiux/unittesting/).
#### Example of Passing Unit Test:  
![Backend unit test pass](unit_test_eg.png)
#### Example of Failing Unit Test that helped us troubleshoot issues before deploying to a live environment:  
![Backend unit test fail](unit_test_eg2.png)

<div align="right"><a href="#table-of-contents">Back to top</a></div>
