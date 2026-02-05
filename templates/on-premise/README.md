# On-Premise Network Templates

Network diagram templates for traditional on-premise data center architectures, enterprise networks, and physical infrastructure.

## Overview

This category contains templates for designing on-premise network architectures including data center networks, enterprise campus networks, and traditional IT infrastructure. These patterns are relevant for organizations with physical data centers, colocation facilities, and legacy infrastructure.

## Templates in This Category

Currently, this category is ready for templates. Suggested templates to add are listed below.

---

## On-Premise Network Patterns

### Data Center Architecture

#### Three-Tier Network
Traditional data center design with three layers:
- **Core Layer**: High-speed backbone, redundant switches
- **Aggregation/Distribution Layer**: Policy enforcement, routing between VLANs
- **Access Layer**: End-device connectivity, servers, storage

#### Spine-Leaf Architecture
Modern data center design for east-west traffic:
- **Spine Switches**: High-capacity backbone
- **Leaf Switches**: Connect to servers and storage
- Equal path cost to any leaf from any spine
- Scalable and predictable performance

#### Collapsed Core
Simplified design combining core and distribution:
- Suitable for smaller data centers
- Reduced complexity and cost
- Core switches perform distribution functions

### Enterprise Campus Networks

#### Building Distribution
- Core switches at main distribution facility
- Building switches connected to core
- Access switches on each floor
- Wireless access points
- VoIP infrastructure

#### Departmental Segmentation
- VLANs for different departments
- Security policies between segments
- Quality of Service (QoS) for voice/video
- Guest network isolation

### Storage Networks

#### Fibre Channel SAN
- Dedicated storage network
- High-speed, low-latency
- Block-level storage access
- Redundant fabric

#### iSCSI SAN
- Storage over IP networks
- Lower cost than Fibre Channel
- Uses existing Ethernet infrastructure
- VLAN separation from other traffic

#### NAS
- File-level storage access
- NFS or SMB/CIFS protocols
- Dedicated or shared network

## Network Components

### Core Infrastructure

#### Core Switches
- Highest performance switches
- Redundant for high availability
- Minimal processing (fast forwarding)
- Support for routing protocols (OSPF, BGP)

#### Distribution/Aggregation Switches
- Layer 3 routing between VLANs
- Policy enforcement (ACLs)
- Load balancing
- Connect access layer to core

#### Access Switches
- Layer 2 switching
- PoE for phones and wireless APs
- Port security
- VLAN assignment

### Connectivity

#### Routers
- Border routers for internet connectivity
- Internal routers for complex routing
- VPN concentrators
- BGP for external routing

#### Firewalls
- Perimeter security
- DMZ segmentation
- Internal segmentation
- VPN termination

#### Load Balancers
- Application load balancing
- SSL offloading
- Health checking
- Session persistence

### Wireless Infrastructure

#### Wireless Controllers
- Centralized AP management
- Roaming support
- Security policies
- Guest portal

#### Access Points
- Indoor and outdoor APs
- Coverage planning
- Channel assignment
- Band steering (2.4 GHz / 5 GHz)

## High Availability Patterns

### Redundancy
- Dual power supplies
- Redundant switches and routers
- Multiple uplinks
- Redundant internet connections

### Protocols
- **VRRP/HSRP**: First-hop redundancy
- **STP/RSTP**: Loop prevention
- **LACP**: Link aggregation
- **MLAG/vPC**: Multi-chassis link aggregation

### Design Principles
- No single point of failure
- Automatic failover
- Geographic redundancy
- Regular failover testing

## Network Services

### DHCP
- IP address assignment
- DHCP relay for distributed networks
- Reservation for servers
- DHCP failover/redundancy

### DNS
- Internal DNS for name resolution
- Split-horizon DNS (internal/external)
- Active Directory integration
- DNS redundancy

### NTP
- Time synchronization
- Stratum hierarchy
- Redundant NTP servers
- Internal time sources

### Authentication
- RADIUS/TACACS+ for network device authentication
- 802.1X for port-based authentication
- Active Directory integration
- Certificate management

## Network Segmentation

### VLANs
- Logical segmentation
- Broadcast domain isolation
- Security boundaries
- Performance optimization

### Subnets
- IP address organization
- Routing boundaries
- ACL application points
- DHCP scopes

### Zones
- DMZ for public services
- Internal network for users
- Server network for infrastructure
- Management network for devices
- Guest network for visitors

## Physical Infrastructure

### Cabling
- Cat 6/6a for 1/10 Gbps Ethernet
- Fiber for long distances and high speeds
- Cable management and labeling
- Structured cabling standards

### Racks and Cabinets
- 42U standard racks
- Cable management
- Power distribution (PDUs)
- Cooling considerations

### Environmental
- Redundant power (A/B feeds)
- UPS for power protection
- Cooling systems (CRAC/CRAH)
- Environmental monitoring

## Security Considerations

### Network Access Control
- 802.1X authentication
- MAC address filtering
- Port security
- DHCP snooping

### Segmentation
- Firewall between zones
- ACLs on routers and switches
- Private VLANs
- Micro-segmentation

### Monitoring
- Network flow analysis (NetFlow)
- Intrusion detection (IDS)
- Log aggregation (Syslog)
- SNMP monitoring

## Best Practices

### Design
- Capacity planning
- Scalability considerations
- Future growth accommodation
- Technology refresh cycles

### Documentation
- Network diagrams
- IP address management (IPAM)
- Device configurations
- Change management

### Operations
- Backup configurations
- Firmware updates
- Monitoring and alerting
- Incident response

### Security
- Defense in depth
- Least privilege access
- Regular security audits
- Patch management

## Common Protocols

### Routing
- **OSPF**: Interior gateway protocol
- **BGP**: Exterior gateway protocol
- **EIGRP**: Cisco proprietary (legacy)
- **Static routes**: Simple networks

### Switching
- **STP/RSTP**: Loop prevention
- **VTP**: VLAN management (not recommended)
- **LACP**: Link aggregation
- **LLDP**: Device discovery

### Management
- **SNMP**: Monitoring
- **Syslog**: Logging
- **SSH**: Secure access
- **TFTP/SCP**: Configuration backup

## Hardware Vendors

### Enterprise Networking
- Cisco
- Juniper
- Arista
- HPE/Aruba
- Dell
- Extreme Networks

### Firewall Vendors
- Palo Alto Networks
- Fortinet
- Check Point
- Cisco (ASA, Firepower)
- pfSense/OPNsense (open-source)

## Contributing

To add a new on-premise template:

1. Create a new `.md` file in this directory
2. Follow the template format in `../TEMPLATE-GUIDE.md`
3. Include YAML frontmatter with `category: on-premise`
4. Show physical and logical topology
5. Document protocols and technologies
6. Include redundancy and HA considerations
7. Add the template to this README

## Suggested Templates to Add

- Three-tier data center network
- Spine-leaf fabric architecture
- Enterprise campus network
- Branch office network
- DMZ with firewall zones
- Redundant internet connectivity
- Data center interconnect (DCI)
- Storage area network (SAN)
- Voice over IP (VoIP) network
- Wireless network architecture
- Remote access VPN
- MPLS WAN topology
- Active Directory site topology
- Disaster recovery site network
- High-performance computing (HPC) network
