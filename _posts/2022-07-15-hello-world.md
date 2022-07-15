---
layout: post
title: "Welcome to Jekyll!"
tag: "Hello World"
category: "Docker"
---

# Hello World

We're up and running, I hope...

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
    ports:
      - 4000:4000
    networks:
      - web
    command: ["jekyll", "serve", "--watch", "--drafts"]

networks:
  traefik:
    external: true
```
