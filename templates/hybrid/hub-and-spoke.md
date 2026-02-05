---
title: Hub and Spoke Network Topology
description: A centralized network architecture with a hub (central point) connected to multiple spoke networks, enabling efficient inter-spoke communication through the hub
category: hybrid
tags: [hub-and-spoke, network-topology, cloud, azure, aws, enterprise]
author: Network Templates
---

# Hub and Spoke Network Topology

The hub and spoke topology is a network architecture pattern where a central hub network is connected to multiple spoke networks. All inter-spoke traffic flows through the hub, which provides centralized control, security, and shared services.

## Diagram

```mermaid
graph TD
    Hub[Hub Network<br/>10.0.0.0/16<br/>Shared Services]

    Spoke1[Spoke 1<br/>Production<br/>10.1.0.0/16]
    Spoke2[Spoke 2<br/>Development<br/>10.2.0.0/16]
    Spoke3[Spoke 3<br/>Testing<br/>10.3.0.0/16]
    Spoke4[Spoke 4<br/>Partner Network<br/>10.4.0.0/16]

    OnPrem[On-Premise<br/>Data Center<br/>192.168.0.0/16]
    Internet[Internet]

    Hub <--> Spoke1
    Hub <--> Spoke2
    Hub <--> Spoke3
    Hub <--> Spoke4

    Hub <--> OnPrem
    Hub <--> Internet

    style Hub fill:#4A90E2,stroke:#2E5C8A,stroke-width:3px,color:#fff
    style Spoke1 fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style Spoke2 fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style Spoke3 fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style Spoke4 fill:#7ED321,stroke:#5FA319,stroke-width:2px
    style OnPrem fill:#F5A623,stroke:#C77F1B,stroke-width:2px
    style Internet fill:#D0021B,stroke:#A00116,stroke-width:2px
```

## How to Use

1. **Copy this template** to create your own hub and spoke architecture
2. **Customize the hub network**:
   - Update the CIDR block (e.g., `10.0.0.0/16`)
   - Add shared services (DNS, monitoring, security, etc.)
3. **Define your spoke networks**:
   - Rename spokes based on your environment names
   - Update CIDR blocks to match your IP addressing scheme
   - Add or remove spokes as needed
4. **Configure connections**:
   - Add VPN/Express Route connections for on-premise
   - Configure NAT Gateway or Internet Gateway for internet access
   - Set up VNet peering (Azure) or Transit Gateway (AWS)
5. **Apply network policies**:
   - Define routing rules for inter-spoke communication
   - Implement security groups/NSGs at hub and spoke levels
   - Configure firewall rules at the hub

## Example Use Cases

### Multi-Environment Isolation
Separate production, development, and testing environments into different spokes while maintaining centralized security and monitoring in the hub.

### Partner Network Integration
Connect partner or vendor networks as isolated spokes with controlled access to specific hub resources.

### Hybrid Cloud Architecture
Connect on-premise data centers to cloud environments through the hub, enabling gradual cloud migration while maintaining connectivity.

### Centralized Security Services
Deploy firewalls, intrusion detection systems, and security monitoring in the hub to protect all spoke networks.

### Shared Services Hub
Host shared services (Active Directory, DNS, NTP, monitoring) in the hub that all spokes can access without exposing them to each other.

## Customization Points

- **Hub Network**: Replace with your hub VNet/VPC name and CIDR
- **Spoke Networks**: Add, remove, or rename spokes based on your requirements
- **On-Premise Connection**: Adjust or remove if not using hybrid connectivity
- **Internet Gateway**: Customize based on internet access requirements
- **CIDR Blocks**: Update all IP address ranges to match your addressing scheme
- **Styling**: Modify colors to match your architecture diagram standards

## Architecture Considerations

### Advantages
- Centralized management and security
- Simplified network design
- Easier to implement network policies
- Cost-effective for shared services
- Scalable by adding more spokes

### Trade-offs
- Hub becomes a single point of failure (mitigate with redundancy)
- Additional latency for inter-spoke communication
- Hub bandwidth limitations may affect performance
- More complex routing configuration

## Implementation Notes

### Azure
Use VNet Peering to connect spokes to hub, with Azure Firewall or NVA in the hub for traffic inspection.

### AWS
Use AWS Transit Gateway to connect VPCs in a hub and spoke pattern, with centralized routing and security.

### Multi-Region
For multi-region deployments, consider a regional hub in each region with inter-hub connectivity.
