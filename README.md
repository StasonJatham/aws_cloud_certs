# aws_cloud_certs
Notes for AWS Certifications

[1. AWS Cloud Practitioner](#aws-cloud-practitioner)

## AWS Cloud Practitioner

### AWS Overview
(AWS) Cloud is
- more efficient
- scalable 
- reduced risks because agile , can adapt to change
this reduces risk 

scalable
- use services at own pace
- scalabiullity = use resources needed (more or less) 
- cloud can adapt to needs

- high availabillty
- increase speed

agile
- use aws datacenters to get close to customers
- global reach 
- focus less on infrastrucutre

experiment with low cost an low risk
leads to more innovation

elasticity
-scale resources up or down quickly
- add resources needed
- shut down resources no longer needed

low latency and better experience fgor your customer

reliabillty
get computing resources as needed
get more capacity that oon-prem does not have

AWS regions
- seperate geograpühic region 
- isolated in many availabillty zones

places reesources in multiple different location 
using more availabillty zones gets more fault tolerance

fault tolerance = system remains operational even though some parts of it fail 
downtime is minimized without human intervention

You own your own data, amazon doies not have access to your data, you hold the encryption keys 

AWS monitoring contoinually 

AWS industry leading capabillities , so services meet stricted security requirements

AWS datacenters are protected by security guardss and access is strictly regulated 

aws assets can use your own security policies freom the get go 



### AWS Management Interfaces

convenient options of using resources
- AWS Management Console
graphical interface to access feature
easy search for what you need
browse through all servioces
you can pin icons right to the toolbar
resource groups to streamline aws console
quickly navigate to each resource group

Resource Groups are identiy specifc so each user can create their own 
youz can share resource group defintions with users in same account 

learn to build has learning resources like tutorials and guides docs so you can learn to build what you need




- command line interface
lets u control aws from command line
used to automate and repeat tasks
all operating systems are supportewd



- Softwarew Development Kits (SDK)
control api through programming languages 
help u use aws in existing applications



all built upon aws api = foundation 
can use all of the above ways interchangibly 


power to scale computignn resources up and down quickly = elasticity 







### AWS Core Services

talk about key services and common use cases

What are the benefits of using amazon ec2 instances compared to physical infrastreucute ?
- pay only for the capacity you use 
- the abillity to have different storage requirementss

Which components of AWS infrastrucutre can be described as multiple isolated locations within one geographic area ?
- Availabillty Zones

Which of the follwoiung staetements is true of amazon virtual private cloud ?
- you can create ,amy subnets in a VPC altough fewer is recommended to limit complexity

#### EC2 - Elastic Compute CLoud
what is ec2 - elastic compute cloud
compute - different servers
cloud - cloud hosted
elastic - scalable

- pay as you go 
- broad hardware and software selction
- global hostin g

build an ec2 instance
- login to aws console
- choose region
- launch ec2 wizard
- select ami - amazon machine image
- select instance type (hardware)
- configure network
- configure storage 
- add tags - give friendly name
- configre security group - set of firewall rules (creates auto rule for ssh connect)
(add rules like open port 80 and name the security group
- click launch 
- create a key pair and downlaod private key (this key is needed to connect vie ssh to you ec2 instance)
- access the instance , below you can find public ip and isntance name (default user ec2-user) use putty to connect an dconfigure private key then you can connect (ssh auth and add private key we downloaded earlier)
(on windows use puttygen and transform thew ssh private key .pem  to .ppk)


#### EBS - Elastic Block Storage
- choose between hdd or ssd (pay as you use)
- persistent and customizable block storage for your ec2 
- automatically replicatable in the same availabillity zones
- backup using point in time snapshots (copy snapshots and recover instantly) 
- easy and tranparent encryption at no additional cost (encryption happens on ec2 site)
- elastic volumes, meaning increase capacity or change hardware from hdd or ssd without havong to stop instances


- volume has to be in same zone as ec2 instance 
- create volume
- specify availabillty zone (same as ec2 instace
- pick volume type 
- click create volume 
- attach to ec2 - click actions and attach , click the desired volume and name the device (like /dev/sdb)
- now go to instances and connect to instance (copy and paste the ssh command)
- check storage with `lsblk` 
- create a filesytsem on the new storage with `sudo mke2fs /dev/xvdb` 
- now linux is creating filesystem on volume 
- now you can mount volume as folder into linux machine 
- to mount we do `sudo mount /dev/xvdb /mnt` , now volume mounted in /mnt folder
- `cd /mnt` , now we are on the new block, you can do everythiong like make a file and folder etc.
- if i want i can `unmount /mnt` and detach the volume back in the aws console, i could attach it to another instance in the same availabiltyx zone 
- add tag value to describe what you used it for 
- tags are very important for example anme the volume "Databasse VOlume" if it hosts a databse

#### S3 - Simple Storage Service
- fully managed storage service (simple api for storing and grabbing data)
- store virtually unlimited number of object 
- can store any type of data or file 
- supports objects several tb in size 
- access anytime, from anywhere, also access privately through vpc endpoint
- rich security tools, per access control , security policies , encrypt in transit or encrypt on server

vreate bucket to hold data 
- specify a key used to retireve file late r
- name like a filepath like "files/test.py"
- highly scalable 
- only billed fo what you use
- url = bucketname.region-specific.objectkey
- suitable for wiude range of scenarions 
- app data , static web hosting, bnbackup and disaster recovery, staging area for big data ..

s3 in action
- go to amazon s3 section through managem,nt console
- create bucket 
- set bucket naem (dns compliant)
- set region (best to use the region where all your stuff is at
- hit create and now we have out bucket
- click on new bucket and you can uplaod files (drag and drop)
- use aws cli, so i have a local file i want to vcopy to aws s3 bucket 
 in cli i type  `aws s3 cp awesome.html s3://mybucketname/awesome.html`
- i can also upload an entire folder usin "sync" like so 
  `aws s3 sync my-folder s3://mybucketname/my-files`
- in managemt console , check out the files we uplaoded and click on one 
- here you see some options to modify permissions on the files etc.


#### AWS Global Infrastructure

aws regions
- geographioc regions houseing 2 or more availabillty zone
- optimize latency while minimizing costs
- regulatory stuff
- you can deploy reosurces in multiple regions 
- regions completely seperated services 
- not all resources are available in all regions 

availabilltyy zones
- collection of datacenterts in region
- each zone is seeperated physically and logically
- netwrokign are connected to each other 
- hoooked up through different electric and interne tprovider
- ensure data redundaqncy and availabillty

edge locations
- host a CDN name cloudfornt 
- used to deliver content to customers
- close to customers

#### VPC - Amazon Virtual Private Cloud
- is a networking servide that will meet your networking requirements
- create private network in cloud, uses same concepts as on premise network
- allow complete control of network configuration, you can isolate and expose resources inside VPC
- offers several layers of security contzrols, allow and deny specific internet and internal traffic
- other aws services deployy into VPC, services inherit security built into network 

- is AWS foundational service and intigrates with all other standard srevices like ec2, rds , s3 , dynamo db etc.
##### features
builds upon globalö infrastructure of regions and infrastructres
hgihly available
amazon vpc liuves within a region 
multiple vpcs per account

subnets
used to divide amazon vpc
allows amazton vpc to span multiple availabillty zones

route table 
control traffiic going in and out

iinternet gateway (IGW)
allow acces toi the internet from amazon vpc

nat gateways
allows private subnet resources to access internet

Network acces control lists (NACL)
control access tto subnets, stateless

build an VPC
- choose region 
- defgine address space (like 10.0.0.0/16)
- make a subvnet like 10.0.0.0/24
- specify subnet live in Availabillty zone A
- make another subnet with 10.0.1.0/24
- this subent also lives in availabillty zone A
- next add a Internet Gateway - hook it up to Subnet A (will be public subnet
- SUbent B will be a private subnet not accessible from thge interent 


#### Security Groups
- sact as built in firewall
- control accessabillty of instances
- filter traffic to instances
- allow treaffic in and out
- configure security roles
- you can make an instance compeletely private or public 

create a security group
- click on ec2
- click on network and securioty
- create security group
- name "web-server-sg"
- descriuption "allow web traffic"
- allow http/https
- http - tcp - 80 - 0.0.0.0/0
- https - tcp - 443 - 0.0.0.0(0
- click create 
- now we hhave a security grooup for a web server






### AWS Integrated Services

talk about key services on aws and use cases 

You have an application composed of individual services. You need to route a request to a service based on the content of the request. Which service should you use?
- Elastic Load Balancing

What is the firststep in getting started with AWS Lambda?
- upload your code


#### Application Load Balancer
- abillity to enable additional routing services
- why use app laod balancer 
- use container for microservices and routew requests to them 
- different container, lsitening on different poirts you can set up routing rules for different locations
- Listeners = proicess that checks for connection request using protocol and port 
- Target = target for destination traffic based on the established lsitner rules
- Target Group = routes requests tto one or more regisstered target using protocol and port number specified

- Supported Protocols: HTTP, HTTPS, HTTP/2, WebSockets
- ClouWatch Metrics: additional load balance metrics and target group metric dimension
- Access Logs: connection details for websockets cpnnections
- HealthChecks: insight into target and application health at more granular level

- path base routing - route based on path url 
- host based routing can route by host

create a load balancer
- go to ec2 console
- (have some instances ready)
- copy public ip of instance 
- go to the public ip (website that ione contaienr hsots
- go to other container public ip with other website
- side navigation click on Load Balancers
- create load balancer (choose application laod balancer)
- name the load balancer (dns friendly name)
- leave ipv4 default 
- default has is listening on port 80
- add listener http - 443
- select avaiulabillty zone (you have to use 2 - so vpc and use the 2 u used for you subnets )
- key: name , value: application load balancer (use a more dexcriptive name for your)
- skip security settings
- deselect security group and select your security group for xour vpc
- configure routing
- keep new target group
- naem it as yu please
- protocol http and port 80
- health check destination http (test.html)
- leave hgealth check rest to default
- select test instance and add to registered 
- next get to review page and check out you settings
- click create and hoepfully everything went ok
- register second target 
- create a target group
- target group name = demo2
- check http request port 443
- health check http test.html
- leave rest to default on health check
- create the target group
- yay success
- click on laod balancer on the left and verify both ports listening (80 and 443)
- view and edit rules to stop forward 443 to demo1 , edit "THEN" forward to demo2
- test to verify that traffic is sent to each contaienr
- copy dns name and open first container in browser
- copy dns name of conatienr two and paste in browser - this should forward to container2 

#### Auto Scaling
- help ensure that you have the correct number of ec2 instances available to handle your workload
- add or remove ec2 instances on conditions you specify
- optimize perofmance and minimize costs
- on-demand resource provisioning
- scaling out = launch instances at condition like cpu utilization 80%
- scaling in = terminate instances

Auto Scaling Components
- Launch configuration
what will be launched by autocaling ?
think of everything needed to start ec2

- auto scaling group
which vps and subnet 
which load balancer 
minimun instances
desired capacity

- auto scaling policy
when to laucnch ?
scheduled, on-demand, scale out policiy, scale in policy

Dynamic Auto Scaling
- cloudwatch alarm triggers autoscaling alarm which will scale out or in 

Sample cloudwatcvh alarm 
- whenever `CPUUtilization` is `>=` `80` for `1` consecutice period (default is 5 minutes per period)
  - whenever this alarm `State is ALARM` From reource type `AutoScaling` From the: `IREASG`take this action: `increase group size - add 2 instances`


Konfigure
- open ec2
- left pane click auto scaling groups
- click on create auto scaling grroup
- create launch configuration
- next steps basically same as EC2 creation
- name launch configuration 
- leave the default settings for storage and security groups
- revies and create
- choose existing keypair and create launch config
- create auto scaling group 
- group anme 
- group size (for example 2)
- choose network to deploy to  (VPC)
- pick subnet to deploy to 
- configure scaling policies
- set sacaling between 2 and 8 (min - max)
- taregt value avg of 60% (auto create and terminate instances)
- crate auto scaling group
(now you will see 2 pending instances if you picked 2 above)


#### Amazon Route 53
DNS servie
- route end users to applications
- user -> browser -> yourapp.com -> ISP -> route 53 -> yourapp.com (send back IP and shows user your app)

Route 53
- create hosted zone (where yyour namesevrer DNS data is kept)
- specify fully qualified domain name (use route 53 or external domain)
- you can have internal or external hosted zones

Create A hosted zone
- werbapp on EC2 with public IP
- routre53 -> create a hosted zone
- put your domain in domain name 
- type public hosted zone 
- create record set (create subdomains for app) -> www.yourdomain.com -> type A IPv4 -> Value= EC2 public IP
- in value you can put load balancer or S3 name as well
- save record set and it is ready to route 

Route 53 offers different types of DNS resolutions:
- simple routing
- geo-location
- failover
- weighted round robin
- latency based
- multi value answer

#### AmazonRDS -  Relations Database Services
- cost efficient and resizable capacity
- lets you focus on applications and not on maintnance
- primary focus is your dat a
- handles all maintnance like os patches, scaliung etc
- managed RDS service

Database Instance
- consists of: cpu, memory, network perofrmace
- storage: magnetic, SSDm provisioned IOPS
- db engines: mysql, amazon aurora, Microsoft sql, postgresql , mariadb, oracle

- you can use a RDS inside of a VPC
- usually isolated in a subnet
- configure databse instance for high availabilty with multi- availabillty zone config

Benefits:
- supports most demanding databse applications
- high scalable
- high performance
- no downtime scaling
- easy to administer
- available and durable
- secure and compliant 


#### AWS Lambda
serverless compute service
- lets u run code without provisioning service
- sclaes automatically and runs code
- only pay for cpompute you use
- dont pay for compute time when not used
- virtually run any application 
- fully managed service
- suppoort: nodejs, java, c# and python
- event driven computing , like api requests or moonitoring m,eesages
- develop serverless applications 

image recoigniton app 

user maeks photo -> mobile app uploads to S3 -> aws lambda is triggered and calls recognition -> detect objects and scense and returns labels -> sernt to lanbda -> sent to S3 -> sent to app and user

- pick lambad form management console
- create function and name function
- choose runtime and name handler
- choose execution role 
- choose memory
- choose execution timeout
- config trigger
- example to use cloudwatch trigger to watch something
- when SNS happens then run lambda

Use Cases:
- process objects to S3
- IoT
- operrating serverless websites
- dynmaic updates and configs

#### AWS Elastic Beanstalk
- platform as a service
- plug code into beanstalk
- allows for quick deployment of your application
- reduces management complexity
- choose instance type -> choose databse type -> set adn adjust autoscaling
- update application , access server log files, enable https on laod balacner
- supports a lot of differen paltforms (docker, go, java , python , node js ,php....(basiucally any web tech))
- **create application -> upload version** -> launch environmetn -> manage evironment (last parts are handled by beanstalk=

use beanstalk
- u have a python web service
- zip the application
- choose elastic beanstalk from management overview
- create new application
- enter the new name and description 
- create the environment (example web server environment)
- enter domain , platform (like python), a description
- upload your code (python zip file)
- create environment


#### Amazon SNS - Simple Notification Service
- flexible fully messaged pub/sub meesaging mobile communication service
- coordinates delivery of messages to subscribing endpoints to clients
- easy to setup, operate and send reliable communications
- decouple and scale microservices, distributed systems and serveröless applications

how to use this sweet SNS:
- SNS dashboard
- create topic
- enter topic name and display name 
- Other topic actions -> basic view -> everyone (usually specify people to send to)
- create subscription
- for email - pick email in prtocoll
- endpoint is your email address
- confirm subscription in your email


#### Amazon CloudWatch
- monitoring servcie real time for resources and applications
 - collect and track metrics
 - collect and filter log files
 - set alarms
 - auto react to changes


#### Amazon CloudFront


#### Amazon CloudFormation


Inline `code` has `back-ticks around` it.

```python
s = "Python syntax highlighting"
print s
``` 
