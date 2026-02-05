# Hybrid Network Templates

Network diagram templates for hybrid architectures combining on-premise infrastructure with cloud services, and multi-cloud deployments.

## Overview

This category contains templates for designing hybrid network architectures that bridge on-premise data centers with cloud environments, or connect multiple cloud providers. These patterns are essential for enterprise migrations, multi-cloud strategies, and distributed systems.

## Templates in This Category

### Hub and Spoke Network Topology
**File**: `hub-and-spoke.md`

A centralized network architecture with a hub (central point) connected to multiple spoke networks, enabling efficient inter-spoke communication through the hub.

**Use Cases**:
- Multi-environment isolation (prod, dev, test)
- Partner network integration
- Hybrid cloud architecture
- Centralized security services
- Shared services hub

**Key Components**: Hub network, spoke networks, on-premise connection, internet gateway, VNet peering/Transit Gateway

---

## Common Hybrid Networking Patterns

### Connectivity Options

#### VPN Connections
- Site-to-site VPN for secure encrypted tunnels
- Lower cost, uses internet connectivity
- Suitable for non-critical workloads

#### Dedicated Connections
- AWS Direct Connect
- Azure ExpressRoute
- GCP Cloud Interconnect
- Higher bandwidth, lower latency, more reliable
- Required for mission-critical workloads

### Architecture Patterns

#### Hub and Spoke
Central hub for shared services and security, with isolated spoke networks for different applications or environments.

#### Multi-Cloud
Connect workloads across AWS, Azure, and GCP with unified networking and routing.

#### Cloud Bursting
On-premise primary infrastructure with cloud overflow capacity for peak demand.

#### Migration Patterns
Gradual migration from on-premise to cloud with parallel operation during transition.

## Hybrid Networking Considerations

### Latency
- Geographic proximity between on-premise and cloud regions
- Network path optimization
- Edge caching strategies

### Bandwidth
- Right-sizing connections for workload requirements
- Bandwidth costs and usage patterns
- Burst capacity planning

### Security
- Encryption for data in transit
- Network segmentation across environments
- Unified security policies
- Identity federation (SSO, SAML, OAuth)

### Routing
- BGP for dynamic routing
- Static routes for simple scenarios
- Route prioritization and failover

### DNS & Name Resolution
- Hybrid DNS solutions
- Private DNS zones
- DNS forwarding between environments

## Use Cases

### Cloud Migration
- Phased migration strategies
- Parallel running during transition
- Gradual workload shifting

### Disaster Recovery
- Cloud as DR site for on-premise workloads
- Backup and restore patterns
- Failover and failback procedures

### Data Residency
- Keep sensitive data on-premise
- Process data in cloud
- Comply with regional data regulations

### Burst Capacity
- On-premise for baseline load
- Cloud for peak/seasonal demand
- Cost optimization

## Technology References

### AWS Hybrid
- [AWS Direct Connect](https://aws.amazon.com/directconnect/)
- [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/)
- [AWS VPN](https://aws.amazon.com/vpn/)

### Azure Hybrid
- [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/)
- [Azure VPN Gateway](https://azure.microsoft.com/en-us/services/vpn-gateway/)
- [Azure Virtual WAN](https://azure.microsoft.com/en-us/services/virtual-wan/)

### GCP Hybrid
- [Cloud Interconnect](https://cloud.google.com/network-connectivity/docs/interconnect)
- [Cloud VPN](https://cloud.google.com/network-connectivity/docs/vpn)
- [Network Connectivity Center](https://cloud.google.com/network-connectivity-center)

## Contributing

To add a new hybrid template:

1. Create a new `.md` file in this directory
2. Follow the template format in `../TEMPLATE-GUIDE.md`
3. Include YAML frontmatter with `category: hybrid`
4. Show both on-premise and cloud components
5. Document connectivity methods (VPN, Direct Connect, etc.)
6. Include routing and failover considerations
7. Add the template to this README

## Suggested Templates to Add

- Site-to-site VPN connection (AWS/Azure/GCP)
- AWS Direct Connect with Transit Gateway
- Azure ExpressRoute with Virtual WAN
- Multi-cloud mesh networking
- Hybrid Active Directory integration
- Cloud DR site for on-premise workloads
- Multi-region hybrid deployment
- SD-WAN integration with cloud
