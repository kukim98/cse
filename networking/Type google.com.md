# What happens when google.com
## Typing
When the letters of `google.com` are typed into the URL address bar, few things can happen depending on the browser.
1. The browser may look at the list of previously visited websites and may start displaying autocompleted webpages that start with those letters.
2. The browser may send a search request to a search engine and return a list of search words that start with those letters. By default, Chrome does this with Google's search engine, and Microsoft Edge does this with Bing's search engine.

## URL Parsing
When `google.com` is typed and the user presses *Enter*, the browser checks to see if the typed-in string is a URL or not. If it is not a URL, it assumes that it is a search term, and it sends a search query using the default search engine. If it is a URL, a top-level navigation will be performed to the URL.

## Protocol
Since `google.com` is a URL, it will check for the protocol being used. **With HTTP, the port used will be 80, and with HTTPS, the port used will be 443.** Because the typed-in string was `google.com`, the protocol was not specified. Older versions of browsers used HTTP as the default protocol. now most browsers will default to HTTPS when the protocol is omitted. In addition, servers can respond with the **HTTP Strict-Transport-Security (HSTS)** response header. This lets the browsers know that the website should only be accessed using HTTPS, not HTTP.

## DNS Lookup
Now that we know we should use HTTPS (443), we need to know the IP address of `google.com`. The browser will first check the local DNS cache. If it is there, then it will use that IP address. If not, then it checks the "hosts" file which contains host names and IP addresses mapping. If not, **DNS query** is performed. DNS uses UDP with port 53, and it is unencrypted. Thus, anyone can sniff DNS queries and will know which domains certain clients are trying to access. **DNS queries CAN BE ENCRYPTED using DoH (DNS over HTTPS).** If DoH is enabled, the DNS queries will occur over TLS, and no one will be able to see the data. By default, most browsers disable DoH. Assuming DoH is disabled, a UDP datagram is sent over to port 53 to the default DNS provider, which is known by the router, which is provided by the ISP. **The browser will now send a DNS query to the primary DNS server via the router; this will go through the OSI model and ARP.** The DNS query is returned with the IP address of `google.com` that the browser can use to make a TCP connection with the server.

## TCP Connection
