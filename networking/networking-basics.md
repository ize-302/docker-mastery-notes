# Networking basics

### LAN - Local Area Network

A private network which comprises of set of devices or machines talking with eachother within a limited range using either cable or wireless technology

- #### Internet Protocol (IP)

  A set of rules governing the format of data sent between devices via the local network or internet. Each device is identified with a unique address called the IP address. An IP address contains location information and makes a device accessible for communication.

- #### Switch

  A networking device that sits in the LAN that helps devices in that network communicate with eachother using the their IP addresses. It operates at the data link layer (Layer 2)

- #### Subnet or Subnetwork

  A subnet, short for subnetwork, is a division of an IP or local network into smaller, interconnected sub-networks

- #### Router

  The router is a networking device that connects different networks together. It operates at the Network layer (Layer 3) of the OSI (Open Systems Interconnection) model. A router is what separates the networks or subnets

  ###

![illustration show network architect and communication](/illustrations/local_area_networks.png "illustration show network architect and communication")

### WAN - Wide Area Network

- #### Firewall

  A firewall is a network device of software that monitors and controls incoming and outgoing traffic using a predefined set of rules. Its purpose is to create a barrier between secured internal network and untrusted external networks to prevent unauthorised communication

- #### DMZ (Demilitarized Zone) or perimeter network

  It is an area that is isolated from the rest of the network to allow access to attached devices from both internal network and the internet. It is a way of protecting a private internal network while allowing access to specific machines or services and at the same time minimizing the potential risks associated with direct exposure to external networks. It typically does this with the use of firewall to monitor and control access
  ![illustration of DMZ using one firewall ](/illustrations/dmz_1_firewall.png "illustration of DMZ using one firewall")
  illustration of DMZ using one firewall

![illustration of DMZ using two firewalls ](/illustrations/dmz_2_firewalls.png "illustration of DMZ using two firewalls")
illustration of DMZ using two firewalls

- #### Port Forwarding

  It is the process of allowing external computers to have access to a computer on your network over the internet even if you are behind a router. It does this by allowing configuring the router to accept requests coming from certain ports and forwarding such request to the desired computer's ip address

- #### NAT (Network Address Translation)

  NAT is a networking technology that maps private ip addresses used in a local network to a single public IP address or a few public IP addresses. This process is usually done in the router and ensures that devices in the same local network share the same public ip address when communicating with external network or the internet
