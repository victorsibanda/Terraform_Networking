# Load Balancer

## What is a load balancer?
 A load balancing refers to efficiently distributing incoming network traffic across a group of backend servers, aka a server farm or server pool.

 Modern high-traffic websites must serve millions of requests from users or clients and return the correct application in the form of pictures, video or data. This all has to happen fast and in a reliable manner. To scale these high volumes of traffic in a cost effective manner, requires adding more servers.

### Load Balancer

A load balancer acts as the "traffic cop" sitting in front servers and routing client requests across all servers capable of fulfilling those requests in a manner that maximises speed and capacity utilisation and ensures that no one server is overworked which degrades performance.
If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the group the load balancer begins to send requests to it.

In practice this means that load balancers will move traffic in the right direction (the servers), this way the service does not become deprecated.

What does a load balancer do ?
- Distributes client request or network load across multiple servers.
- Ensures high Availability and reliability by sending requests only to servers that are online .
- Provides the flexibility to add or subtract servers as demand dictates.

![what-is-load-balancing-diagram-NGINX-640x324](https://user-images.githubusercontent.com/60632288/80627055-41d4d600-8a47-11ea-841b-cf052fe1430b.png)

#### Load Balancing Algorithms (Source Nginx)

- **Round Robin** – Requests are distributed across the group of servers sequentially.

- **Least Connections** – A new request is sent to the server with the fewest current connections to clients. The relative computing capacity of each server is factored into determining which one has the least connections.

- **Hash** – Distributes requests based on a key you define, such as the client IP address or
the request URL. NGINX Plus can optionally apply a consistent hash to minimise redistribution
of loads if the set of upstream servers changes.

- **IP Hash** – The IP address of the client is used to determine which server receives the request.

- **Random with Two Choices** – Picks two servers at random and sends the request to the
one that is selected by then applying the Least Connections algorithm

#### Benefits of Load Balancing

- Reduced Downtime
- Scalability
- Flexibility
- Efficiency

### Terraform Load Balancing

```hcl

resource "aws_lb" "example" {
  name               = "example"
  load_balancer_type = "network"

  subnet_mapping {
    subnet_id     = "${aws_subnet.example1.id}"
    allocation_id = "${aws_eip.example1.id}"
  }

  subnet_mapping {
    subnet_id     = "${aws_subnet.example2.id}"
    allocation_id = "${aws_eip.example2.id}"
  }
}
```


## How does immutability and horizontal scaling (scaling out) work together?

#### Immutability
Immutability refers to something that is unchangeable. And immutable infrastructure is infrastructure that cannot be changed. As opposed to mutable infrastructure where you can upgrade and update on existing machines. The challenge that comes with mutable infrastructure is not all upgrades will happen perfectly and will fail, resulting in partial updates which introduce higher risks and complexity.

Hence moving to immutable infrastructure means we never upgrade servers in place, rather when upgrading a new server would be created, and not implementing on existing infrastructure. Once the new upgraded server is working, the traffic is routed to the new server and it is no longer routed to the older sever. The benefits of this is that it would no longer have partial updates. Although you will have to use an external database, which uses horizontal scaling, that way when the first machine is no longer in service we can still use the same data without destroying it.



#### Horizontal Scaling

Scaling is the process of adding or removing capacity from your system. This occurs when the load increases beyond what can be handled by the current infrastructure, hence a larger capacity may be need. Alternatively if the load decreases you can also decrease capacity as it becomes wasted, and you also lose money. Services like AWS offer utility like pricing which means you pay for what you use and prices can increase if you are using more than what you need.

Scaling Horizontally means you can scale out, hence creating new instances or scaling in removing instances. This is different from vertical scaling which meant increasing or decreasing the size of your machines


When using immutable infrastructure, scaling out becomes easier, as you are able to add more identical servers in your infrastructure. Scaling only the parts of your system you require hence why they are able to work together.


## What is High Availability?

Availability is used to describe when a service is available, in addition to to the time required by a system to respond to a request made by the user. High Availability is a quality of a system that assures high level of operational performance for a given time period. e.g facebook loading fast when you navigate their website.

High Availability is important when setting up a system as minimising downtime and service interruptions means that you reduce the number of events of problems occurring with your system.

Redundancy alone cannot guarantee high availability. A mechanism must be in place for detecting failures and taking action when one of the components of your stack becomes unavailable.

Failure detection and recovery for redundant systems can be implemented using a top-to-bottom approach: the layer on top becomes responsible for monitoring the layer immediately beneath it for failures. In our previous example scenario, the load balancer is the top layer. If one of the web servers (bottom layer) becomes unavailable, the load balancer will stop redirecting requests for that specific server.

# Auto Scaling

Autoscaling helps ensure that you have the correct number of EC2 instances available to handle the load for your application.

## - How does it work?

In AWS autoscaling works by creating collections of EC2 instances called Auto Scaling Groups, You can specify the minimum amount of instances in each group and Amazon EC2 Auto Scaling ensures your group never goes below this size. You can also specify the maximum which means it never goes above that size. (Which becomes useful in saving costs). Therefore if there is ever a need to scale out above the desired capacity Amazon automatically scales out for you reducing it when the capacity drops.

![as-basic-diagram](https://user-images.githubusercontent.com/60632288/80633007-fffc5d80-8a4f-11ea-8ca7-b2b4014af365.png)

## Example of Terraform Autoscaling

```hcl
resource "aws_placement_group" "test" {
  name     = "test"
  strategy = "cluster"
}

resource "aws_autoscaling_group" "bar" {
  name                      = "foobar3-terraform-test"
  max_size                  = 5
  min_size                  = 2
  health_check_grace_period = 300
  health_check_type         = "ELB"
  desired_capacity          = 4
  force_delete              = true
  placement_group           = "${aws_placement_group.test.id}"
  launch_configuration      = "${aws_launch_configuration.foobar.name}"
  vpc_zone_identifier       = ["${aws_subnet.example1.id}", "${aws_subnet.example2.id}"]

  initial_lifecycle_hook {
    name                 = "foobar"
    default_result       = "CONTINUE"
    heartbeat_timeout    = 2000
    lifecycle_transition = "autoscaling:EC2_INSTANCE_LAUNCHING"

    notification_metadata = <<EOF
{
  "foo": "bar"
}
EOF

    notification_target_arn = "arn:aws:sqs:us-east-1:444455556666:queue1*"
    role_arn                = "arn:aws:iam::123456789012:role/S3Access"
  }

  tag {
    key                 = "foo"
    value               = "bar"
    propagate_at_launch = true
  }

  timeouts {
    delete = "15m"
  }

  tag {
    key                 = "lorem"
    value               = "ipsum"
    propagate_at_launch = false
  }
}
```




## **Source List**

- https://www.nginx.com/resources/glossary/load-balancing/
- https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure/
- https://www.digitalocean.com/community/tutorials/what-is-high-availability
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html

#### Author
**Victor Sibanda** - *Junior DevOps Engineer* - [victorsibanda](https://github.com/victorsibanda)
