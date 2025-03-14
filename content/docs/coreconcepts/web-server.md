+++
title = "Web Servers"
weight = 1
+++

Web servers are the backbone of the internet ! But let's start with an analogy :

## Restaurant analogy

Say you want to eat at a restaurant. You sit at a table (indicated by your favorite search engine), and the waiter (the server) comes to give you the menu (the frontpage). You can then order your food (click on a link) and the waiter will bring it to you (the server sends the requested page to your browser).

Now, what is the restaurant in this analogy ? Well it's the actual machine (or container) where everything is running. Now the chef is basically your computer's CPU but they work multiple shifts at the same time to serve multiple customers in multiple restaurants at the same time. (All of this is not Real-Time of course but that's the main idea).

## Prerequisites

You do not need prior knowledge here, this is the starting point of this guide !

## Why do you need a web server ?

Now that we get the gist of what a web server is, let's go a bit more in depth. A web server is a *software* that serves *web pages* to *users* upon request. The requests are made using protocols like **HTTP** or **HTTPS** and the server responds with the requested page or data that can be displayed in the browser.

A web server is a **crucial part** of a home-lab because you will access most of your services through a web interface. On a security level it is also the first thing (and in theory, *only* thing (aside from a VPN)) that you might want to expose to the internet.

## Okay, cool I want a web server, how do I get one ?

There are many web servers out there, you might have already heard of some of them (especially on error pages ⚠️). Here are some of the most popular ones :
  - Apache
  - Nginx
  - Caddy
  - Traefik
  - Many more...

Now all of these are not necessarily referred to as web servers per se but as reverse proxies. We will get into that in a [later section](/docs/coreconcepts/reverse-proxies) but for now, let's just say they act as an hotel receptionist, they take your request and send them to the right room (service).

## But is it safe ?

Well it depends ! Most of the time, the server itself is safe but not necessarily the services running behind it. Some services might have vulnerabilities that could in turn compromise the whole home-lab. That's why it is important to keep everything up to date and to follow best practices when it comes to security.

## What's next ?

Now that you know what a web server is, we first need to understand [basic Internet](/docs/coreconcepts/internet) concepts.
