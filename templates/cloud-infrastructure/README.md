# Cloud Infrastructure Templates

Network diagram templates for cloud-native architectures across AWS, Azure, GCP, and multi-cloud environments.

## Overview

This category contains templates for designing and documenting cloud infrastructure networking patterns. These templates help visualize virtual networks, subnets, gateways, and cloud-specific networking components.

## Templates in This Category

### AWS VPC with Public and Private Subnets
**File**: `aws-vpc-subnets.md`

A production-ready AWS VPC design with multi-AZ deployment, public subnets for internet-facing resources, and private subnets for backend services.

**Use Cases**:
- Three-tier web applications
- Microservices architecture
- Hybrid cloud connections
- Multi-region applications

**Key Components**: VPC, Internet Gateway, NAT Gateway, Public/Private Subnets, Route Tables, Multiple Availability Zones

---

## Common Cloud Networking Patterns

### High Availability
Cloud infrastructure templates emphasize multi-AZ (Availability Zone) deployments for redundancy and fault tolerance.

### Security Layers
- Network isolation through VPCs/VNets
- Public vs private subnet segregation
- NAT gateways for outbound-only internet access
- Security groups and network ACLs

### Scalability
Cloud templates support auto-scaling groups, load balancers, and elastic infrastructure that grows with demand.

### Cost Optimization
- Single vs multi-AZ NAT gateway strategies
- VPC endpoints to reduce data transfer costs
- Right-sizing subnet CIDR blocks

## Cloud Provider Resources

### AWS
- [VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [AWS Architecture Center](https://aws.amazon.com/architecture/)

### Azure
- [Virtual Network Documentation](https://docs.microsoft.com/en-us/azure/virtual-network/)
- [Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/)

### GCP
- [VPC Documentation](https://cloud.google.com/vpc/docs)
- [GCP Architecture Framework](https://cloud.google.com/architecture)

## Contributing

To add a new cloud infrastructure template:

1. Create a new `.md` file in this directory
2. Follow the template format in `../TEMPLATE-GUIDE.md`
3. Include YAML frontmatter with `category: cloud-infrastructure`
4. Use Mermaid diagrams to visualize the architecture
5. Document cloud-specific components and services
6. Include IaC examples (Terraform, CloudFormation, ARM templates)
7. Add the template to this README

## Suggested Templates to Add

- Azure Virtual Network with Application Gateway
- GCP VPC with Cloud NAT
- Multi-cloud networking with Transit Gateway
- AWS EKS cluster networking
- Azure AKS networking
- Serverless architecture networking (Lambda, API Gateway)
- Cloud CDN integration patterns
