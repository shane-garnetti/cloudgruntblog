---
title: "Like Ogres and Onions, Security Has Layers: AWS Services That Will Help You Achieve Defense in Depth"
date: 2023-02-02T12:52:41-08:00
draft: false
tags: ['Security']
---

![Shrek](/shrek.png)

## What is *Defense in Depth* and why is it important?

I am so glad you asked! Defense in Depth (*Layered Security*) is the critical concept of achieving a thorough security posture by implementing protection at multiple resource levels. Think of the White House for example…There are multiple components in place securing the building and the personnel inside. Would it be sufficient to only have a lock on the front door? If I was a betting man, my answer would be no, not it would not. The White House has fences, multiple types of locks on doors, security cameras, smart sensors, special agents, military personnel, air defense–-I think you get the point. When designing solutions in the cloud, it is critical to implement the same layered security approach to protect data, customers and stakeholders. AWS offers a wide variety of security services and design best practices that can help you achieve ultimate fortification. In this blog, I will do the heavy lifting for you by breaking down key security services in AWS, design considerations, and best practices so you can build presidential quality solutions. Let’s get after it!

# Key AWS Security Services...

## Network Defense

**Virtual Private Cloud (VPC)**:
VPC enables you to launch resources into a virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

**AWS Network Firewall**:
AWS Network Firewall is a stateful, managed, protection and prevention service that acts as the first line of defense at the network layer for your VPC. It includes traffic filtering to and from your other AWS network resources along with open source Intrusion Prevention System (IPS) for stateful inspections. 

**Network Access Control Lists (NACLs)**:
NACLs are an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You can use network ACLs to set rules that explicitly allow or deny traffic based on source and destination IP addresses, ports, and protocols.

**Security Groups**:
Security Groups act as a stateless virtual firewall for your EC2 instances and AWS resources. Acting as the last line of defense for controlling inbound and outbound traffic. You can specify which protocol, ports, and source IP ranges are allowed to reach your instances. It is important to note that Security Groups do not allow explicit denies, and any protocol, port or IP that is not included in the configuration, will be denied implicitly. 

**Private Link**:
PrivateLink is a feature that enables you to access services over a VPC endpoint, rather than over the Internet. Private Link increases security by ensuring your traffic remains private through a VPN. This reduces the risk of potential eavesdropping and man-in-the-middle attacks. 

**AWS VPN**:
AWS VPN allows you to securely connect your on-premises data centers to your VPC, and to your VPCs across multiple regions. AWS VPN can be used to create a secure communication channel between your data center and your VPC, and can also be used to connect multiple VPCs to each other.

**Gateway Load Balancer**:
Gateway Load Balancer provides a single entry point for all traffic, and it can route the traffic to the appropriate service based on the content of the request. It is a combination of Application Load Balancer (ALB) and Network Load Balancer (NLB) and it allows you to use them together to handle different types of traffic.


## Application Defense

**Web Application Firewall (WAF)**:
AWS WAF helps protect web applications from common web exploits that could affect application availability, compromise security, or consume excessive resources. AWS WAF gives you control over how traffic reaches your applications by enabling you to create security rules that block common attack patterns, such as SQL injection or cross-site scripting (XSS), and rules that filter out specific traffic patterns you define. WAF offers a free set of AWS managed rules, along with third party rule sets from reputable firewalls such as Palo Alto, Fortinet and many others. 

**CloudFront**:
CloudFront is a managed Content Delivery Network (CDN) service. It caches content at strategically-located edge locations around the world, so that when a user requests content, the content is delivered from the edge location that is closest to the user. This improves the performance of the content delivery by reducing latency, as well as increasing performance of backend resources by reducing the number of direct hits. CloudFront also improves security by using HTTPS and to restrict access to content using signed URLs or signed cookies. Additionally, CloudFront integrates with AWS Web Application Firewall (WAF) to provide an additional layer of security for your content.

**AWS Shield**:
Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards web applications running on AWS. AWS Shield provides always-on detection and automatic inline mitigations that minimize application downtime and latency.

**Network Load Balancer (NLB)**:
Network Load Balancer is best suited for handling TCP/UDP traffic and it can handle millions of requests per second while maintaining ultra-low latencies. It is designed for handling heavy traffic, and it can automatically route incoming traffic to the optimal instance based on the health of the instances. This improves security by allowing your backend instances to reside in private subnets. Allowing the instances to only maintain an internal private IP that is not accessible over the internet.

**Application Load Balancer (ALB)**:
Similar to the Network Load Balancer, ALB routes HTTP/HTTPS traffic and is ideal for applications that require advanced routing and management features. It allows you to route a client request to one of the available service instances based on the content of the request. It also supports path based routing and is very useful for load balancing micro services. Leveraging an ALB also improves security by allowing your backend instances/microservices to reside in private subnets. Reducing the need for public IP addresses that could potentially be targeted over the internet.


