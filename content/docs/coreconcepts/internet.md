+++
title="Internet"
+++

This page will cover the basics of exposing your services to the internet. If you are here, you probably know what the internet is but let's go over some basic concepts.

## IP Addresses

A machine on the internet is identified by an IP address. This is an identifier that allows other machines to communicate with it. There are two types of IP addresses:
- **IPv4**: The most common. It is a 32-bit number represented in the form of 4 octets separated by dots (e.g. 192.168.1.1).
- **IPv6**: A newer version of the IP protocol. It is a 128-bit number represented in the form of 8 groups of 4 hexadecimal digits separated by colons (e.g. 2001:0db8:85a3:0000:0000:8a2e:0370:7334).

It is a bit like an address for your computer. However IP addresses are hard to remember, so we use domain names instead.
You might also have noticed that there are only a limited number of IPv4 addresses available and today, ISPs are starting to mutualize them because they are running out of them. IPv6 was created to solve this issue, by trying to put the number of IPv6 addresses on the surface of the earth, there would be 6.67 * 10^23 addresses per square meter.

Usually, if you are a home user, you will have one IP address that points to your router. This is called a public IP address. Your router will then assign private IP addresses to the devices on your network. These private IP addresses are not accessible from the internet. More on the LAN part in the [Networking](/docs/coreconcepts/networking) section.

## Domain Names

Ever told your friends that you love watching videos on 65.21.155.186 (peertube.tv) ? No ? Am I the only one ? Well, that's because domain names are easier to remember than IP addresses. They are human-readable names that map to an IP address.
