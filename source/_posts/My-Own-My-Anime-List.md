---
title: >-
	My Own MyAnimeList
date: 2019-08-17 12:03:20
tags:
---
Summer in Japan is hot, way too hot it makes me stay at home the whole day with the air condition on. But staying at home the whole day without anything to do is kind of suck too, all the things that i'm working on has reached stalemate at this moment. My CV for the next job is currently being reviewed by my friend, the Book project i've been working on just isn't going anywhere and current work just bores me out. I crave to try something new, something different, something that i make myself, that has meaning to it. Thinking of that reminds me of an idea i had along time ago, making an app where i can watch animes that i added into watch list in MAL. Yeah, something like that would be cool. So let's get on to it.

<!-- more -->

### Data crawling

To build this app, first of all i need to collect my personal list from MAL. After a quick look up, apparently MAL at this moment doesn't have public api where i can query my data. (They are planning to release one half a year from now on, so by the time you read this, go check it out to see if it's available yet) So crawling the site is necessary, luckily the site itself is not a SPA, so a python script would work just fine. The idea is to write a function to crawl my data from MAL, deploy it to a serverless function and schedule it to run everyday.

I'm already familiar with AWS Lambda, using it again would be boring. Let's check out what Google Cloud has to offer.

Google Cloud Function turned out to be quite similar to AWS Lambda Function, so setting one up wasn't too hard. So was getting the necessary data. 

```python
def execute(event, context):
    page = requests.get(f'https://myanimelist.net/animelist/{user_name}?status=7')
    tree = html.fromstring(page.text)
    html_element = tree.xpath(".//table[@class='list-table']")
    data = json.loads(html_element[0].attrib['data-items'])
```

Alright, next challenge is to find a database to store above data. My goal is to make this app run as long as possible, so priority is to find the cheapest database service possible. Since they offer free tier up to 1GB storage (which is more than enough for my personal usage), Google Cloud Datastore fits right into the criteria.

Added a few tweaks to above python script and it's done !

{% asset_img mal_data.png %}

### Back end

The next step is building a backend api, same as the crawler service, will be built on top of Google Cloud Function. This time i went with Node, so Express is the framework of choice. I've never built a node app from scratch, so i spent a bit of time studying tutorials of how to make a minimum express server. Fortunenately, [this](http://expressjs.com/en/guide/routing.html) and [this](https://github.com/babel/example-node-server) helped out alot with the initial setup.

```json
{
  "name": "mal-api",
  "version": "1.0.0",
  "description": "Backend API for My Anime List web app",
  "main": "app.js",
  "scripts": {
    "build": "babel src -d dist",
    "start": "npm run build && nodemon dist/app.js",
    "serve": "node dist/app.js"
  },
  "repository": {
    "type": "git",
    "url": "git@me.github.com:WhiteWingedSoul/mal-api.git"
  },
  "author": "The lone dev",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "@babel/cli": "^7.5.5",
    "@babel/core": "^7.5.5",
    "@babel/preset-env": "^7.5.5",
    "nodemon": "^1.19.1"
  }
}
```

