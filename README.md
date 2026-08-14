# AWS-Auto-Scaling-Groups
## Architechture

<img width="912" height="530" alt="image" src="https://github.com/user-attachments/assets/c557f5c2-fa3e-4f66-974d-81f1bfb62eb7" />


The architecture includes AWS VPC which spans across multiple availability zones(implicit)
- VPC contains an application load balancer to distribute traffic evenly across instances.
- Public subnet contains internet- facing resources
- Internet- facing traffic enters through the internet gateway and is distributed
  by the LB to reach the intended resources.
- EC2 instances scale up as more load memory and CPU power is used
- EC2 instances scale down as less memory and CPU is utilised.


## AWS Services

- Amazon VPC
- Availability Zone (implicit)
- Public Subnets
- Internet Gateway
- EC2
- Application Load Balancer
- Launch Templates
- Auto Scaling Groups
- Target Group

## How it Works

- when a user wants to access a resource, a request is first sent to the internet gateway.

- The internet directs the request to the application load balancer determines which instance to direct the inbound request to, based on the load on each instance.

- If the volume of requests is high, based on the configurations (max CPU/memory utilisation) auto scaling will trigger the creation of more instances, while
  considering other setting like min, max, desired instances.


