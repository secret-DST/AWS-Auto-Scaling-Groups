# AWS-Auto-Scaling-Groups
## Architechture

<img width="912" height="530" alt="image" src="https://github.com/user-attachments/assets/c557f5c2-fa3e-4f66-974d-81f1bfb62eb7" />


# AWS Application Load Balancer and Auto Scaling Architecture

## Architecture Overview

The architecture uses an Amazon VPC with resources distributed across multiple Availability Zones to improve availability and scalability.

* The VPC provides the isolated network environment for the application.
* An internet-facing Application Load Balancer (ALB) receives incoming HTTP/HTTPS traffic from users.
* The ALB is deployed across multiple public subnets in different Availability Zones for high availability.
* The ALB forwards requests to healthy EC2 instances registered with its target group.
* The EC2 instances are managed by an Auto Scaling Group (ASG).
* Launch Templates define the configuration used when new EC2 instances are launched.
* The Auto Scaling Group maintains the configured minimum, maximum, and desired number of instances.
* Scaling policies can increase or decrease the number of EC2 instances based on configured CloudWatch metrics, such as CPU utilization.

## AWS Services

* Amazon VPC
* Availability Zones(implicit)
* Public Subnets(1 in diagram for ease)
* Internet Gateway
* Application Load Balancer
* Target Group
* Amazon EC2
* Launch Templates
* Auto Scaling Groups
* Amazon CloudWatch

## How It Works

1. A user sends a request to the application's public endpoint.

2. The request enters the AWS VPC through the Internet Gateway. The route table associated with the public subnet provides the route between the subnet and the Internet Gateway.

3. The internet-facing Application Load Balancer receives the request.

4. The ALB checks the health of the registered targets and forwards the request to an appropriate healthy EC2 instance in the target group.

5. The EC2 instances are managed by an Auto Scaling Group. The ASG maintains the desired capacity and can launch or terminate instances based on the configured scaling policies.

6. If application demand increases, the Auto Scaling Group can launch additional EC2 instances, up to the configured maximum capacity.

7. If demand decreases, the Auto Scaling Group can terminate unnecessary instances, while maintaining at least the configured minimum capacity.

8. New instances are created using the configuration defined in the Launch Template and are automatically registered with the target group.

## Scalability and High Availability

The architecture is designed to provide:

* **High availability** by distributing resources across multiple Availability Zones.
* **Load balancing** through the Application Load Balancer.
* **Automatic scaling** through the Auto Scaling Group.
* **Health-based routing** by allowing the ALB to send traffic only to healthy targets.
* **Consistent instance configuration** through the Launch Template.
* **Monitoring and scaling decisions** through Amazon CloudWatch metrics.

## Traffic Flow

```text
User
  |
  v
Internet
  |
  v
Internet Gateway
  |
  v
Application Load Balancer
  |
  v
Target Group
  |
  +-------------------+
  |                   |
  v                   v
EC2 - AZ A         EC2 - AZ B
  |                   |
  +---------+---------+
            |
            v
     Auto Scaling Group
```



