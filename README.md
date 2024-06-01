# Lab11

Part 1: Designing Cloud Infrastructure
Task:
  Design a cloud infrastructure for a scalable web application.
  Include components like compute instances, storage, and network configurations.
  Use AWS EC2, S3, and VPC to build the basic architecture.

<img width="1005" alt="image" src="https://github.com/KarlaPR10/Lab11/assets/138635602/d5038548-c74d-40ad-b854-1d2d514e2f43">

Part 2: IAM Configuration
Task:
  Define IAM roles and policies for different components of the architecture, such as developers, admins, and application servers.
  Ensure that each role adheres to the principle of least privilege.

    Developers
    
    Role: Developer
    Permissions:
    Read-only access to project resources (e.g., code, configurations)
    Ability to create and manage issues in issue tracking systems
    Limited access to deployment and release management tools
    Policy: developer-policy
    iam.roles/Developer: roles/Viewer, roles/Editor
    iam.permissions/Developer: storage.objects.list, storage.objects.get, storage.objects.create, storage.objects.update, storage.objects.delete
    iam.permissions/Developer: issues.create, issues.update, issues.delete
    Admins
    
    Role: Admin
    Permissions:
    Full access to project resources (e.g., code, configurations, infrastructure)
    Ability to manage users, groups, and roles
    Ability to manage deployment and release management tools
    Ability to manage security and compliance settings
    Policy: admin-policy
    iam.roles/Admin: roles/Owner, roles/Editor, roles/Viewer
    iam.permissions/Admin: iam.roles.create, iam.roles.update, iam.roles.delete, iam.permissions.create, iam.permissions.update, iam.permissions.delete
    iam.permissions/Admin: storage.objects.list, storage.objects.get, storage.objects.create, storage.objects.update, storage.objects.delete, storage.buckets.list, storage.buckets.get, storage.buckets.create, storage.buckets.update, storage.buckets.delete
    Application Servers
    
    Role: Application Server
    Permissions:
    Ability to read and write to application data stores
    Ability to execute application code and scripts
    Ability to access and use application-specific APIs
    Policy: app-server-policy
    iam.roles/Application Server: roles/Editor
    iam.permissions/Application Server: storage.objects.list, storage.objects.get, storage.objects.create, storage.objects.update, storage.objects.delete, storage.buckets.list, storage.buckets.get, storage.buckets.create, storage.buckets.update, storage.buckets.delete, app-specific-apis.read, app-specific-apis.write

Part 3: Resource Management Strategy
Task:
Develop a strategy for managing resources that includes auto-scaling, load balancing, and cost optimization using AWS Auto Scaling, ELB, and AWS Budgets.

    Auto-Scaling Strategy:
    
    Define Scaling Plans: Create scaling plans for each resource type (e.g., EC2 instances, RDS instances, and ElastiCache nodes) based on usage patterns, peak demand, and cost considerations.
    Choose Scaling Strategies: Select the most suitable scaling strategy for each resource type, such as:
    Optimize for Availability: Scale out to maintain resource utilization at 40%.
    Balance Availability and Cost: Scale out to maintain resource utilization at 50%.
    Optimize for Cost: Scale out to maintain resource utilization at 70%.
    Configure Scaling Policies: Set up scaling policies for each resource type, including:
    Scale-in and scale-out triggers based on CPU utilization, memory usage, or custom metrics.
    Define scaling cooldown periods to prevent rapid scaling fluctuations.
    Monitor and Adjust: Continuously monitor resource utilization and adjust scaling policies as needed to ensure optimal performance and cost-effectiveness.
    Load Balancing Strategy:
    
    Choose Load Balancer Type: Select the most suitable load balancer type based on application requirements, such as:
    Application Load Balancer (ALB) for HTTP/HTTPS traffic.
    Network Load Balancer (NLB) for TCP traffic.
    Gateway Load Balancer (GLB) for hybrid cloud and on-premises resources.
    Configure Load Balancer: Set up the load balancer with:
    Target groups for EC2 instances, containers, or IP addresses.
    Health checks to monitor instance health and detect issues.
    Session persistence to ensure sticky sessions.
    Route Traffic: Configure routing rules to direct traffic to the load balancer and distribute it across instances.
    Cost Optimization Strategy:
    
    Set Budgets: Establish budgets for each resource type and service using AWS Budgets.
    Track and Monitor: Track and monitor budget usage and adjust scaling policies as needed to stay within budget.
    Right-Size Resources: Right-size resources to match demand and avoid over-provisioning.
    Use Reserved Instances: Consider using reserved instances for long-term commitments to reduce costs.
    Additional Recommendations:
    
    Use CloudWatch Alarms: Set up CloudWatch alarms to trigger scaling activities and notify teams of issues.
    Implement Auto-Scaling with ELB: Integrate Auto Scaling with ELB to ensure seamless scaling and load balancing.
    Monitor and Analyze: Continuously monitor and analyze resource utilization, scaling activities, and costs to refine the strategy and optimize performance and cost-effectiveness.
    By following this strategy, we can ensure optimal resource utilization, scalability, and cost-effectiveness for our application using AWS Auto Scaling, ELB, and AWS Budgets.

Part 4: Theoretical Implementation
Using the AWS services identified, outline the architecture for the web application. Describe how each component interacts with others, focusing on the flow of data and control between services. This description should detail the role of each service in the architecture, ensuring a clear understanding of their interactions and dependencies.

      The APIs are accessed through public IPs defined in the ELB
    The ELB is responsible for balancing and sending requests to the EC2 according to the available load.
    The EC2 contains the web components responsible for the API's own operations, such as accessing S3 for readings or writing, accessing RDS databases for reading and writing.
    S3 is responsible for storing our required files in the APIs.
    RDS is responsible for managing the databases required in the APIs.
    VPC is responsible for controlling network access to the infrastructure.

Part 5: Discussion and Evaluation
Discussion Points:
Explain the choice of services and how they interact to provide a resilient and secure infrastructure.
Discuss how the designed IAM policies contribute to overall security.
Review the resource management strategy to ensure it meets the scalability and cost-efficiency needs.


    This design provides a scalable cloud infrastructure for a web application using AWS EC2, S3, and VPC. It includes compute instances for web, application, and database servers, as well as storage for static content, database data, and backups. The network configurations include a VPC, subnets, security groups, and Route 53 for domain routing. Load balancing is achieved using ELB and HAProxy, and scalability is ensured through Auto Scaling and database scaling. Monitoring and logging are handled through CloudWatch, CloudTrail, and ELB logs.
