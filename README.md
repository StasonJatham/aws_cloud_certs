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



Inline `code` has `back-ticks around` it.

```python
s = "Python syntax highlighting"
print s
``` 
