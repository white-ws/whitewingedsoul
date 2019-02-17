---
title: >-
	How this site was made
date: 2018-11-10 10:55:00
tags: 
- blogging
- hexo
- next
---

#### Foreword

I've made this blog quite for quite sometime, following the trend of blogging about tech, daily life style in Japan between my uni friends. Yet, i've never actually contributed anything to this blog, or anywhere else. Part of me think it was due to the inability to express myself to others, as well as inexperience in any area of knowledge. But deep down inside i know it's just an excuse for my laziness, and the ignorance of it was the same as letting go of a oppurtunity for improving myself. 

So no longer, from today onward, i'll force myself to write, no matter how shallowed and foolish the content it maybe, no matter how crappy my English may sound like, i'll write, and improve upon.

Thus, begin the first post on this blog. How this site was made.


<!-- more -->

# Installing Hexo

First, i checked the list of prerequisite preparation

- a Mac or Linux Operating System, with an Unix shell
- node.js
- Git

After that, installed hexo comand line interface

```
npm install -g hexo-cli
```

Created blog project folder

```
$ hexo init thelondev
$ cd thelonedev
$ npm install
```

After the installation was finished, deployed the hexo blog with

```
hexo server
```

Woala!

{% asset_img default_hexo_blog.png Default Hexo Blog Site %}

After this step, it's possible to start writing.

##### But wait, that was all of it

Having a default blog is nice and all, but it would be boring and would't define what thelonedev is. 
So it was time for customization.

There are 2 approach to this. One can do it from scratch, customizing html, css, js and make their own ideal blog site.
The other is to use an already existed custom theme. I'm more of a lazy one, so i fell to this category, and NexT was my choice.

# Installing NexT theme

Installation took place in project folder

```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

After i pulled next repo into my blog project folder, i changed the `_config.yml` file to switch to NexT theme.

*Note: There are many other customization that can be made by changing `_config.yml` file such as site description, writting style, index, date&time format ..... although those won't be covered in this blog post, it's easy enough that i believe you can do it on your own and customize your site further more*

{% asset_img next_config.png Change default theme to NexT %}

After applied change to `_config.yml` file, i had to reboot hexo server in order for change to take place.

And it turned out quite nice.

{% asset_img next-theme-blog.png NexT theme Hexo Blog %}

There are 4 different schemes that can be used in NexT theme: Muse, Mist, Pisces and Gemini.      
My choice was Mist.

Changed the scheme option in `themes/next/_config.yml` by uncommenting Mist line

```
# Schemes
# scheme: Muse
scheme: Mist
# scheme: Pisces
# scheme: Gemini
```

{% asset_img hexo-mist-scheme.png NexT theme Hexo Blog %}


That was all what needed to create this blog. Though it would be meaningless if i can only run it locally.
So i had to deploy it to a Github Page.

# Deploy

For all of those who's unawared, Github allows you to host one of your site, on the domain username.github.io . All you need to do is create a new repository named username.github.io, push your site source code there and let Github take care of the rest.
More information regards this [can be found in here](https://pages.github.com/).

Now, back to main topic, hexo provides a deploy method to github. First, install [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)

```
$ npm install hexo-deployer-git --save
```

Change deploy config in `_config.yml`

{% asset_img deploy.png Deploy Config %}

And enter below command

```
hexo deploy
```

Once i finished with above steps, **thelonedev** was available to access at [whitewingedsoul.github.io](https://whitewingedsoul.github.io)

... though as you noticed, clicking on the above link redirected you to [thelonedev.com](https://thelonedev.com). To use a custom domain with github page. You have to follow the below extra steps.

# Custom domain

First thing first, this procedure will cost you money. So if you don't mind using github subdomain for your site, you should stop here and start having fun with your own blog !

But, if you are determined to get your own brand, you have to purchase a domain. There are many domain registrars where you can purchase domain, notably Namecheap, GoDaddy, Google, Onamae... Their price don't differ that much so just choose the one you like.

I chose [Onamae](https://www.onamae.com/) to purchase thelonedev so i don't have to deal with the hassle converting yen to foreign currency. 

{% asset_img purchase-domain.png %}

After i got my thelonedev.com domain ready, i added it to my Github Page setting.
Go to `Your Project Name > Settings > Github Pages > Custom domain` and add the custom domain you've purchased.

{% asset_img custom-domain.png %}

And finally, i went to onamae configuration page to set up my apex domain.

Created A records with following addresses

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

{% asset_img configure-a-records.png %}

You may have to wait for at most 24 hours for DNS changes to take place. 
And that was all it takes to make this website lives at [thelonedev.com](https://thelonedev.com). 

I hope this has been helpful to spark up your writting journey. 




