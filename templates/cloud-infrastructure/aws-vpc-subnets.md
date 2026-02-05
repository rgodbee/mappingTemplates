---
title: AWS VPC with Public and Private Subnets
description: A standard AWS VPC architecture with public and private subnets across multiple availability zones, including internet gateway, NAT gateway, and route tables
category: cloud-infrastructure
tags: [aws, vpc, subnets, cloud, networking, availability-zones, high-availability]
author: Network Templates
---

# AWS VPC with Public and Private Subnets

A production-ready AWS VPC design with multi-AZ deployment, public subnets for internet-facing resources, and private subnets for backend services. This architecture provides high availability, security, and scalability.

## Diagram

```mermaid
graph TD
    Internet[Internet]
    IGW[Internet Gateway]

    VPC[AWS VPC<br/>10.0.0.0/16<br/>us-east-1]

    subgraph AZ1[Availability Zone 1a]
        PubSub1[Public Subnet 1<br/>10.0.1.0/24]
        PrivSub1[Private Subnet 1<br/>10.0.11.0/24]
        NAT1[NAT Gateway 1]
    end

    subgraph AZ2[Availability Zone 1b]
        PubSub2[Public Subnet 2<br/>10.0.2.0/24]
        PrivSub2[Private Subnet 2<br/>10.0.12.0/24]
        NAT2[NAT Gateway 2]
    end

    subgraph AZ3[Availability Zone 1c]
        PubSub3[Public Subnet 3<br/>10.0.3.0/24]
        PrivSub3[Private Subnet 3<br/>10.0.13.0/24]
        NAT3[NAT Gateway 3]
    end

    RT_Pub[Public Route Table<br/>0.0.0.0/0 -> IGW]
    RT_Priv1[Private Route Table 1<br/>0.0.0.0/0 -> NAT1]
    RT_Priv2[Private Route Table 2<br/>0.0.0.0/0 -> NAT2]
    RT_Priv3[Private Route Table 3<br/>0.0.0.0/0 -> NAT3]

    Internet <--> IGW
    IGW <--> VPC

    VPC --> AZ1
    VPC --> AZ2
    VPC --> AZ3

    IGW <--> PubSub1
    IGW <--> PubSub2
    IGW <--> PubSub3

    PubSub1 --> NAT1
    PubSub2 --> NAT2
    PubSub3 --> NAT3

    NAT1 --> PrivSub1
    NAT2 --> PrivSub2
    NAT3 --> PrivSub3

    RT_Pub -.->|associated| PubSub1
    RT_Pub -.->|associated| PubSub2
    RT_Pub -.->|associated| PubSub3

    RT_Priv1 -.->|associated| PrivSub1
    RT_Priv2 -.->|associated| PrivSub2
    RT_Priv3 -.->|associated| PrivSub3

    style VPC fill:#FF9900,stroke:#EC7211,stroke-width:3px,color:#fff
    style AZ1 fill:#E8F4F8,stroke:#00A4A6,stroke-width:2px
    style AZ2 fill:#E8F4F8,stroke:#00A4A6,stroke-width:2px
    style AZ3 fill:#E8F4F8,stroke:#00A4A6,stroke-width:2px
    style PubSub1 fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style PubSub2 fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style PubSub3 fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style PrivSub1 fill:#4A90E2,stroke:#2E5C8A,stroke-width:2px,color:#fff
    style PrivSub2 fill:#4A90E2,stroke:#2E5C8A,stroke-width:2px,color:#fff
    style PrivSub3 fill:#4A90E2,stroke:#2E5C8A,stroke-width:2px,color:#fff
    style IGW fill:#F5A623,stroke:#C77F1B,stroke-width:2px
    style NAT1 fill:#BD10E0,stroke:#9012FE,stroke-width:2px,color:#fff
    style NAT2 fill:#BD10E0,stroke:#9012FE,stroke-width:2px,color:#fff
    style NAT3 fill:#BD10E0,stroke:#9012FE,stroke-width:2px,color:#fff
    style Internet fill:#D0021B,stroke:#A00116,stroke-width:2px,color:#fff
```

## Detailed Component View

```mermaid
graph LR
    subgraph Public_Resources[Public Subnet Resources]
        ALB[Application Load Balancer]
        Bastion[Bastion Host]
        NAT_GW[NAT Gateway]
    end

    subgraph Private_Resources[Private Subnet Resources]
        Web[Web Servers<br/>Auto Scaling Group]
        App[Application Servers<br/>Auto Scaling Group]
        Cache[ElastiCache Redis]
    end

    subgraph Data_Layer[Data Subnet Resources]
        RDS[RDS Database<br/>Multi-AZ]
    end

    Internet[Internet] --> ALB
    Bastion --> Web
    Bastion --> App
    NAT_GW --> Internet

    ALB --> Web
    Web --> App
    Web --> NAT_GW
    App --> Cache
    App --> RDS
    App --> NAT_GW

    style Public_Resources fill:#E8F4F8,stroke:#00A4A6,stroke-width:2px
    style Private_Resources fill:#F0F0F0,stroke:#888,stroke-width:2px
    style Data_Layer fill:#FFE8E8,stroke:#CC0000,stroke-width:2px
    style ALB fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style Bastion fill:#F5A623,stroke:#C77F1B,stroke-width:2px
    style NAT_GW fill:#BD10E0,stroke:#9012FE,stroke-width:2px,color:#fff
    style Web fill:#4A90E2,stroke:#2E5C8A,stroke-width:2px,color:#fff
    style App fill:#4A90E2,stroke:#2E5C8A,stroke-width:2px,color:#fff
    style Cache fill:#50E3C2,stroke:#00D4B4,stroke-width:2px
    style RDS fill:#D0021B,stroke:#A00116,stroke-width:2px,color:#fff
```

