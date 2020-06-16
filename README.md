#HA Architecture design
Implemented a highly available and resilient architecture design of a word press site using the below components:
1. MySQL Server RDS as the DB for the wordpress site.
2. EC2 instances to serve as a Writer Node and multiple Reader Nodes(with appropriate Security Groups, roles and VPC)
3. Route53 to distribute the read and write request, so that only the admins can do write request and all the read request will be directed to a naked domain address that will be backed with an Elastic Application Load Balancer.
4. Internet facing Application Load Balancer to maintain the traffic flow among the Reader Nodes target group with health check of individual instances (Each Reader node in different AZ)
5. Auto-scaling group to add Resilient feature to the architecture, so that in case of any Reader node failure, it automatically scale out the new instances of Reader nodes and continue in serving the read requests without any downtime and interruption.
6. Used S3 bucket to store the backup of the site code and site content, so that auto-scaling group can easily pull up the code while scaling out.
7. CloudFront is used to allow site content to be cached at the edge location and it will not hit the site for the resources and ultimately provide low latency over the network.
