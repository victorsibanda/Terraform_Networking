# DNS Route 53

## - What is DNS?

The Domain Name System (DNS) is the phonebook of the internet. Humans access information online through domain names, like nytimes.com or espn.com. Web browsers interact through IP addresses. DNS translates domains names to IP addresses so browsers can load internet resources.

Each device connected to the internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorise IPv4 or IPv6 addresses.

## - How Does DNS work?

The process of DNS resolution involves converting a hostname into a computer friendly IP address. An IP address is given to each device on the internet, and that address is necessary to fine the right device.

When a user loads a webpage a translation must occur between what the user types into their browser and the machine friendly address to locate example.com

#### There are 4 DNS servers involved in loading a webpage.

* **DNS recursor** - The recursor can be thought of as a librarian who is asked to go find a particular book somewhere in a library. The DNS recursor is a server designed to receive queries from client machines through applications such as web browsers. Typically the recursor is then responsible for making additional requests in order to satisfy the client’s DNS query.

* **Root nameserver** - The root server is the first step in translating (resolving) human readable host names into IP addresses. It can be thought of like an index in a library that points to different racks of books - typically it serves as a reference to other more specific locations.

* **TLD nameserver** - The top level domain server (TLD) can be thought of as a specific rack of books in a library. This name-server is the next step in the search for a specific IP address, and it hosts the last portion of a hostname (In example.com, the TLD server is “com”).

* **Authoritative nameserver** - This final name-server can be thought of as a dictionary on a rack of books, in which a specific name can be translated into its definition. The authoritative name-server is the last stop in the name-server query. If the authoritative name server has access to the requested record, it will return the IP address for the requested hostname back to the DNS Recursor (the librarian) that made the initial request.



## Amazon Route 53 DNS
- **A Reliable and cost-effective way to route to end users to internet applications.**

Amazon Route 53 is a highly available and scalable cloud DNS web service. It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to internet applications by translating names like www.example.com into numeric IP addresses. Amazon Route 53 is fully compliant with IPv6.

Amazon Route 53 effectively connects user requests to infrastructure running in AWS - such as EC2 instances or  Elastic Load Balancing load balancers.  You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its end points.

Amazon Route 53 traffic flow makes it easy to manage traffic globally based on different routing types. Using Amazon Route 53 Traffic Flow's visual editor, allows you to manage how your end users are routed to your app. In addition you can register your Domain name and purchase them from Amazon Route 53.


# **sources**
- https://www.cloudflare.com/learning/dns/what-is-dns/