## How to Use

1. **Copy this template** to create your VPC architecture
2. **Customize the VPC CIDR block**:
   - Choose an appropriate CIDR range (e.g., `10.0.0.0/16`)
   - Ensure it doesn't overlap with other VPCs or on-premise networks
3. **Define subnet ranges**:
   - Public subnets: Use smaller CIDR blocks (e.g., `/24` gives 256 IPs)
   - Private subnets: Allocate larger ranges for more instances
   - Leave room for future subnet additions
4. **Select availability zones**:
   - Use at least 2 AZs for high availability
   - Add 3 AZs for production workloads
   - Adjust based on your region's available AZs
5. **Configure NAT Gateway strategy**:
   - **High Availability**: One NAT Gateway per AZ (higher cost)
   - **Cost Optimized**: Single NAT Gateway in one AZ
   - **Hybrid**: NAT Gateway in 2 AZs for balance
6. **Add security layers**:
   - Configure Security Groups for each tier
   - Set up Network ACLs for subnet-level filtering
   - Implement VPC Flow Logs for monitoring

## Example Use Cases

### Three-Tier Web Application
Deploy a classic web application with load balancers in public subnets, application servers in private subnets, and databases in isolated data subnets.

### Microservices Architecture
Run containers (ECS/EKS) in private subnets with Application Load Balancer in public subnets for ingress traffic.

### Hybrid Cloud Connection
Connect this VPC to on-premise data centers using VPN or AWS Direct Connect through a Virtual Private Gateway.

### Multi-Region Application
Replicate this VPC architecture in multiple regions with VPC peering or Transit Gateway for global applications.

### Development/Staging Environment
Create a smaller version of this architecture for non-production environments with fewer AZs and resources.

## Customization Points

- **VPC CIDR**: Change `10.0.0.0/16` to your preferred address range
- **Region**: Replace `us-east-1` with your target AWS region
- **Availability Zones**: Adjust number of AZs (2 minimum, 3 recommended)
- **Subnet Sizing**: Modify CIDR blocks based on expected instance count
- **NAT Gateway**: Choose HA vs cost-optimized NAT strategy
- **Additional Subnets**: Add database subnets, DMZ, or dedicated subnets for specific services
- **VPN/Direct Connect**: Add Virtual Private Gateway for hybrid connectivity

## Architecture Components

### VPC (Virtual Private Cloud)
The logical isolation of your AWS resources with a defined CIDR block.

### Internet Gateway
Enables communication between VPC and the internet for public subnets.

### NAT Gateway
Allows instances in private subnets to access the internet for updates and patches while remaining private.

### Public Subnets
- Have routes to Internet Gateway
- Host internet-facing resources (load balancers, bastion hosts)
- Instances get public IP addresses

### Private Subnets
- Route internet traffic through NAT Gateway
- Host application servers, compute resources
- Instances only have private IP addresses
- Protected from direct internet access

### Route Tables
- Public Route Table: Routes `0.0.0.0/0` to Internet Gateway
- Private Route Tables: Routes `0.0.0.0/0` to NAT Gateway (per AZ)

## Cost Considerations

### NAT Gateway Costs
- **Per Hour**: ~$0.045 per hour per NAT Gateway
- **Data Processing**: ~$0.045 per GB processed
- **Multi-AZ**: 3 NAT Gateways = ~$97/month + data transfer

### Cost Optimization Options
1. **Single NAT Gateway**: Use one NAT in a single AZ (lower HA)
2. **NAT Instance**: Use EC2 NAT instance instead (more management)
3. **VPC Endpoints**: Use for AWS services (S3, DynamoDB) to avoid NAT costs
4. **PrivateLink**: Direct access to AWS services without internet

## Security Best Practices

### Network Segmentation
- Separate public and private resources
- Use separate subnets for different tiers (web, app, data)
- Implement least privilege access

### Security Groups
- Stateful firewall at instance level
- Only open required ports
- Use security group references instead of CIDR blocks

### Network ACLs
- Stateless firewall at subnet level
- Add an additional layer of defense
- Consider default deny rules

### Flow Logs
- Enable VPC Flow Logs for traffic analysis
- Store logs in CloudWatch or S3
- Monitor for unusual patterns

### Encryption
- Use TLS/SSL for data in transit
- Enable encryption at rest for storage
- Use AWS PrivateLink for service communication

## Terraform Example

```hcl
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name = "main-vpc"
  }
}

resource "aws_subnet" "public" {
  count                   = 3
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.${count.index + 1}.0/24"
  availability_zone       = data.aws_availability_zones.available.names[count.index]
  map_public_ip_on_launch = true

  tags = {
    Name = "public-subnet-${count.index + 1}"
  }
}

resource "aws_subnet" "private" {
  count             = 3
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.${count.index + 11}.0/24"
  availability_zone = data.aws_availability_zones.available.names[count.index]

  tags = {
    Name = "private-subnet-${count.index + 1}"
  }
}
```

## CloudFormation Example

```yaml
Resources:
  VPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsHostnames: true
      EnableDnsSupport: true
      Tags:
        - Key: Name
          Value: main-vpc
```
