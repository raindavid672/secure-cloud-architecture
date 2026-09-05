Then answer:
1. What does Security OF the Cloud mean? It refers to the cloud provider's responsibility to protect the underlying infrastructure, including the physical data centers, hardware, and core network facilities.
2. What does Security IN the Cloud mean? It refers to the customer's responsibility to secure everything they put into the cloud, including their data, applications, user access, and resource configurations.
3. Which resource should be directly accessible from the Internet? The Content Delivery Network (CDN) and the Load Balancer.
4. Why should the database remain private? To protect sensitive information from public internet exposure, minimizing the risk of unauthorized access and data breaches.
5. Why should users not connect directly to the database? Bypassing application logic and security controls increases the risk of data theft, corruption, and malicious direct attacks like SQL injection.
6. What is the purpose of a load balancer? To distribute incoming internet traffic evenly across multiple application servers, ensuring high availability and preventing any single server from becoming overwhelmed.
7. What happens if one application server fails? The load balancer detects the failure and automatically redirects incoming user traffic to the remaining healthy application servers, preventing system downtime.
8. What is the purpose of a CDN? To cache and deliver static content from edge locations physically closer to the users, which reduces latency and speeds up website loading times.
9. Why should administrator accounts use MFA? Administrator accounts have full control over the infrastructure, making them prime targets; MFA adds a critical layer of defense if a password is compromised.
10. Why should administrator access not be given to every employee? It violates the principle of least privilege, significantly increasing the risk of accidental system damage, data leaks, or internal threats.
11. Why are logging and monitoring important? They provide continuous visibility into system activity, allowing security teams to quickly detect, investigate, and stop unauthorized access or operational errors.
12. Why are backups important? They ensure that critical data can be quickly recovered after a hardware failure, accidental deletion, or ransomware attack, preventing permanent data loss.

# Secure Cloud Architecture Plan

Users 
-> 
CDN 
-> 
Load Balancer 
-> 
Application Servers 
-> 
Private Database

## CDN
The CDN stores cached copies of static content closer to users to improve loading speed.

## Load Balancer
The load balancer distributes incoming requests across multiple application servers to maintain performance and reliability.

## Application Servers
Application servers process requests from users. These servers should be placed in a private subnet to prevent direct access from the public internet.

## Database
The database stores student records. The database should remain private and should not be directly accessible from the Internet, accepting connections only from the internal application servers.


# Public and Private Resources
Identify whether the following resources should be Public or Private.
Resource Public or Private? Explanation
CDN - Public
Load Balancer - Public
Application Server - Private
Database - Private
# EXPLANATION
CDN - Must be accessible over the internet to distribute cached static content directly to end-users.
Load Balancer - Acts as the internet-facing entry point, receiving public user requests and securely routing them to the internal backend servers.
Application Server - Placed in a private subnet to process application logic; it only accepts internal traffic routed from the load balancer, protecting it from direct internet attacks.
Application Server - Strictly isolated in a private subnet to protect sensitive student records; it only accepts internal connections directly from the application servers.

# Security Controls
IAM
Access to the cloud environment must follow the principle of least privilege, granting administrators control over the infrastructure while restricting developers to only updating the application code. End users have absolutely no access to the underlying cloud resources and can only interact with the public-facing website.
MFA
Multi-Factor Authentication (MFA) must be strictly enforced for all human users, especially cloud administrators and developers who have the power to modify the infrastructure or access sensitive data. Meanwhile, automated service accounts do not use MFA and instead rely on secure API keys or internal roles for authentication.
Firewall / Security Group
The load balancer's security group should allow public inbound internet traffic on standard web ports (HTTP/HTTPS) to ensure users can reach the application. Meanwhile, internal firewalls must strictly limit access so that the application servers only accept traffic from the load balancer, and the private database only accepts connections from the application servers.
Encryption
Student information contains sensitive personal data, such as names and academic records, which must be protected against unauthorized access and cyberattacks. Encrypting this data ensures that even if hackers manage to breach the database or intercept network traffic, the stolen information remains completely unreadable and useless to them.
Logging
Logging should record all authentication attempts, infrastructure modifications, and system errors to quickly detect unauthorized access or security breaches. Additionally, it must track all data access events to maintain a clear audit trail of exactly who viewed or altered sensitive student records.
Monitoring
Monitoring systems should actively watch for unusual login patterns, such as repeated failed attempts or access from unexpected geographic locations, which often indicate unauthorized hacking attempts. Additionally, they must track anomalous network traffic—like sudden spikes in outbound data—and unauthorized privilege changes to quickly detect potential data exfiltration or internal threats.
Backup
The database must have regular backups to prevent the permanent loss of critical student records due to hardware failures, accidental deletions, or ransomware attacks. Having reliable backups ensures that the system can quickly restore lost data and resume normal operations with minimal downtime in the event of a disaster.
Example firewall / security group rules:
Internet → Load Balancer = Allowed
Load Balancer → Application Server = Allowed
Application Server → Database = Allowed
Internet → Database = Blocked

# Principle of Least Privilege
USER 
Administrator 
Instructor
Student
Developer
ALLOWED ACCESS
Administrator - Full access to cloud infrastructure, network configurations, security settings, and user access management.
Instructor - Application-level access to view and update student records and grades only for their specifically assigned courses.
Student - Application-level access to view only their own personal information, enrolled courses, and individual grades.
Developer - Access to application code, deployment pipelines, and testing environments, with no access to the live production database.

# Shared Responsibility Model
RESPONSIBILITY
Physical data center - Cloud Provider
Physical servers - Cloud Provider
User accounts - Customer
Student data - Customer
IAM permissions - Customer
Application security - Customer
Database access rules - Customer
Backups - Customer