## Intelligent Threat Detection

**GuardDuty**:
GuardDuty is a threat detection service that uses machine learning to automatically identify potential security threats in your AWS environment. It continuously monitors your AWS accounts, resources, and data streams for malicious or unauthorized behavior. It also generates findings that can be used to investigate and mitigate potential security issues.

**Inspector**:
Inspector is a security assessment service that automates the process of assessing the security of your Amazon Elastic Compute Cloud (EC2) instances. It helps you to identify vulnerabilities and misconfigurations in your instances, and it provides recommendations for how to remediate these issues. Inspector generates a detailed report that includes a list of the security issues that it identified, along with recommendations for how to remediate these issues. The report can be viewed in the AWS Management Console or can be exported to an S3 bucket for further analysis.

**Macie**:
Macie is a security service that automatically discovers, classifies, and protects sensitive data in AWS. It uses machine learning to identify sensitive data, such as personally identifiable information (PII) and financial data, then alerts you to any unauthorized access or changes to that data. Macie integrated with multiple storage services such as Simple Storage Service (S3), Elastic Block Store (EBS), Relational Database Service (RDS), and Elasticsearch Service domains. 

**EventBridge**
EventBridge allows you to create event-driven architectures where different parts of your application can respond to specific events. EventBridge can be triggered by API event calls from AWS resources and services, along with routine scheduled events. This can improve security by allowing event-driven workflows for automated and quick response times.


## Encryption

**Key Management Service (KMS)**:
KMS is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data. KMS keys can be used to secure your AWS resources along with on-premises resources.

## Compliance / Auditing

**CloudTrail**:
Cloudtrail continuously logs, monitors, and retains account activity related to actions across your AWS infrastructure. CloudTrail records AWS Management Console sign-in events, AWS SDKs, command line tools, and other programmatic calls for select services. These events are recorded in an event history that you can use to track changes to your AWS resources and troubleshoot operational issues.

**Config**:
Config assess, audits, and evaluates the configurations of your AWS resources. It provides an inventory of your AWS resources, and automatically tracks changes to the configurations of those resources. Config also supports Compliance Packs which are pre-built sets of AWS Config rules and remediation actions that customers can use to check resource configurations against specific compliance standards such as PCI DSS, HIPAA, FedRAMP, NIST, CIS and many others.

**Security Hub**:
Amazon Security Hub is a managed service that allows customers to centralize the security findings from multiple AWS services such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie, and third-party security solutions into one place. This allows customers to quickly identify and prioritize security issues and take action to remediate them.

## Account Management

**Identity and Access Management (IAM)**:
IAM allows customers to securely control access to their AWS resources. IAM enables customers to create and manage AWS users, groups, and permissions, and to use those entities to grant and deny access to AWS resources.

**Organizations**:
AWS Organizations is a service that allows customers to centrally manage and govern their AWS accounts. Organizations enables customers to create hierarchies of AWS accounts and to apply policies to those accounts at different levels in the hierarchy. This can improve security posture by isolating accounts and implementing Service Control Policies (SCP) limiting resources and API call limitations dynamically in each account.

**AWS SSO**:
AWS SSO connects workforce identities and manages their access centrally across AWS accounts and applications. IAM Identity Center is the recommended approach for workforce authentication and authorization on AWS for organizations of any size and type. AWS SSO supports MFA authentication and adds improved security for user and account management.

**Control Tower**:
Control Tower is a managed service providing a single location to set up a well-architected, multi-account environment to easily govern your AWS workloads with rules for security and AWS best practices. I often refer to Control Tower as the foundation for building a secure and well-architected organization.


# Design Considerations
![Mike Tyson](/mike.jpg)
#### When designing secure environments in AWS, it is important to understand the overall business objective and what security deliverables need to be met to to achieve the objective. 
#### Planning is good in theory, but it is critical that routine testing and validation of your defensive posture and tactics meet your expectations. So if an actual security incident does arise, you are not left on your back seeing little birds spinning around your head! 

#### When planing for a thoroughly secure design, consider the following 6 concepts as a baseline to start from:

## 1) Identity and Access Management 
- Who will be accessing this solution?
- Who will be managing this solution?
- What types of permissions will they need?
- How will they be authenticated?

## 2) Compliance
- Is there a required compliance standard that needs to be met such as HIPAA, PCI DSS, FedRAMP?, CIS, NIST?
- Will there be required audits? If so, how often and what type of data is needed for the audit?

## 3) Exposure
- Is this an internal facing solution?
- Is this an external facing solution?

