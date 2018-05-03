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

#### SCM Controller

#### Payload Mapper

#### API Server

#### Data

#### State DB

#### Linguist

#### Parser

#### Workflow checker

#### Security scanner

#### Workflow builder

#### Notifier

#### SCM Reporter

#### Workflow commiter

#### Workflow starter

#### Build system

## Current status

## Next challenges

## How to contribute

## FAQ
