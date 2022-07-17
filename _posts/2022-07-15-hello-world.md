---
layout: post
title: "Hello Jekyll!"
tags: ["Hello World", "Docker", "jekyll", "nginxproxymanager"]
category: "Docker"
date: 2020-07-16 01:25:00 +0200
---

## Hello World

We're up and running, I hope...

<!--more-->

This magnificent page is published using [Jekyll Docker](https://github.com/envygeeks/jekyll-docker/blob/master/README.md) with the beautiful [Chirpy Theme](https://chirpy.cotes.page/)!

Using the [Chirpy Starter](https://github.com/cotes2020/chirpy-starter/generate), I made a fork that I pulled locally to `~/www/jekyll/jekyll-blog`{: .filepath}, removed unneeded files for selfhosting, and changed `_config.yml`{: .filepath} to my needs.

### Building

For building, I went with [Jekyll Docker](https://github.com/envygeeks/jekyll-docker/blob/master/README.md) as I already have lots of stuff running with docker already.

As my goal is to push changes to Github before deploying, I came up with the following `docker-compose.yml`{: .filepath} that pulls the changes from Github, before building the site.

```yml
version: "3.9"
services:
  jekyll-blog:
    image: jekyll/jekyll
    container_name: jekyll-blog
    volumes:
      - ~/www/jekyll/jekyll-blog:/srv/jekyll:Z
    environment:
      - JEKYLL_ENV=production
    command: >
      sh -c "git config --global --add safe.directory /srv/jekyll &&
             git pull &&
             jekyll build" 
```
{: file="docker-compose.yml" }

### Hosting

![](/assets/images/2022-07-15-hello-world//2022-07-17-20-34-00.png){: style="max-width: 250px" .right}
As for hosting the site it self, I already have [nginx-proxy-manager](https://nginxproxymanager.com/) running, it can access my `www-folder` though bind mounts.

Added a new host with my new subdomain, and set the appropriate configuration under the SSL tab.

Adding the following in its `Advanced` -> `Custom Nginx Configuration` lets you serve static content.
 
No need to spin up another container for serving a static webpage.

```
location / {
  root /www/jekyll/jekyll-blog/_site;
}
```

### Updating the blog on-the-go

I currently use [WorkingCopy](https://workingcopyapp.com/) for other projects and it got a built-in markdown editor with previews. It's excellent for pushing/pulling changes to Github, but I'm not certain it's the best markdown editor. Got some suggestions? Drop a comment.

For building, it's as easy as pointing [Shelly - SSH Client](https://apps.apple.com/us/app/shelly-ssh-client/id989642999) to my server, adding a key-file, and adding `docker start jekyll-blog` to `Command`. It will then log in, start the container, then exit.
