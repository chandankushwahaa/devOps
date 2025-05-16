# AWS  CLOUD
Content
1. [Virtualization](#virtualization)
2. [Cloud Computing](#cloudcomputing)
3. [AWS](#aws)
4. []()

 ## 1. Virtualization
Virtualization is a technology that allows you to create virtual versions of computing resources, such as: Servers, Desktops, Networks, etc.

- **Virtual Machine** : A virtual machine runs as a guest on a physical machine, known as the **host**. A piece of software called a **hypervisor** manages the allocation of the host's physical resources (CPU, RAM, storage, network) to one or more virtual machines. Each VM is isolated from the host operating system and other VMs, providing a secure and independent computing environment.
- Types of hypervisor:- 
	- **Type1 (Bare-Metal Hypervisors or Native Hypervisors)** :  These hypervisors run directly on the host's physical hardware, without an underlying operating system. They act as a lightweight operating system themselves, specifically designed for virtualization
		- *e.g - VMware vSphere/ESXi, Xen, Red Hat Virtualization (RHV)*
	- **Type2 (Hosted Hypervisors)** : These hypervisors run as an application on top of a traditional operating system (the host OS). The hypervisor relies on the host OS to access and manage the underlying hardware.
		- *e.g -Oracle Virtual Box, VMware*

## 2. CloudComputing
Cloud computing refers to the delivery of computing services—including servers, storage, databases, networking, software, analytics, and intelligence—over the internet ("the cloud"). Instead of owning and maintaining your own physical data centers and servers, you access these resources on demand from a cloud provider. You typically pay only for the services you use, helping to lower costs, improve efficiency, and offer greater flexibility.
- *e.g - AWS, Azure, GCP, IBM cloud, DigitalOcean, VMware*

### **Types of Cloud Deployment Models:**

-   **Public Cloud:** Owned and operated by a third-party cloud service provider, Resources are available to the public over the internet.
	- e.g- AWS, Microsoft Azure, GCP. 
-   **Private Cloud:** Infrastructure is provisioned for exclusive use by a single organization. It can be located on the organization's premises or hosted by a third-party provider. Offers greater control and security but can be more expensive.
-   **Hybrid Cloud:** A composition of two or more distinct cloud infrastructures (public, private, or community) that remain unique entities but are bound together by technology that enables data and application portability. Offers flexibility and more deployment options.
-   **Community Cloud:** The cloud infrastructure is provisioned for exclusive use by a specific community of consumers from organizations that have shared concerns.
	- e.g- mission, security requirements, policy, and compliance considerations.
    

### **Types of Cloud Service Models:**
These models represent different layers of the cloud "stack".

-   **Infrastructure as a Service (IaaS):** Provides access to fundamental computing resources like virtual machines, storage, and networks. The user manages the operating system, middleware, and applications. 
	- e.g- AWS EC2, Azure Virtual Machines, and Google Compute Engine.
    
-   **Platform as a Service (PaaS):** Provides a platform allowing customers to develop, run, and manage applications without the complexity of managing the underlying infrastructure. Includes operating systems, programming language execution environment, database systems, and web servers. 
	- e.g- AWS Elastic Beanstalk, Azure App Service, and Google App Engine.
    
-   **Software as a Service (SaaS):** Delivers software applications over the internet, on demand, typically on a subscription basis. Users access the software through a web browser or a dedicated client application without managing the underlying infrastructure, operating systems, etc. 
	- e.g- Gmail, Salesforce, Dropbox, and Microsoft 365.
-   **Serverless Computing (Function as a Service - FaaS):** Allows developers to run code without provisioning or managing servers. The cloud provider automatically allocates and manages the compute resources needed to run the code. Users are typically billed based on the number of executions and the resources consumed by the code. 
	- e.g- Cloudflare, AWS Lambda, Azure Functions, and Google Cloud Functions.

## 3. AWS
**AWS (Amazon Web Services)** is a comprehensive and widely adopted cloud platform offered by Amazon. It provides a vast array of on-demand cloud computing services to individuals, businesses, and governments globally. Instead of owning and maintaining physical servers and data centers, users can access a wide range of services over the internet on a pay-as-you-go basis. AWS was launched in 2006 as the first public cloud platform.
**Popular Services Provided by AWS:-**
- **EC2** for scalable compute capacity.
- **S3** for highly reliable storage
- **RDS** for managed databases
- **Lambda** for serverless computing
- **CloudFront** for content delivery.
## 4. IAM (Identity & Access Management)
IAM is a service that helps you securely control access to AWS resources. It allows you to manage users, roles and permissions to define who can access what within your AWS environment.
- **Free Service**: IAM is offered at no additional cost.
- Global Service
- Root account, created by default, shouldn't be used or shared.
> Better don't use root user create a new user and use it.
1. Create User
2. Assign Permissions
3. Create Groups
4. Create Roles
5. Define Policies
6. Manage Federated Access 

## 5. EC2 (Elastic Compute Cloud)
It is a cloud service that provides resizable virtual servers, called instances, which you can use to run applications.