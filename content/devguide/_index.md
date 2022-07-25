---
title: "Developer Guide"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
emojify: true
---
- [Introduction](#introduction)
- [Frontend](#frontend)
  - [Installation](#installation)
    - [Pre-requisite: Node.js](#pre-requisite-nodejs)
    - [Pre-requisite: Firebase CLI](#pre-requisite-firebase-cli)
    - [Cloning and installing dependencies](#cloning-and-installing-dependencies)
  - [Configuration](#configuration)
    - [Setting up API keys on Google Cloud console](#setting-up-api-keys-on-google-cloud-console)
    - [Setting up Firebase CLI](#setting-up-firebase-cli)
    - [Setting up the .env file](#setting-up-the-env-file)
  - [Launch the app](#launch-the-app)
  - [Branching Strategy](#branching-strategy)
  - [Versioning](#versioning)
- [Backend](#backend)
  - [Installation Guide](#installation-guide)
    - [Pre-requisite: Golang](#pre-requisite-golang)
    - [Pre-requisite: Docker](#pre-requisite-docker)
    - [Pre-requisite: OpenAPI Generator](#pre-requisite-openapi-generator)
    - [Setting up the Codebase](#setting-up-the-codebase)
      - [Installing Golang Microservice Dependencies](#installing-golang-microservice-dependencies)
  - [Building on the RESTful API](#building-on-the-restful-api)
  - [Unit Testing](#unit-testing)
  - [Secrets Management](#secrets-management)
  - [Pull Request (PR) Etiquette](#pull-request-pr-etiquette)
# Introduction
Want to contribute and work on FindNUS? This is the guide for you.  
This guide covers how to setup the development environment for the Frontend and Backend respectively.  


# Frontend
## Installation
### Pre-requisite: Node.js

You will need Node.js to be installed to run npm. We recommend the LTS version of Node.js >= 16.13, which can be downloaded [here](https://nodejs.org/en/) for Windows/MacOS. For installation via package managers, refer to [this page](https://nodejs.org/en/download/package-manager/) instead.

### Pre-requisite: Firebase CLI

Firebase CLI is required for running tests, or if you wish to make amendments to the Emulator Suite. To install, run the following command:

```shell
npm install -g firebase-tools
```

### Cloning and installing dependencies

```shell
git clone https://github.com/FindNUS/frontend.git
cd frontend
npm install
```

## Configuration
### Setting up API keys on Google Cloud console

There are two environment variables required for the Google Maps API integration. You will need to set the following configurations in the Google Cloud console under "APIs & Services" > "Credentials"

| Variable Name                | API Restrictions                         | Application Restrictions   | Website Restrictions                  |
| ---------------------------- | ---------------------------------------- | -------------------------- | ------------------------------------- |
| REACT_APP_MAPS_EMBED_KEY     | Maps Embed API                           | HTTP referrers (web sites) | example.com/* <br /> example.com/\*/* |
| REACT_APP_MAPS_GEOCODING_KEY | Geocoding API <br /> Maps JavaScript API | Same as above              | Same as above                         |


_Note: It is possible to skip this step and use one API key for both environment variables with no application/website restrictions during development. However we __do not__ recommend this to be done in production to prevent unauthorised use of your API key, as it is accessible by the user (Click [here](https://cloud.google.com/docs/authentication/api-keys?hl=en_US&_ga=2.241587970.-1032343160.1658240189#securing_an_api_key) for more information)._

### Setting up Firebase CLI

An authentication token is required for running tests on the Emulator Suite. You may generate the token with the following command:

```shell
firebase login:ci
```

Upon logging in to your Google account, you will be provided with an _access token_ in the command line. Store this key as `FIREBASE_TOKEN`.

### Setting up the .env file

- Make a copy of [.env.example](.env.example) and rename it as `.env`
- Configure the project in the `.env` file by setting the parameters corresponding to your firebase project, the path to API, and the parameters as described above
- Depending on your application environment, `REACT_APP_DEPLOY_ENV` should be set accordingly to `production`, `development` or `test`.

  _Note: The backend setup must be linked to the same firebase project_ 

## Launch the app

- Run `npm start` to initialise the local server

<div align="right"><a href="#table-of-contents">Back to top</a></div>

## Branching Strategy

We follow the [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow#:~:text=Gitflow%20is%20a%20legacy%20Git,software%20development%20and%20DevOps%20practices) branching strategy to ensure we always have a production-ready branch (`main`). All pull requests for feature branches (`feature/*`) should be merged into the `dev` branch. 

<a href="https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow#:~:text=Gitflow%20is%20a%20legacy%20Git,software%20development%20and%20DevOps%20practices" rel="noopener" target="_blank">
<img src="./gitflow-example.png" title="Gitflow Example" style="width: 500px; height: auto; " />
</a>

## Versioning

We follow the [Semantic Versioning 2.0.0](https://semver.org/) standard when publishing [releases](https://github.com/FindNUS/frontend/releases). 

# Backend
## Installation Guide
### Pre-requisite: Golang
You need to have golang >=1.18 installed.
Install guide for [Windows/MacOS](https://go.dev/doc/install).   
Install via Linux Package Managers or MacOS Brew:
```bash
# This varies based on your package manager
$ sudo apt install golang-go 
```
### Pre-requisite: Docker
If you wish to directly build and test the docker microservices for whatever reason, you need to install docker.  
Install guide for [Windows/MacOS](https://docs.docker.com/get-docker/).  
Install via Linux Package Managers or Macos Brew -> This is a [more involved process](https://docs.docker.com/engine/install/ubuntu/).  

### Pre-requisite: OpenAPI Generator
If you are working on the `backend` microservice and changing the HTTP endpoints that interfaces with the Frontend, **you must download this** in order to work on the Backend RESTul API documentation.  
```bash
# Assumes you have npm installed
npm install -g openapi3-generator
```  

### Setting up the Codebase
Simply clone the project and branch out from `dev`.  
```bash
git clone https://github.com/FindNUS/backend.git
# Switch to the dev branch
git branch dev
# Create your own branch to work on some feature
# Branch naming convention example: feat/CatPicture-Integration-120622
git checkout -b <type>/<descripton>-<date DDMMYY> dev
```
#### Installing Golang Microservice Dependencies
Each microservice is logically separated in `/internal/{Microservice Name}`.  
If you are working on, say the `item` microservice, you need to install `item`'s go package dependecies.  
```bash
cd /internal/{Microservice Name}
go get .
```
After that, you are free to work on the files in the project and develop on FindNUS' backend!  

## Building on the RESTful API
If you are modifying/adding a new endpoint or changing anything that **interfaces directly with Frontend**, you MUST update the API documentation.  
The backend API documentation is kept in `/api`. Edit the documentation via `findnus.yaml` in accordance to [OpenAPI3.0 Specs](https://swagger.io/specification/). Once you are done, **build the human-friendly docs** via the build script provided under `/scripts`.  
```bash
# Root directory of project 
cd /scripts
bash build_api_docs.sh
```

## Unit Testing
Where possible, unit test critical functions. This is [easily done in golang](https://go.dev/doc/tutorial/add-a-test).  

For example, to test  `foo.go`, create `foo_test.go` in the same folder.  
Then, in `foo_test.go`, prepend the function to be tested with Test.  
Trivial Example:  
```go
// foo.go
func Add(x int, y int) int{
    return x+y
}
// foo_test.go
func TestAdd(t *testing.T){
    x1 := 2
    x2 := 40
    res := Add(x1, x2)
    if res != 42 {
        t.Fail()
        t.Log("Expected 42 but got", res)
    }
}
```
The above is a trivial test case for demonstration purposes. **It is not rigorous enough for production** You should ideally design your testcases to cover all sorts of edge cases. If you need to use a file to store testcase data, simply make a `test` directory within `internal/{Microservice Name}` and store your txt/json/whatever data there. You can get inspiration from [some of our actual unit test examples here](/technical/unittesting/).  

## Secrets Management
Secrets are exposed to the Docker container via environment variables.  

- If you are adding features that need secrets such as an API key, ping the maintainer to have it registered under the official findnus email and to be added to the repository secrets list on Github.
- Update the following files to ensure that the secrets are being passed to the program at Deploy time
   1. `/.github/workflows/deploy_<microservice>.yml`
   2. `/.github/workflows/test_<microservice>.yml`
   3. `/build/<microservice>.Dockerfile`


Secrets should NEVER be exposed as plaintext in your code. If you need to test locally, consider creating a `secrets` folder that is added to the `.gitignore` to store the confidential information that can be loaded on demand. A boilerplate example used in our live codebase: 
```go
someSecret := os.Getenv("SOME_SECRET")
	var err error
	if someSecret == "" {
		// Read from secrets file
		f, err := os.Open("../../secrets/someSecret.txt")
		if err != nil {
			log.Fatal(err)
		}
		scanner := bufio.NewScanner(f)
		defer f.Close()
		for scanner.Scan() {
			someSecret = scanner.Text()
		}
	}
```

## Pull Request (PR) Etiquette
We follow a strict PR flow to ensure changes do not break FindNUS backend.  
1. We compile all experimental/fresh changes into the dev branch
2. The dev branch is put through regression unit testing. Once passed, it is PR-ed into UAT (staging) environment for system testing
3. The UAT environment, once tested will be merged with `main` as a release

PR into `UAT` and `MAIN` will be done by key appointment holders/maintainers as they involve Heroku deployment checking and debugging. For all other purposes, when you PR into dev, you will be subject to a Unit Test of your code as well as a **code review** by the maintainer before it gets accepted into dev.  

`<feat>/<name>-<date>` -> `dev` -> `uat` -> `main`  

Your PR should be **descriptive** and have a detailed **changelog**, referencing issues where appropriate.  
