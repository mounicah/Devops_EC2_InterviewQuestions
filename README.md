# Devops_EC2_InterviewQuestions
Descriptive Q&amp;As
Below are formal, interview‑ready answers to the AWS Account and EC2 questions you asked earlier. Each answer is concise, professional, and aligned with how cloud engineers respond in real interviews.

AWS ACCOUNT — FORMAL ANSWERS

1. What is an AWS account and why do companies use multiple accounts?

An AWS account is an isolated environment that contains its own resources, billing, identities, and security boundaries. Organizations use multiple accounts to achieve stronger isolation, enforce governance, separate workloads by environment (dev/test/prod), and simplify cost tracking through consolidated billing.

2. What is the root user and why should it never be used?

The root user is the original identity created with the AWS account and has unrestricted permissions. It should not be used for daily operations because it poses a significant security risk. Best practice is to secure it with MFA and use IAM roles or users for all operational tasks.

3. What is IAM and how do users, groups, and roles differ?

IAM (Identity and Access Management) is the service that controls authentication and authorization. Users represent individuals, groups are collections of users for permission management, and roles are temporary identities assumed by users or services to access resources without long‑term credentials.

4. What are IAM policies and how are they used?

IAM policies are JSON documents that define allowed or denied actions on AWS resources. They are attached to users, groups, or roles to enforce least‑privilege access and ensure controlled, auditable permissions.

5. What is AWS Organizations and how does it help manage multiple accounts?

AWS Organizations enables centralized management of multiple AWS accounts. It supports consolidated billing, automated account creation, and governance through Service Control Policies (SCPs), ensuring consistent security and compliance across the organization.

6. What is an SCP (Service Control Policy)?

An SCP is a policy applied at the organization or organizational unit level to define the maximum permissions that member accounts can have. SCPs act as guardrails and cannot grant permissions—only restrict them.

7. How do you secure an AWS account?

Account security is achieved through MFA on the root user, IAM least‑privilege access, CloudTrail logging, GuardDuty threat detection, Config compliance rules, strong password policies, and the use of IAM roles instead of static credentials.

8. How do you track costs across accounts?

Costs are tracked using Cost Explorer, AWS Budgets, cost allocation tags, and consolidated billing under AWS Organizations. These tools provide visibility into usage patterns and help enforce cost governance.

EC2 — FORMAL ANSWERS

9. What is Amazon EC2?

Amazon EC2 is a scalable compute service that provides virtual servers in the cloud. It allows users to run applications with flexible CPU, memory, storage, and networking configurations.

10. What are EC2 instance types?

Instance types are predefined configurations optimized for specific workloads, such as general purpose (t3, m6g), compute optimized (c6i), memory optimized (r6g), storage optimized (i3), and accelerated computing (p4, g5).

11. What is the difference between On‑Demand, Reserved, Spot, and Savings Plans?

On‑Demand instances are pay‑as‑you‑go. Reserved Instances provide discounted pricing for long‑term commitments. Spot Instances offer steep discounts but can be interrupted. Savings Plans provide flexible, commitment‑based discounts across compute services.

12. What is an AMI and how do you create one?

An Amazon Machine Image (AMI) is a template containing the OS, configuration, and software required to launch an EC2 instance. It is created by selecting an existing instance and generating an image through the EC2 console or API.

13. What is the difference between EBS and Instance Store?

EBS volumes are persistent block storage that remains intact after instance termination (unless configured otherwise). Instance Store provides ephemeral storage that is physically attached to the host and is lost when the instance stops or terminates.

14. What is an EBS volume and what types exist?

An EBS volume is durable block storage for EC2. Types include gp3 (general purpose), io1/io2 (provisioned IOPS), st1 (throughput optimized), and sc1 (cold HDD), each optimized for different performance requirements.

15. How do you attach, detach, and resize EBS volumes?

Volumes are attached or detached through the EC2 console or CLI. Resizing involves modifying the volume size and then extending the filesystem within the instance.

