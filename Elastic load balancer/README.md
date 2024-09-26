## ELASTIC LOAD BALANCER


Creating load balancer on Aws depends on the type of load balancer you want to create. Whenever you want to build a cluster of services, let's say multiple webservers, you need a single endpoint to access them and thats mostly provided through a load balancer.

### LOAD BALANCER PORTS

__FRONTEND PORT__: Listens from the user requests on this port AKA listeners (like you access Google.com on port 443 generally https default port 443). So if you're hosting a web service for https connection you will be given frontend port 443 to your load balancer. e.g 80, 443, 25 etc


__BACKEND PORT__: Services running on OS listening on this port. They are based on the services port number that is running on the backend servers. eg 80, 443, 8080 etc. so if you are running tomcat server, which is running on port 8080, then the load balancer backend port will be 8080.


Aws ELB is goin to receive the traffic and distributed on the backend on multiple targets. These targets mostly will be ec2 instances, but you can have containers and have other IP addresses which are distributed in multiple availability zones, so you can have a cluster that is in multi zones and the load balancer will be an endpoint for that.


AWS offers 3 types of ELB

__Application load balancer__(ALB): Best suited for only web traffic , App, http and https protocol. 

__Network load balancer__(NLB): Handles TCP and UDP traffic, designed for ultra-high performance and low latency. Its  a high performing load balancer and also expensive and handles millions of request.

__Classic load balancer__(CLB): Supports both HTTP/HTTPS and TCP protocol and is suitable for basic load balancing needs (legacy option) which is everyone's favorite, the simplest one.




## AWS CLOUD 


Lift and shift application workload

Some of the AWS services we will be using for the project

- EC2 instances: VM for tomcat, RabbitMQ, memcache, MYSQL

- ELB(load balancer): Nginx LB replacement

- Autscaling: Automation for Vm scaling (which will automatically scale out and scale in our ec2 instance)

- S3/EFS storage: for shared storage

- Route 53: for private DNS service



__FLOW OF EXECUTION__

- Login to AWS Account

- Create key pairs

- Create security groups for load balancer, Tomcat and backend services

- Launch instances with user data (which will be our bash script)

- Update IP to name mapping in Route 53

- Build application from source code

- Upload artifacts to S3 bucket

- From S3 bucket download artifacts to Tomcat EC2 instances

- Set up ELB with HTTPS (from Amazon certifacte manager) (using fot HTTPS connection on LB)

- Map ELB endpoint to website name in Namecheap DNS

- Then verify 

- Build an autoscaling group for Tomcat instance


__Additional Tips:__

- Make sure you have the necessary IAM permissions to perform these actions.

- Regularly monitor your resources and optimize your configurations based on usage.

- Keep your security groups as restrictive as possible to minimize exposure.









































































































































































































