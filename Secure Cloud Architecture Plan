# Secure Cloud Architecture Plan

Users -> CDN -> Load Balancer -> Application Servers -> Private Database

## CDN
The CDN stores cached copies of static content closer to users to improve loading speed.

## Load Balancer
The load balancer distributes incoming requests across multiple application servers to maintain performance and reliability.

## Application Servers
Application servers process requests from users. These servers should be placed in a private subnet to prevent direct access from the public internet.

## Database
The database stores student records. The database should remain private and should not be directly accessible from the Internet, accepting connections only from the internal application servers.
