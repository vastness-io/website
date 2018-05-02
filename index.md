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

## First stages


![CommitScanner](https://raw.githubusercontent.com/vastness-io/website/master/images/CommitScanner.png)

## Next challenges

## How to contribute

## FAQ
