---
title: >-
	Kotlin - Configuring a Mutli-modules Project with Gradle
date: 2019-02-17 22:43:00
tags: 
- kotlin
- gradle
- build
---

For the last couple of days, i've been trying to write the introduction for this post, but so far it has been going no where at all. Turn out, writting blog is way more difficult than i thought. I had a vague idea about what i want to write, but i couldn't find the right words to express it, to make it sounds intelligently. And then i remembered a lesson from a [book of Dale Carnegie i've been reading lately](https://www.amazon.com/s?k=9788180320217).

> First, arouse in the other person an eager want. He who can do this has the whole world with him. He who cannot walks a lonely way.

> "You can make more friends in two months by being interested in them, than in two years by making them interested in you." The only way to make quality, lasting friendships is to learn to be genuinely interested in them and their interests

 I realized, i was too focus on trying to show how literate, knowledgable i am rather than actually providing useful knowledge to you readers. I was thinking in term of what i want to show, not what you want to see when you google your way to this blog. That's not helpful to anybody, not even to myself. So i need to forget my perspective, my ego and try to write this post simple, and easy to understand as possible. With 3 questions to understand the subject: **What**, **Why** and **How**.

<!-- more -->

# What

In this post, i'll show you how to create and configure a multi-project build with Gradle and Kotlin language. The project will consists of 3 sub projects: presentation, core and persistence. Each has its own purpose and can be used independantly.


[Click here to go straight to #How where i explain step by step how to do it](#How).

# Why

Splitting code into modules give you the following advantages:

1. **Separation of concern -> Increase readibility, maintainability & decrease complexity**. 
>Code that you do not have to change is less likely to break than code that you do change. So splitting up the concerns helps you to avoid breakage in unrelated features

	Instead of putting everything in one place, **each module** is **separated from one another** and **has only one job**. For example, the module in charge of presentation logic is separated from core business logic, and both are separated from persistence logic. By decoupling the dependency between modules and focusing on the sole unified purpose it serves, code and logic inside said modules can be easier to understand and maintain by even fresher developer while keeping complexity in check, which in turn promotes its reusability and scalibility.

	A real life example, when i first designed a multi-project system for my company. It was a webapp so i splitted it into 3 modules api - to take in charge of webserver related config & handle all request coming, core - where our business logic lie and database - to connect to a Redshift instance and perform CRUD operation. Four months later, the need arised that we need to make another copy of this system, but this time with data store in Clickhouse. Instead of having to rewrite the whole project, all i need was to fork the current system, make another database module and replace the current one with it, without breaking any logic flow from api and core module. 

	Following that, we decided that we need a mobile version of the current webapp. Same as usecase above, only the api module is needed to be replaced. Changes that normally covers the whole system got reduced to only parts that are actually changed, by clear separation of concerns.

2.  **Reusability**
	**Each module** serves a single purpose, **is independant from others** and **can be deployed separately**. So should the need arise, you can easily copy a module right to another project, without the need of any special tinkering.


3. **Faster individual development time -> By reduce wasted build & test time**
Splitting code into modules gives you the oppoturnity to take advantage of [Gradle's parallel execution](https://guides.gradle.org/performance/) feature, so multiple **builds can be executed simultaneously**. Also since they are separated, you don't need to worry about breaking other modules when making changes to one. Only the **changed module is needed to be rebuilt and tested** instead of recompling the whole project. This can drastically reduce wait time when Gradle executes build process, makes development go faster.

	Dependency to 3rd parties is also kept in check, each module depends on different set of dependencies. By exposing dependencies to only module that actually uses it, you can keep build size small, plus reduce the chance of any error or side effect. (Two dependencies having same class name can be mistook for one another for example)


4. **Faster team development time -> By enabling team collaboration** 
One major advantage of using multi-module design is that it is an effective way for developers to collaborate. As i mentioned earlier each module has a specific purpose and is independant from others. Change occur to one module will not affect others. So multiple modules can be developed by different people at the same time without any problem. 


# How 


Let's start by creating a new Gradle Project. 

{% asset_img new_project.png %}

You should get something that roughly looks like this (But definitely not exactly the same !)

{% asset_img inited_project.png %}