# What is DevOps

## About this article

This article is targeted for organizational approach towards DevOps and bridging the gap between expectations and variance in DevOps role.

## Role of DevOps

Though almost every computer engineer is familiar with the term DevOps, but only some of them know the crux of it. What I learnt from the candidates' interview experiences, which are posted online and discussed with my friends who are working as DevOps engineers, is that organizations are somehow missing the basic ideology. That's why most of the interviewers are focusing only on either python programming or AWS solution architect questions to test and evaluate the candidates while the real story is a bit different.

## What should be the DevOps?

DevOps can be defined as *a is a set of practices, including both development and operational aspects for managing the infrastructure, which helps to achieve agility in dynamic environment for rapid and sustainable software development.* In simple terms, DevOps is a type of SDLC (Software Development Life Cycle). Its phases range from `plan` to `release` similar to that of Agile, Waterfall. 

In general, DevOps consists of phases namely `plan`, `code`, `build`, `test`, `release`, `operate` and `monitor`. In case of DevOps, interesting thing is one can use and modify required phases of DevOps life cycle as per need of the project. For example, in the phase of `planning`, you must know how to use Git, how to send and update commits between Git client and `GitHub.com`. You need to have knowledge of Git in terms of GUI and CLI to master the `planning` phase. Similarly, you need to learn about several tools and technologies related to other phases of DevOps SDLC.

Though it looks scary at first, it will be simple if you are consistent at learning tools and technologies stepwise. Following are some of my recommendations if you're getting into DevOps:

- **Plan** - `Git`, `Mercurial`, `Bitbucket` for Version Control System
  
- **Code** - `Python` is preferred still one should also know `Shell` and `Golang`

- **Build** - `Ant` and `Maven` for building softwares

- **Test** - `Selenium` for automation testing or `Pytest` for native test library

- **Release** - `Jenkins` for CI/CD (Continuous Integration/Continuous Deployment) or `AWS CodePipeline` like web services for release management

- **Deploy** - `Ansible` or `Chef` for infrastructure automation

- **Operate** - `Docker` or `K8s` (Kubernetes) for infrastructural operations

- **Monitor** - `Nagios` for infrastructure monitoring tool

## DevOps is not about

- Python developer who'll learn all tools overnight
- Software engineer trying to become Site Reliability Engineer
- Someone who knows about solution architecture of AWS components but not about on-premise tools
- Someone who can't pickup operational part quickly and effectively
- Someone who is not interested in system administration but only writing the code.

## What does DevOps engineer do?

DevOps engineer cares about SDLC and its principles rather than just learning the tools. For example, if some developer needs to test new software on MongoDB for which you don't have dedicated infrastructure available due to budget restrictions but client needs to check fault tolerance of the application. In such a case, Docker comes to the rescue. Launching multiple Docker containers on cloud based or on-premise infrastructure help to understand fault tolerance of that application.

In general, some of the requirements for DevOps engineer are:

- Knowledge of Linux system administration or at least have curiosity because no one knows which tool your company wants you to use on Linux
- Know about Linux command and shell scripting because you're going to spend most of your time with it
- Python up to the level that one can write automation script using native and third-party libraries
- Git and GitHub to commit and manage code both at remote and on-premise as well
- Docker and Kubernetes, like containerization, platform to test any software before putting it into the production.
- Jenkins to build and manage the process of software release and so on.

I hope this short article gives you good idea about DevOps profile expectations and variance from organization and job seeker point of view.

---
Let me know about your feedback over the email.

And don't forget to subscribe to my newsletter, [It's about CSE](https://tinyletter.com/mayurp7), for exciting contents and news in the world of computer science.