## 4) Backup / Disaster Recovery
- Are backups required? If so, how often?
- Where will the backups be stored?
- How will backups be protected?
- If your account became compromised, would you be able to replicate your solution in another isolated account?
- Are there RTO and RPO standards?

## 5) Monitoring
- How will you proactively monitor for vulnerabilities?
- What metrics will be monitored to signal security related events?

## 6) Remediation
- If a security breach occurred, is there a documented procudure for how will you remediate?
- Is there any automated remediations actions required?
- Is there a validated Disaster Recovery solution that meets RTO/RPO requirements?

# Best Practices

### Superior security design begins with purpose…

#### Below are some security best practices in AWS:

**Least Privilege**
 
It is important to implement the Principle of Least Privilege (grant the minimum permissions necessary to perform a specific task) at all layers of the anticipated solution. Examples include IAM Policies, Firewall rules, network ports, security group configurations and subnet segmentation. This will ensure users, resource access, and network traffic are all limited to the specific needs and nothing more. 

**Multi Factor Authentication (MFA)**

MFA adds additional protection for users with access to AWS Accounts, backups and resources. 

**Encryption**

Utilize AWS KMS encryption both at-rest and in-transit along with HTTPS for web applications. This protects data from being compromised or accessed maliciously. High levels of encryption also may be required for certain security compliance requirements of solutions. KMS Customer Managed Keys offer additional security benefits as they allow a policy to be defined for key administration and usage.

**Firewalls**
	
Implement AWS WAF for layer 7 protection when hosting externally available solutions. Leverage AWS Network firewall for layer 4 protection. 

**Monitoring**

Monitor resource metrics and account behavior for anomalies and desired thresholds for notifications and remediations. AWS CloudWatch, GuardDuty, Config and Inspector can be perfect for this. It is critical to determine what type of metrics imply a security threat, then monitor those. If too many metrics are being monitored and notifications are being automated, this can cause fatigue and can easily lead to people ignoring ‘routine’ alerts because of frequency. 

**Identity and Access Management**

Employ user permissions via Policies by attaching them to IAM Groups rather than directly to individual users. Ensure only necessary users have CLI access along with password and key rotation policies.

**Compliance and Auditing**

Determine compliance standards and remain vigilant with AWS Config, AWS Audit Manager and CloudTrail. AWS Security Hub is also fantastic for centrally representing the overall security posture of your AWS account(s). Routinely audit your account(s) to maintain security compliance and proof for stakeholders.

**Automation**

Utilize AWS EventBridge and Lambda to automatically remediate certain security findings such as vulnerable security group ports. Simple Notification Service (SNS) is also a great tool for remaining vigilant with security events happening within your account. 

**Backups and Disaster Recovery**

Establish a strong backup policy for retention and frequencies with AWS Backup. Replicating backups to an additional AWS Region assists with improving Fault tolerance, but replicating backups to a dedicated AWS Account is a best practice should an entire account become compromised. Furthermore, based on desired RTO/RPO needs, it is imperative to conduct failover tests and restore jobs to your DR account to validate expectations are met and satisfied. 
Additionally, it is critical to develop a simple and well documented plan for a scenario of your data becoming compromised. Reviewing this procedure with staff and implementing the plan with vulnerability tests will ensure efficiency and highlight areas for improvement. 

**Vulnerability Tests**

AWS does allow degrees of penetration testing with pre-approval. Running scans and controlled/simulated attacks on your own environments can highlight any gaps or vulnerabilities in your solution. This is beneficial to put the ‘theory’ to actual tests, then learning and improving from the results. Soldiers do not just read field manuals and retain theory of battle tactics. They run simulations and war games with all kinds of variables to better understand what is most effective to reach victory on the battlefield. The same logic applies for your cloud security posture. 

**Shared Responsibility Model**

Ensure you understand what **YOU** as the customer of AWS are responsible for:

![Shared Responsibility Model](/shared-resp-model.jpg)

# Conclusion

Security requires an understanding of how bad actors may try to compromise your solutions, also explained as knowing your enemy. This enables us to counter those attack methods with purpose built solutions. Security is always changing and we must remain vigilant, constantly adapting to new tactics and strategies.  While there are many AWS security services, not all may be directly needed for your solution. This highlights the importance of asking yourself about components mentioned in the Design Considerations to determine what is needed and practical to fortify your “White House!” 

Finally, leveraging an AWS Partner like **Triumph Tech** can assist in achieving your desired security posture. Triumph can help your business by supplying instant support, design strategies and advice from trusted security experts and architects. Triumph Tech is a Premiere AWS Partner which highlights our level of expertise and AWS competence. If you would like to chat with our professionals about your security needs check us out!

Triumph Tech: [Triumph Tech](https://www.triumphtech.com/)


