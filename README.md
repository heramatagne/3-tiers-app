# 3-tiers-app
This Git repository contains CloudFormation templates for deploying a scalable and resilient 3-tier web application on Amazon Web Services (AWS). The architecture follows best practices for a three-tiered application, including networking components, compute resources, and a database layer.

# Templates

**Networking**
- p1-network.yml

**Compute**
- p1-app-.yml
  
**IAM role**
- p1-ssm-session-manager.yml
  
**database**
- p1-db.yml

# Tier Description

- **Networking Tier**: Defines a Virtual Private Cloud (VPC), subnets, route tables, and security groups to establish a secure and isolated network environment for the application.
- **Compute Tier**: Includes template for deploying EC2 instances, an auto-scaling group, and load balancers to handle web traffic efficiently. Implements scalability and fault tolerance for the compute layer.
- **Database Tier**: Defines a multi-AZ Mysql database to manage the application's database, providing a scalable and managed relational database solution.