16. What is the difference between stopping, terminating, and rebooting an EC2 instance?

Stopping halts the instance while preserving the EBS root volume. Terminating permanently deletes the instance and may delete the root volume. Rebooting restarts the OS without affecting data or configuration.

17. What happens to the root EBS volume when an instance is terminated?

By default, the root EBS volume is deleted upon termination. This behavior can be modified by disabling the “Delete on Termination” flag.

18. What is user data and how is it used?

User data is a script executed at instance launch to automate configuration tasks such as installing software, applying updates, or configuring services.

19. How do you connect to an EC2 instance?

Linux instances are accessed via SSH using a key pair, while Windows instances use RDP with a decrypted administrator password. Alternatively, SSM Session Manager allows access without opening inbound ports.

20. What are security groups and how do they differ from NACLs?

Security groups are stateful, instance‑level firewalls that control inbound and outbound traffic. Network ACLs are stateless, subnet‑level firewalls that evaluate both inbound and outbound rules independently.

NETWORKING & TROUBLESHOOTING — FORMAL ANSWERS

21. What is a VPC and why does every EC2 instance run inside one?

A VPC (Virtual Private Cloud) is an isolated virtual network within AWS. EC2 instances run inside a VPC to ensure controlled networking, routing, and security boundaries.

22. What is the difference between a public and private subnet?

A public subnet has a route to an Internet Gateway, enabling direct internet access. A private subnet does not, and instances rely on NAT or internal networking.

23. How does an EC2 instance get internet access?

Instances in public subnets require a public IP and a route to an Internet Gateway. Instances in private subnets use a NAT Gateway for outbound internet access.

24. What is an Elastic IP and when should you use it?

An Elastic IP is a static public IPv4 address that remains associated with your account. It is used when a stable public endpoint is required, such as for bastion hosts.

25. How do you secure EC2 instances?

Security is achieved through security groups, IAM roles, OS patching, encrypted EBS volumes, restricted SSH access, and monitoring via CloudWatch and GuardDuty.

SCENARIO‑BASED — FORMAL ANSWERS

26. You cannot SSH into an EC2 instance — what do you check?

I verify the instance state, security group inbound rules, key pair correctness, route table configuration, NACL rules, and whether SSM is enabled as an alternative access method.

27. Your EC2 instance is running but the application is slow — what do you check?

I review CPU credits, memory usage, EBS IOPS, network throughput, application logs, and CloudWatch metrics to identify performance bottlenecks.

28. Your EC2 instance was terminated unexpectedly — what do you check?

I check Auto Scaling Group activity, Spot interruption notices, CloudTrail logs, and billing or service quota issues.

29. Your EBS volume is full — how do you fix it?

I expand the EBS volume, extend the filesystem inside the instance, and validate the new capacity.

30. You need zero‑downtime deployment for EC2 — what do you use?

I use an Auto Scaling Group with a Load Balancer and perform rolling updates or blue‑green deployments.

ARCHITECTURE — FORMAL ANSWERS

31. How do Auto Scaling Groups work with EC2?

ASGs automatically launch, terminate, and replace EC2 instances based on scaling policies, health checks, and demand patterns to maintain availability and performance.

32. How do you design a highly available EC2 architecture?

I distribute instances across multiple Availability Zones, use an Elastic Load Balancer, configure Auto Scaling, and ensure data redundancy through EBS snapshots or multi‑AZ storage.

33. How do you migrate on‑prem servers to EC2?

I use AWS Server Migration Service (SMS), Application Migration Service (MGN), or VM Import/Export to replicate and migrate workloads with minimal downtime.

34. How do you secure secrets on EC2?

I store secrets in AWS Secrets Manager or SSM Parameter Store and assign IAM roles to the instance to retrieve them securely without hard‑coded credentials.

35. How do you monitor EC2 instances?

I use CloudWatch metrics, logs, alarms, dashboards, and integrate with services like CloudTrail, GuardDuty, and AWS Config for full observability.

