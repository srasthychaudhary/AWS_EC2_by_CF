**AWS EC2 Instance Template by Cloud Formation**

We’ll look at CloudFormation templates to create EC2 instances in their own VPC.

Step-1: PAPAMETERS

Any values that might be customized by the end user are defined as parameters.

The instance type, which defines the hardware associated with our VM.

The IP address of a workstation that can connect to the instance via SSH.

The AMI used to create the VM. AMIs can be found in the AWS Marketplace.

The key pair used to secure the instance.


The next section of the template defines the resources to be created.


Step-2: VPC

We start with a VPC, which is essentially an isolated network segment that holds our resources. This VPC will hold private IP addresses in the 10.0.0.0/16 range.


Step-3: INTERNET GATEWAY

To give our EC2 access to the Internet, we need an Internet gateway.


Step-4: ATTACH INTERNET GATEWAY TO VPC

The Internet gateway is then attached to the VPC.


Step-5: SUBNET

Inside the VPC we can have one or more subnets. While a VPC can span multiple availability zones, a subnet is a network address range in a single AZ. We are creating one EC2 instance, and so we only create one subnet to hold it.


Step-6: ROUTE TABLE

Traffic routing is handled by a route table.


Step-7: ROUTES

We then route any external traffic to the Internet gateway. This will give our EC2 instance Internet access.


Step-8: ASSOCIATION OF ROUTE TABLE TO SUBNET

The route table is then associated with the subnet. 

Any subnet whose traffic is routed through an Internet gateway is known as a public subnet.


Step-9: SECURITY GROUP

Traffic in and out of the EC2 instance is controlled by a security group


Step-10: ELASTIC IP

While our EC2 instance will get a public IP address when it is created, this address will change if the instance is stopped and started again. To ensure the instance always has a static IP address, we create an elastic IP.


Step-11: EC2 INSTANCE 

We have now created all the networking required to host an EC2 instance with Internet access and a static IP. Now we create the EC2 instance.


Step-12: OUTPUT

The outputs capture the instance ID and elastic public IP that the instance is available on.


We can now deploy this template with a Deploy an AWS CloudFormation template step.
