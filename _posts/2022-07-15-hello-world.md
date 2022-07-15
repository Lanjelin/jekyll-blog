---
layout: post
title: "Hello Jekyll!"
tags: ["Hello World", "Docker"]
category: "Docker"
date: 2020-07-15 23:55:00 +0200
---

## Hello World

We're up and running, I hope...

<!--more-->

This magnificent page is published using [Jekyll Docker](https://github.com/envygeeks/jekyll-docker/blob/master/README.md) with the beautiful [Chirpy Theme](https://chirpy.cotes.page/)!

The compose-file is pretty much copy-pasta from the [Jekyll Github](https://github.com/envygeeks/jekyll-docker/blob/master/README.md)

```yml
version: "3.9"
services:
  jekyll:
    image: jekyll/jekyll
    container_name: jekyll
    volumes:
      - ~/www/jekyll/jekyll-blog:/srv/jekyll:Z
    #ports:
    #  - 4000:4000
    networks:
      - web
    command: ["jekyll", "serve", "--watch"]

networks:
  web:
    external: true
```
{: file="docker-compose.yml" }

_Running everything though nginx-proxy-manager, I usually skip the port declaration, as all my containers exposed to the internet is on the same network as nginx-proxy-manager, and it accesses them directly._

_More on nginx-proxy-manager will hopefully come later_
