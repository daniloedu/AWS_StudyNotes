# Personal Notes
## *Solutions Architect Certification 2021*

[![N|AWS](https://miro.medium.com/max/1248/1*BAsXOt5-QpdWNiKm-lAD-w.png)](https://aws.amazon.com)

## Quick availability reminder.
| Service | Availability |
| ------ | ------ |
| EC2 | 99.99% |
| S3 Standard, S3 Reduced Redundancy| 99.99% |
| S3 Standard-IA, S3 Intelligent Tiering, S3 Glacier Instant Retrieval | 99.9% |
|S3 Glacier Flexible Retrieval and S3 Glacier Deep Archive Class | 99.99%

*When you calculate the availability for multiple products you have to sum the total percentage of individual unavailability. For example for 3EC2 instances.*
` 100% - (10%* 10% * 10%) = 99.9% `

## Some Userful Numbers
* 25 regions before Re:invent 2021.
* 81 Availability Zones before Re:invent 2021.
* 5 VPCs per region (soft-limit)
* 200 Subnets per VPC (soft-limit)
* IPv4 CIDR blocks per VPC is 5 (soft-limit)
* IPv6 CIDR blocks per VPC is 1 (soft-limit)
* 5 Elastic Ip Address per region. (soft-limit)
* VPC must have a mask of at least /16 
* The maximum possible prefix length for an IP subnet is /32
*More information at [AWS Global Infrastructure]*

## For EC2 Instances
* AWS Snowball edge is best suited for IoT applications. There is one for memory optimized and other for computing optimized.
* Amazon Data Lifecycle Manager to make weekly backups of EC2 instances.
* By default, AWS has a limit of 20 instances per region (soft-limit)
* The VM Import/Export tool handles the secure and reliable transfer for a virtual machine between your AWS account and local data center. 
* The instance type determines the size of the instance store available and the type of hardware used for the instance store volumes. 
* Instance store volumes are included as part of the instance's usage cost. You must specify the instance store volumes that you'd like to use when you launch the instance (except for NVMe instance store volumes, which are available by default).

## Simple Storage Service (S3)
* All S3 names need to be globally unique.
* You can use prefixes to apply lifecycle rules to only certain objects within a bucket. 
* You should also be aware that there are minimum times (30 days, for instance) an object must remain within one class before it can be moved.
* You can’t transition directly from S3 Standard to Reduced Redundancy. 
* For pre-signed URL the default expiration value is 3,600 seconds (one hour) 
* Glacier guarantees 99.999999999 percent durability 
* Glacier supports archives as large as 40 TB, whereas S3 buckets have no size limit 
* Glacier is encrypted by default
* Glacier IDs are machine-generated IDs. Glacier names don’t have to be unique.
* Glacier vault = S3 bucket.
* In a bucket single object may be no larger than 5 TB. 
* Individual uploads can be no larger than 5 GB. 
* Use Multipart Upload for any object larger than 100 MB. As the name suggests, Multipart Upload breaks a large object into multiple smaller parts and transmits them individually to their S3 target. 
* When using Transfer Acceleration, uploads are routed through geographically nearby AWS edge locations and, from there, routed using Amazon’s internal network. 
* You’re allowed only 100 S3 buckets per account. 
* Security groups are not used with S3 buckets. 
* The principal is the user to be assigned in an attached policy.
* Amazon S3 inventory lets you make audits of the objects in the bucket.
* AWS Backup allows to make backup plans for
    * Aurora
    * Amazon FsX
    * Amazon EFS
    * AWS Storage Gateway
    * EBS
    * RDS
    * DynamoDB.
* S3 Remote acceleration will work for two buckets in different regions.
* RTMP distributions can manage content only from S3 buckets. RTMP is intended for the distribution of video content. 
* Access Analyzer for S3 alerts you to S3 buckets that are configured to allow access to anyone on the internet or other AWS accounts, including AWS accounts outside of your organization.
* Athena lets you perform advanced SQL queries against data stored in S3. 

## Amazon MQ
* Amazon MQ, Amazon SQS, and Amazon SNS are messaging services that are suitable for anyone from startups to enterprises. If you're using messaging with existing applications, and want to move your messaging to the cloud quickly and easily, we recommend you consider Amazon MQ.  
* If you are building brand new applications in the cloud, we recommend you consider Amazon SQS and Amazon SNS.
* Compatible with RabbitMQ

## AWS Lake Formation
AWS Lake Formation is a service that makes it easy to set up a secure data lake in days. A data lake is a centralized, curated, and secured repository that stores all your data, both in its original form and prepared for analysis. 

## Application Load Balanccer
Because an Application Load Balancer terminates incoming TCP connections and creates new connections to your backend targets, it does not preserve client IP addresses all the way to your target code (such as instances, containers, or Lambda code). The source IP address that your targets see in the TCP packet is the IP address of the Application Load Balancer. However, an Application Load Balancer does preserve the original client IP address by removing it from the original packet’s reply address and inserting *it into an HTTP header before it sends the request to your backend over a new TCP connection.*

## Virtual Private Cloud (VPC)
* You can’t change the primary CIDR block after you create your VPC, so think carefully about your address requirements before creating a VPC. 
* You can’t choose your own IPv6 CIDR.
* All IPv6 addresses are reachable from the Internet. 
* The prefix length of an IPv6 VPC CIDR is always /56. 
* VPN connections are always encrypted. 
* You must always assign an IPv4 CIDR block to a subnet, even if you intend to use only IPv6. 
* If your VPC includes an IPv6 CIDR, AWS will automatically add inbound and outbound rules to permit IPv6 traffic. 
* Global Accelerator static addresses are spread across different AWS points-of-presence (POPs) in over 30 countries. These static addresses are also called any-cast addresses because they are simultaneously advertised from multiple POPs. 
* In VPC peering, can’t use it to share Internet gateways or NAT devices. You can, however, use it to share a network load balancer (NLB). 
* In VPC peering If you want to enable peering only between specific subnets, you can specify the subnet CIDR. 
* Inter region VPC peering is not available for some AWS regions. Peering connections between regions have a maximum transmission unit (MTU) of 1,500 bytes and do not support IPv6. 
* AWS Transit Gateway 
    * You can configure a transit gateway to function as a centralized router that controls how traffic is routed among all of your VPCs and on-premises networks. 
    * Isolated VPCs.- When you have multiple VPCs that you want to connect to an on-premises network but want to keep the VPCs isolated from each other. 
    * Isolated VPCs with Shared Services.- If you’re hosting shared services (such as Active Directory or Link Layer Discovery Protocol [LLDP]) in one VPC, you can use a transit gateway to securely share those resources with other networks, while maintaining isolation among them. 
    * Transit Gateway Peering.- You can peer transit gateways together, even between different regions.
    * Multicast.- AWS Transit Gateway supports multicast traffic between VPCs (Note that a multicast receiver can be any EC2 instance, but the sender must be a Nitro instance.)Keep in mind that multicast routes do not appear in any route tables. 
    * Blackhole Routes.- If you want to block a specific route, you can create a blackhole entry for that route in the transit gateway route table. 
* Unlike VPN connections, Direct Connect links are not encrypted. However, because AWS endpoints are all secured by TLS, traffic between your on-premises network and AWS is secure. 
* Elastic Fabric Adapter.- It’s for super fast TCP/IP networking connections for clusters.
* AWS ParallelCluster can automatically manage your Linux-based HPC cluster so that you don’t have to do it manually 
* A subnet cannot span availability zones. 
* Every ENI must have a primary private IP address. 
    * It can have secondary IP addresses, but all addresses must come from the subnet the ENI resides in. 
    * Once created, the ENI cannot be moved to a different subnet. 
    * An ENI can be created independently of an instance and later attached to an instance. 
* Each VPC contains a default security group that can’t be deleted.
* You can create a security group by itself without attaching it to anything. 
* You also attach multiple security groups to the same ENI. 
* An NACL is attached to a subnet, whereas a security group is attached to an ENI. 
* An NACL can be associated with multiple subnets, but a subnet can have only one NACL. 
* An Internet gateway has no management IP address. 
    * It can be associated with only one VPC at a time and so cannot grant Internet access to instances in multiple VPCs. 
    * It is a logical VPC resource and not a virtual or physical router. 
* Every subnet is associated with the main route table by default. 
* A NAT gateway is a VPC resource that scales automatically to accommodate increased bandwidth requirements. A NAT instance can’t do this. 
* A NAT gateway exists in only one availability zone. 
* There are not multiple NAT gateway types. 
* A NAT instance is a regular EC2 instance that comes in different types. 
* The source/destination check on the NAT instance’s ENI must be disabled to allow the instance to receive traffic not destined for its IP and to send traffic using a source address that it doesn’t own. 
* A peering connection can be used only for instance-to-instance communication. You can’t use it to share other VPC resources (except NLB).
* You cannot route through a VPC using transitive routing. 
* The Site-to-Site VPN tool doesn’t use OpenVPN. 

More information about limits at [AWS VPC Limits]

## AWS Artifact
* Is your go-to, central resource for compliance-related information that matters to you. It provides on-demand access to AWS’ security and compliance reports and select online agreements. Reports available in AWS Artifact include our Service Organization Control (SOC) reports, Payment Card Industry (PCI) reports, and certifications from accreditation bodies across geographies and compliance verticals that validate the implementation and operating effectiveness of AWS security controls. Agreements available in AWS Artifact include the Business Associate Addendum (BAA) and the Nondisclosure Agreement (NDA).
* List of services that comply with (PCI DSS) Level 1 for the handling and transmission of credit card data [AWS PCI DSS]

## Systems Manager
* Automation documents let you perform actions against your AWS resources, including taking EBS snapshots. Although called automation documents, you can still manually execute them. 
* A command document performs actions within a Linux or Windows instance.
* A policy document works only with State Manager and can’t take an EBS snapshot.
* There’s no manual document type. 

## For IAM and authentication
* The Action element refers to the kind of action requested (list, create, etc.), the Resource element refers to the particular AWS account resource that’s the target of the policy, and the Effect element refers to the way IAM should react to a request. 
* For IAM policies In general, an explicit deny effect will always overrule an allow. 
* There’s no such thing as an IAM action statement. 
* The top-level command is IAM, and the correct subcommand is get-access-key-last-used. The parameter is identified by --access-last-key-id. 
    * Parameters (not subcommands) are always prefixed with -- characters. 
* X.509 certificates are used for encrypting SOAP requests, not authentication. 
* AWS CloudHSM provides encryption that’s FIPS 140-2 compliant.
* Key Management Service manages encryption infrastructure but isn’t FIPS 140-2 compliant. 
* Security Token Service is used to issue tokens for valid IAM roles
* Secrets Manager handles secrets for third-party services or databases. 
* Identity pools provide temporary access to defined AWS services to your application users 
* IAM policies are global—they’re not restricted to any one region. Policies do, however, require an:
    * action (like create buckets)
    * an effect (allow)
    * and a resource (S3).  
* STS tokens are used as temporary credentials to external identities for resource access to IAM roles.
* Differentiate between Cognito identity pools and user pools.
* Rotation Process:
    * Monitor the use of old keys
    * Deactivate old keys.
    * Delete old keys.
* You attach IAM roles to services in order to give them permissions over resources in other services within your account. 
* IAM keeps five versions of every customer managed policy 
* RunInstances action launches a new instance.
* StartInstances starts an existing instance but doesn’t launch a new one. 
* Granting a user access to use a KMS key to decrypt data requires adding the user to the key policy as a key user. 
* VPC flow logs record source IP address information for traffic coming into your VPC. 
* You can use an IAM policy or SQS access policy to restrict queue access to certain principals or those coming from a specified IP range. 
* A security group to restrict inbound access to authorized sources is sufficient to guard against a UDP-based DDoS attack. 
* You can revoke and rotate both a customer-managed CMK and a customer-provided key at will. You can’t revoke or rotate an AWS-managed CMK or an S3-managed key. 
* AWS-managed CMKs are rotated only once a year. 
* You can install an ACM-generated certificate on a CloudFront distribution or application load balancer. You can’t export the private key of an ACM-generated certificate, so you can’t install it on an EC2 instance. 
* Security Hub checks the configuration of your AWS services against AWS best practices. 
* An IAM group is not a principal. It’s not possible to perform actions under the auspices of a group in the way that you would a role. 
* A role is an IAM principal that doesn’t have a password or access key. 
    * The IAM user that assumes the role can be in the same account as the role or in a different account 
* Users without AWS credentials tend to consume the AWS services that offer resource-based policies. 
* It can take up to 15 minutes between the time an event occurs and when the CloudTrail creates the log file containing the event. 
* AWS Config can alert you when a resource configuration in your AWS account changes. It can also compare your resource configurations against a baseline and alert you when the configuration deviates

## GuardDuty
* Amazon GuardDuty offers threat detection enabling you to continuously monitor and protect your AWS accounts, workloads, and data stored in Amazon Simple Storage Service (Amazon S3).
* Amazon GuardDuty is a regional service.
* Analyzes AWS CloudTrail, VPC Flow Logs, and AWS DNS logs.
* Amazon GuardDuty is priced based on the quantity of AWS CloudTrail Events analyzed and the volume of Amazon VPC Flow Log and DNS Log data analyzed
* Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS. Support Linux and Windows Server instances.
* There are no upfront costs and you pay only for the events analyzed, with no additional software to deploy or threat intelligence feed subscriptions required.
* Consider the following actions:
    * The Behavior finding type is triggered by an instance sending abnormally large amounts of data or communicating on a protocol and port that it typically doesn’t. 
    * The Backdoor finding type indicates that an instance has resolved a DNS name associated with a command and control server or is communicating on TCP port 25. 
    * The Stealth finding type is triggered by weakening password policies or modifying a CloudTrail configuration. 
    * The ResourceConsumption finding type is triggered when an IAM user launches an EC2 instance when they’ve never done so. 
* You do not need to stream any logs to CloudWatch Logs for GuardDuty to be able to analyze them. 
* finding is a notification that details the questionable activity 
* Findings can be categorized in:
    * Backdoor.- EC2 compromised with malware, DDoS attacks, TCP port 25
    * Behavior.- Unusual port or large amount of traffic to an external host.
    * Cryptocurrency.- It may be sending, receiving, or mining Bitcoin. 
    * Pentest.- A system is running Kali Linux. Penetration testing
    * Persistence.- IAM user changing resource permissions, security groups, routes or ACLs
    * Policy.- Root credential used or S3 block public access was disabled.
    * Recon.-  This indicates a reconnaissance attack may be underway
    * ResourceConsumption.- Launching an EC2 instance
    * Stealth.- Password policy was weakened.
    * Trojan.- An EC2 may have a trojan installed.
    * UnauthorizedAcces.- Via API or console.
* Notice that every finding type relates to either the inappropriate use of AWS credentials or the presence of malware on an EC2 instance. 
* It’s different from Amazon Macie that helps you discover and protect your sensitive data in Amazon S3 by classifying what data you have and the security, along with the access controls associated with that data.
* Customers can choose to aggregate security findings produced by Amazon GuardDuty across regions by utilizing Amazon CloudWatch Events

## Amazon Inspector
* Amazon Inspector is an agent-based service that looks for vulnerabilities on your EC2 instances. 
* Inspector agent runs an assessment on the instance and analyzes its network, filesystem, and process activity.
* Common Vulnerabilities and Exposures (Linux and Windows) 
* Center for Internet Security Benchmarks  (Linux and Windows) 
* Runtime Behavior Analysis (Linux and Windows) 
* Network Reachability (Linux and Windows)
* Security Best Practices  (Linux Only)
* Types of alerts:
    * High - Fix ASAP
    * Medium - At next possible opportunity
    * Low - Informational

## Amazon Detective
* Detective is designed to help you correlate events and see how a given event affects particular resources 
* Instead of digging though CloudTrail logs manually.

## Security Hub
* Display findings in user-friendly dashboard.
* Security Hub assesses your account against AWS security best practices and the Payment Card Industry Data Security Standard (PCI DSS). 
* Gathers info from Inspector, GuardDuty and Macie.




## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [AWS Global Infrastructure]: <https://aws.amazon.com/about-aws/global-infrastructure/>
   [AWS VPC Limits]: <https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html>
   [AWS PCI DSS]: <https://aws.amazon.com/compliance/services-in-scope/>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
