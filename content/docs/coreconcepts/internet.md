+++
title="Internet"
+++

This page will cover the basics of exposing your services to the internet. If you are here, you probably know what the internet is but let's go over some basic concepts.

## IP Addresses

A machine on the internet is identified by an **IP address**. This is an identifier that allows other machines to communicate with it. There are two types of IP addresses:
- **IPv4**: The most common. It is a 32-bit number represented in the form of 4 octets separated by dots (e.g. 192.168.1.1).
- **IPv6**: A newer version of the IP protocol. It is a 128-bit number represented in the form of 8 groups of 4 hexadecimal digits separated by colons (e.g. 2001:0db8:85a3:0000:0000:8a2e:0370:7334).

It is a bit like an *address for your computer*.

Usually, if you are a home user, you will have one IP address that points to your router. This is called a public IP address. Your router will then assign private IP addresses to the devices on your network. These private IP addresses are not directly accessible from the internet. More on the LAN part in the [Networking](/docs/coreconcepts/networking) section.

*Culture Note* : Some companies or universities have a range of public IP addresses. Sometimes so many that they can even assign one to each device on their network.

You might also have noticed that there are only a limited number of IPv4 addresses available and today, ISPs are *mutualizing* them because they are running out of IPs. IPv6 was created to solve this issue, by trying to put the number of IPv6 addresses on the surface of the earth, there would be 6.67 * 10^23 addresses per square meter. That's about enough, right ?

## Ports

Okay so now you know where the router lives with its public IP address. But how do you access a server ? What if you have multiple websites ?? What if you want **waffles** for dinner ???! Well, that's where ports come in. Ports are doors ! It's the appartement number in the building. It allows you to access different services on the same machine. Some ports are used by protocols like SSH (22), HTTP (80), HTTPS (443), etc. You can also use custom ports for your services. For example, you could run a web server on port 8080.

Ports can be listened to by a service, only one at a time (how can your drive and video hosting service live in the same flat ?)

So as a recap :
- **Public IP address**: The address of your router on the internet. Street name !
- **Private IP address**: The address of your device on your local network. Street number !
- **Port**: The door number !

*Note* : by default, when you access a website, you don't specify the port number in the URL. This is because the browser uses the default port for the protocol (80 for HTTP, 443 for HTTPS).

## Domain Names

Ever told your friends that you love watching videos on 65.21.155.186:443 (peertube.tv) ? No ? Am I the only one ? Well, that's because domain names are easier to remember than IP addresses. They are human-readable names that map to an IP address. minecraft.hiseho.net (don't bother, it doesn't exist) is easier to remember than 8.8.8.8:25565 right ?

But how do you know who is who ? Well, that's where DNS comes in. It's a phone book of the internet ! It maps domain names to IP addresses. When you type a domain name in your browser, it will ask a DNS server for the IP address of the domain name. The DNS server will then respond with the IP address and your browser will connect to the server.

## Foreshadowing

Now, you might have noticed that you access some services without ever specifying a port number. How does this witchcraft work ? How can you have multiple services on the same machine, accessed through the same port despite that a port can only be listened to by one service at a time ? Well, that's where reverse proxies come in. You can read more about them in the [Reverse Proxies](/docs/coreconcepts/reverse-proxy) section.


