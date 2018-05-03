# VASTNESS

## Continuous Quality Platform

Vastness is the implementation of the [Quality Manifesto](qualitymanifesto.io) for entire CI/CD stack. It can be seen as a replacement of build servers like Jenkins, Teamcity, Bamboo. But this explanation would be too simplistic - ambitions of the platform are way bigger. The goal is to bring the same revolution as Docker and Kubernetes brought to DevOps world, but in Dev/QA area. With this project we want to make quality important, easy and fascinating. 

## Vastness overview

There are four pillars in Quality Manifesto - here is how Vastness is going to implement them:

### Obvious:
+ Made for humans: use as easy as possible syntax to define pipelines and configuration
+ Stored with the code: no UI for configs on vastness, everything defined in the SCM repository and a plugin for your SCM server
+ Integrated into developer workflow: works with modern development tools, IDEs...
+ With predefined templates: come with the tooling for all languages, build tools, test tools...

### Complete
+ From first line of code to running deployment: collect data from every stage, don't stop tracking the commit once it gets deployed
+ Covers every environment: local, test, production, it's all the same
+ Covers all types of testing: make testing complete, recommend new test types
+ Challenges assumptions: don't trust tests blindly, check their quality, challenge test coverage

### Smart
+ Detects as much as possible: analyse the code and detects things like languages, build tools
+ Smart feedback: provide meaningful information from builds, for pull requests
+ Big data + machine learning: analyse all the coming data and provide knowledge

### Informative
+ Fast feedback: fail fast, split jobs into subtasks
+ Gather all the data: collect every possible piece of information about code
+ No information overload: return only useful information
+ Actionable quality: only show alerts that can be acted on

## Target audience
Main user group would be bigger companies with multiple programming teams that have a big amount of projects, including a substantial amount of complex ones. For smaller teams or single projects, it would be best to deploy Vastness centrally and offer it as a service offering, in a similar way to Travis for Github.

## The big picture

![Vastness Overview](https://raw.githubusercontent.com/vastness-io/website/master/images/BigPicture.png)

#### SCM source
Your source server - Github, Gitlab, Bitbucket

#### Metadata source
Place where additional information is stored, for example Slack channel for notifications, deployment targets. It can be an SCM server plugin.

#### Commit Scanner
Collection of services that process all events coming from SCM. Examples would be parsing commits for new programming languages, updating pipeline definitions, notifying SCM about results. It's one of the two biggest building blocks, alongside build system.

#### Data
Central database storing information about everything related to the code, from the first commit till a system running in production.

#### Language snippet registry
Repository od small code snippets with their dependencies and metadata. It can store multiple languages of snippets, in our case it's Dockerfile snippets for generating build executors and Pipeline steps for creating job definitions. It has built-in topological sorting for resolving dependencies.

#### Workflow builder
Generator of workflow pipelines, based on results of commit scanner. Talks to snipper registry to translate requirements into sorted output.

#### Worker builder
Generator of container-based workers for executing builds. Talks to snipper registry to translate requirements into docker images.

#### Build system
Set of services and tools managing the entire build system. It includes modules like queues, queue managers, resource managers, state memory, secrets manager.

#### Notifier
Set of tools for notifying about events and build results. It would include things like reporting back to SCM, Slack notifications, emails.

#### Test flow & Test toolset
Set of internal and external tools that get triggered by the build system. Some of them can be calls to external services.

#### Deployment flow
Set of tasks and services responsible for deploying the application.

#### Registry
External services that accept build artifacts, so it can be Docker registry, npm registry, jar storage.

#### Live deployment
Running deployed application, that feeds data related to pushed code back to database.

#### Dashboards, alerts, reports
All services responsible for alerting and monitoring of all actions around the code.

#### Machine learning & Pattern predictor
Services that would use the stored data for many actions. Some possibilities: looking for trends in commit quality (e.x. notify developer if his quality is getting lower), starting idle workers when more commits are expected.


## First stages


![CommitScanner](https://raw.githubusercontent.com/vastness-io/website/master/images/CommitScanner.png)


#### SCM & Metadata 
Code repositories and associated metadata.

#### SCM Controller
Service that validates incoming events from SCM and passes them to payload mapper.

#### Payload Mapper
Mapping from multiple SCM formats into a standard Vastness one, so they can be uniformly processed later.

#### API Server
The most important building block in that area of Vastness. It is responsible for taking SCM events and dividing them into subtasks. It then communicates with services that implement subtask steps and transfers data between them. All results get reported to central database.

#### Data
Central database with all code information and results.

#### State DB
Database to back up state of queues and tasks from API server.

#### Linguist
A service that scans incoming events to detect changes in used programming languages and build and test tools.

#### Parser
A service that scans contents of config files for information, e.x. pom.xml

#### Workflow checker
A service that checks if build pipeline has to be modified.

#### Security scanner
Possible security checks in the commits, e.x. adding credentials.

#### Workflow builder
A service to generate workflow definition based on results of previous steps.

#### Notifier
Set of services to notify of results into all possible channels, e.x. Slack, email.

#### SCM Reporter
Reporting back to SCM about results.

#### Workflow commiter
Creates a Pull Requests back to repository if there was a change in workflow definition file.

#### Workflow starter
Starts a job on the build system for the processed event.

#### Build system
Set of services that execute the workflow.

## Current status

## Tech stack
Current microservices are written in *Golang* and we see it as a preferred choice for development of most future components. There are no frontend instances yet and choice for language has not been made for it. Pazuzu registry is currently in Java with Spring, but it requires heavy rewriting and it may be changed into Golang too.

## Next challenges

### Self-registering subtask implementations

API Server in Commit Scanner module and also the Build System require a flexible way of executing steps. For that we want to define in the server basic step (subtask) definitions (interfaces) that can be implemented by external services. Only when all required steps are implemented, the server becomes healthy and available for processing requests. It is possible to have multiple services implementing a step, based on rules (e.x. for PCI-compliant repositories; only Github commits, but not Bitbucket ones). Every step definition has the trigger rules, incoming payload, outgoing payload. There is also a possibility to implement undefined steps, and it requires declaring the order in the queue of steps. 
Our research did not find a suitable library or software that would allow such a specific software discovery/plugin system, so it has to be developed here, probably as a separate project, so it can be used by other people having similar usecase.

## How to contribute
We are looking for all people passionate about quality:
+ Backend developers proficient in Golang
+ Frontend developers (yes, we need a better website than Github Pages)
+ DevOps specialists
+ QA Engineers - for defining workflows and services
+ Data Science & Machine Learning

Please do drop us a line and we will add you to the slack channel :)

## FAQ
