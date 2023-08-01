# DNS (Domain Name Server)
## Introduction
DNS is used to return the IP address of the destination machine given the URL address. To ensure that the DNS can server billions of requests, there are multiple DNS servers all around the world. Web URLs are composed of a **top-level domain**, **host name**, and **subdomains**.  The top-level domains are like *.com*, *.edu*, and *.gov*.  Host names are the ones that come right before the top-level domain such as *google*, *osu*, and *state*. Subdomains are the ones that come before the host name; this can be *mail*, *docs*, and etc.

## Flow
When the client wants to get the IP address of a URL (**canonical name**), it performs a **NS lookup** which is handled by the **resolver**. The resolver contacts one of the root servers with the URL. The **root server** returns a list of IP addresses that the resolver can contact based on the URL's top-level domain. For instance, with `google.com`, the root server will return the IP address of a **top-level domain server** that may know the IP address. The resolver will then contact the top-level domain server, and it will respond back with the **authoritative name server** that may know the IP address; these may be hosted by the companies themselves or third-party companies like GoDaddy and etc. The resolver will now return a series of IP addresses that are aliases of the canonical name that the client can use to contact the destination machine. DNS queries are **recursive** and **stateless**. The resolver may cache the query results; each result has **TTL (Time To Live)** which tells for how long the results should be cached. Once expired, new queries will be made to update the cache.

## UDP and DNS Poisoning
DNS runs over **UDP**.  To match the appropriate queries to each other, query IDs are attached to DNS queries. This method opens up the possibility of **DNS poisoning**. Hackers send UDP packets with randomly generated query IDs and the fake IP address. If one of the queries successfully match with one of the DNS queries, the client will access the wrong website.

## Availability
Most DNS issues occur due to outages in the authoritative name servers. When these servers are down, clients cannot get the IP address to access the website. 

## Chrome
When clients typed the canonical name of an URL, Chrome sent out DNS queries to get the IP address of whatever the clients have typed. It will first check the local network to see if the typed string matches any of the endpoints registered. Then, it will send a DNS query to the root server to get the IP address. However, this was overloading the root servers since everyone was sending DNS queries. In addition, Chrome wanted to detect any internal rerouting done by the ISPs or the network managers that intercept and capture traffic from mistyped domain names. So for instance, when a user types `marketing` Chrome wanted to know whether to display `Search marketing` or `https://marketing`.  To do so, Chrome will send out random string DNS queries and will see if it resolves to an IP address at the start. If they do, then the IP address is cached and used to display the appropriate user suggestion. This resulted in DNS overloading, and the feature has been removed after 10 years.