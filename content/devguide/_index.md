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
    - [Configuration](#configuration)
    - [Launch the app](#launch-the-app)
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


# Frontend
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

# Backend
To work on backend features and bugfixes, the first thing you want to do is set up the development environment
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
If you are working on the HTTP router that interfaces with the Frontend, **you must download this** in order to work on the Backend RESTul API documentation.  
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
The above is a trivial test case for demonstration purposes. **It is not rigorous enough for production** You should ideally design your testcases to cover all sorts of edge cases. If you need to use a file to store testcase data, simply make a `test` directory within `internal/{Microservice Name}` and store your txt/json/whatever data there. You can get inspiration from [here](/technical/unittesting/).  

## Secrets Management
Secrets are exposed to the Docker container via enviroment variables.  

- If you are adding features that need secrets such as an API key, ping the maintainer to have it registered under the official findnus email and to be added to the repository secrets list on Github.
- Update the following files to ensure that the secrets are being passed to the program at Deploy time
   1. `/.github/workflows/deploy_<microservice>.yml`
   2. `/.github/workflows/test_<microservice>.yml`
   3. `/build/<microservice>.Dockerfile`


Secrets should NEVER be exposed as plaintext in your code. If you need to test locally, consider creating a `secrets` folder that is added to the `.gitignore` to store the confidential information that can be loaded on demand. For example: 
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


# Pull Request (PR) Etiquette
We follow a strict PR flow to ensure changes do not break FindNUS backend.  
1. We compile all experimental/fresh changes into the dev branch
2. The dev branch is put through regression unit testing. Once passed, it is PR-ed into UAT (staging) environment for system testing
3. The UAT environment, once tested will be merged with `main` as a release

PR into `UAT` and `MAIN` will be done by key appointment holders/maintainers as they involve Heroku deployment checking and debugging. For all other purposes, when you PR into dev, you will be subject to a Unit Test of your code as well as a **code review** by the maintainer before it gets accepted into dev.  

`<feat>/<name>-<date>` -> `dev` -> `uat` -> `main`  

Your PR should be **descriptive** and have a detailed **changelog**, referencing issues where appropriate.  
