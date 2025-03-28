+++
title="Networking"
weight=15
+++

So far, we have been talking about the internet and its [IPV4](/docs/coreconcepts/internet#ip-addresses). However, you might have noticed that all your machines are not necessarily exposed to the internet. In fact, we saw that the only one that is exposed is basically your router. This is because your router is the only one with a public IP address. All the other machines on your local network have private IP addresses. Now you might wonder how your devices can communicate with the internet right ? Let's take a look at how this works.

## Local Area Network (LAN)

You have your own network ! Believe it or not but some of these super rare IP addresses are only for you ! There are some **private ranges**. These IP addresses are not public IP addresses and these sub-networks ranges are reserved for private networks. This means that you can have the same IP address as someone else, as long as you are not on the same network.

The private ranges are:
 - 10.0.0.0/8
 - 172.16.0.0/12
 - 192.168.0.0/16

### Netmask

Notice those / that I keep adding ? They represent the network mask. Basically It means that the first x bits of the IP are the ones that shouldn't change to stay in the range. So if you followed, you know that 192.167.255.255 is **NOT** a private IP, same thing goes for 192.169.0.0 . Here only a few bit changes but if you look at the second octet : 167 = 10100111 in binary and 169 = 10101001 whereas 168=10101000. So you see here that we would change the first 16 bits.

Another simpler way to see it is that you can basically discard the 32-x last bits to know the range you can use.
We are going to take advantage of this IP range for our server later on.

## IP Allocation

When you connect to a network, your router assigns your device an IP address using a protocol called **DHCP (Dynamic Host Configuration Protocol)**. This protocol ensures that each device on the network receives a unique IP address, preventing conflicts. The router maintains a record of assigned IP addresses to avoid duplication.

In cases where your device cannot obtain an IP address from the router, it will automatically assign itself an address in the range which starts with `169.254.0.0/16`.
You can also either freeze an IP address in your router admin panel or set a static IP address on your device. This is useful for servers that need to maintain a consistent IP address so we know where to point services to.

## Security

A good practice is to make it so certain critical services are only accessible from the local network. This way, you can access these using a VPN (Virtual Private Network) which adds an extra layer of security.

### ❗Warning❗

Security by obscurity is equivalent to no security at all. If you keep critical services exposed to the internet under a domain, people can find them using logs. There are lists of all the certificates issued by a CA (Certificate Authority). There are people out there that try to poke holes in services just for fun and to see if they can turn your machine into a botnet. So be careful and don't expose services that you don't want to be exposed to the internet.
