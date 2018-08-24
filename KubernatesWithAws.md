
###Install and configure aws CLI

Installing aws cli
https://docs.aws.amazon.com/cli/latest/userguide/awscli-install-linux.html

Configuring aws cli :
Configure the cli to use by aws user
https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html

Guide for using aws cli :
https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-using.html


###Networking :

Understanding IP,Subnet, CIDR
https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking


Create a VPC and get the vpc id, tag the vpc using the vpc ID (key=name,value=kubernetes)
modify vpc attribte to enable dns support and enable dns hostnames

DHCP Option set (domain name and domain name server)

SUBNET :: Create a subnet and tag (name) 

Internet Gateways :: Create an internet gateway and attach it with the above created VPC

Route Tables :: create a new routing table with tag (name) 
                associate the above created subnet with the routing table 
                add another route 0.0.0.0/16 and igw(above created internet gateway)


####Firewall Rules :

SG (Security Group) :: Create a security group with a discription and tag(name)
                       Add inbound rules to vpc ( Firewall rules )

####Kubernates Public Address 

Create load balancer with subnet and the security group 
DNS - kubernetes-1948820705.eu-west-1.elb.amazonaws.com


###Provision Virtual Machines
Ubuntu 16.04
All machines will be created with the --no-source-dest-check flag to enable traffic between foriegn subnets to flow. that will enable pods to communicate with nodes and another pods via the cubernates server IP.

Creating Instance IAM Policies :: create the iam role json with required statements 
                                  create role using that kubernates-iam-role.json
                                  create the iam policy json
                                  attach that policy document with the created role
                                  create instance profile and add the above created role to that instant profile.

Pick the latest Ubuntu Xenial server :: Within the same region  -- AMI

Generate the SSH key pair ::  put in ~/.ssh/kubernates_the_hard_way
                              give permission chmod 600 ~/.ssh/kubernates_the_hard_way
                              and ssh-add ~/.ssh/kubernates_the_hard_way

SSH Access (login to kubernates nodes) see the documentation :)

###Virtual Machines
####Kubernetes Controllers 

create an instance by adding iam-instace-profile("kubernates") and imagethe AMI we selected above and attaching the security group assigning a private-ip in the range 10.240. in the subnet we created

Once created the instance modify the instance-attribute --no-source-dest-check

tag the instance as controller0

follow the same process to create 3 controller instances controller0,controller1,controller2

####Kubernetes workers

Follow the above steps to create 3 workers 


#####Verify

Veryfy the instances which are created as controllers and workers





















