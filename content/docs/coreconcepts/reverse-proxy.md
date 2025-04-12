+++
title = "Reverse Proxies"
weight = 20
+++

Reverse proxies are a service that takes requests and map them to the right service. Up until now, we have been talking about web servers but you might have noticed that a machine only has a limited number of ports, and you don't access this webpage specifying the port number in the URL. This is where reverse proxies play their magic.

## Prerequisites

To understand reverse proxies, you need to know about the following concepts:
- [Web Servers](/docs/coreconcepts/web-server)
- [Internet](/docs/coreconcepts/internet)
- [Networking](/docs/coreconcepts/networking) is advised but not necessary if you have only one machine.


## What is a reverse proxy ?

A reverse proxy basically is a piece of software that will listen to ports and forward requests to the right service. When you have two subdomains, for instance `cloud.xxx.yy` and `wiki.xxx.yy`, the reverse proxy listens to port 80 and 443 and forwards the requests to the right service depending on the URL used to access the site. This way, you can have multiple services running on the same machine without having to specify the port number in the URL !


### Pranks

A funny thing that one could do if they wanted to prank their friends could be to use a wild card. A wild card (*) matches any string. Typically, putting this in [caddy](https://caddyserver.com/) in the following file :
```
*.xxx.yy {
  redir https://www.youtube.com/watch?v=dQw4w9WgXcQ
}
```

Would redirect ***EVERY*** subdomain to the famous song "Never gonna give you up". I've set this up because I'm a true prankster. Also you could think that bots would be redirected to this page as well but they usually look at the certificates that are issued for your domain (typically `cloud.xxx.yy` but not `*.xxx.yy`). Bots would only try routes that they know exist as certificate logs are public.

## Safety bit

A reverse proxy is a great way to expose your services to the world wide web. It also allows fine-grained access depending on the IP address of the user. For instance, you could set up critical services with a reverse proxy and only allow access to them from your local network. This way, you can access these using a [VPN](https://en.wikipedia.org/wiki/Virtual_private_network) which adds an extra layer of security.


