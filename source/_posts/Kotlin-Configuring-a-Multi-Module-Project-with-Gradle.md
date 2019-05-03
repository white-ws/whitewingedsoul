---
title: >-
	Kotlin - Configuring a Mutli-modules Project with Gradle
date: 2019-02-17 22:43:00
tags: 
- kotlin
- gradle
- build
---

I don't really know what to write...

For the last couple of days, i've been trying to write the introduction for this post, but so far it has been going no where at all. Turn out, writting blog is way more difficult than i thought. I had a vague idea about what i want to write, but i couldn't find the right words to express it, to make it sounds intelligently. And then i remembered a lesson from a [book of Dale Carnegie i've been reading lately](https://www.amazon.com/s?k=9788180320217).

> First, arouse in the other person an eager want. He who can do this has the whole world with him. He who cannot walks a lonely way.

> "You can make more friends in two months by being interested in them, than in two years by making them interested in you." The only way to make quality, lasting friendships is to learn to be genuinely interested in them and their interests

 I realized, i was too focus on trying to show how literate, knowledgable i am rather than actually providing useful knowledge to you readers. I was thinking in term of what i want to show, not what you want to see when you google your way to this blog. That's not helpful to anybody, not even to myself. So i need to forget my perspective, my ego and try to write this post simple, and easy to understand as possible. With 3 questions to understand the subject: **What**, **Why** and **How**.

<!-- more -->

# What

In this post, i'll show you how to create and configure a multi-project build with Gradle and Kotlin language. The project will consists of 3 sub projects: presentation, core and persistence. Each has its own purpose and can be used independantly.

Click here to go straight to #How where i explain step by step how to do it.

# Why




point trying to prove: 
- first touched system was a monolithic, where every part of the system intertwines with another.
- code were hard to read, hard to maintain

- objective: separation of concerns
- purpose of design principles: enable team collaboration & speed up development process




Gradle-Multi+modules

benefit: 

- loose coupling -> reusable code for another project
- separation of concern -> high cohesive and readibility
- achieve parallel build & test -> drastically reduce build time
- only need to rebuild & test module that changed instead of the whole project -> reduce waste time during development
- keep dependecies in check, only expose dependencies to module that actually uses them -> reduce waste time
- effective for team members to collaborate


!!Code that you do not have to change is less likely to break than code that you do change. So splitting up the concerns helps you to avoid breakage in unrelated features

What
 - Splitting code into module
Why
 - Clear isolation between modules -> increase reusability and readability while keep complexity maintainable
Who
When
Where
How