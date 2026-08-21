# What is AWS CloudFront?
Amazon CloudFront is a managed AWS service that provides a Content Delivery Network (CDN).
A CDN helps deliver content such as:

Images
Videos
Web pages
Static files
Application content

to users faster by serving the content from locations closer to the user.
Where Do We Use CDNs?
The main purpose is to provide content with low latency and a better user experience.

How Does a CDN Solve This Problem?

A CDN creates or caches copies of content at locations closer to users.
### What Is an Edge Location?

An Edge Location is a location used by the CDN to deliver cached content closer to users.
When a user requests content, CloudFront can deliver it from a nearby edge location instead of requiring every request to travel back to the origin.
Edge Location

An Edge Location is where CloudFront delivers cached content closer to users.

The main purpose of AWS CloudFront is:

To deliver content to users with lower latency and better performance by using a global network of edge locations and caching content closer to users.

The simplest way to remember it

CloudFront = Makes content delivery faster globally

ALB = Distributes application traffic across servers

EC2/ECS/EKS = Runs your application
