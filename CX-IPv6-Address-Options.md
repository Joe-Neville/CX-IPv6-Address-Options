# Aruba AOS-CX IPv6 Address Allocation

## Abstract
This document explains the numerous methods of IPv6 address allocation available on the Aruba AOS-CX Network Operating System and details how to configure the different methods.

## IPv6 Address Allocation Overview

IPv6 addresses can be allocated to clients by a variety of methods:

1. Stateless Address Autoconfiguration - the client generates its own globally routable address using the /64 prefix advertised by the local gateway in a Router Advertisement (RA).

2. DHCPv6 Stateful - Through the exchange of DHCPv6 messages between client and DHCPv6 server, a /128 address is assigned to the client by the server. By this method, the DHCPv6 server can also assign additional options such as DNS server and DNS Search-List.

3. DHCPv6 Stateless - A combination of SLAAC and DHCPv6, the client generates its address via the prefix in the local gateway's RA, but also queries the DHCPv6 server for other information such as DNS server and search-list.

## Network Design

### Design Overview

The network device of prime importance is an Aruba AOS-CX 8320. This is the Layer 3 gateway, and the source of IPv6 Router Advertisements.
The 8320 has connectivity to a Server LAN, upon which resides a Windows Server configured for DHCPv6.
The 8320 is positioned as a core or aggregration layer switch. It is connected to an Aruba 3810M switch, which provides the access layer function and Power-Over-Ethernet. The 3810M is merely a Layer 2 switch and is not configured for IPv6.
Wireless connectivity is provided by an Aruba UAP303-HR Access Point.
The 8320 is configured with four client subnets & VLANs which connect through the 3810M to the UAP's Uplink Port via an 802.1Q trunk.
Each client subnet on the 8320 is configured with the necessary features to enable a connected client to obtain its IPv6 address by one of the various allocation methods, see the table below:

| VLAN | Prefix  |  Method | SSID  |
|------|---------|---------|-------|
| 1001 | 2001:db8:a:1001::/64 | SLAAC | v6net-SLAAC |
| 1002 | 2001:db8:a:1002::/64 | DHCPv6 Stateful | v6net-DHCPv6-Stateful |
| 1003 | 2001:db8:a:1003::/64 | DHCPv6 Stateless | v6net-DHCPv6-Stateless |
| 1004 | 2001:db8:a:1004::/64 | SLAAC & DHCPv6 | v6net-All-On |


### Network Kit List

* 1 x Windows Server 2019 - acting as DHCPv6 and DNS server.
* 1 x Aruba 8320 Switch running CX version 10.03.40 - this is the Layer 3 IPv6 gateway.
* 1 x Aruba 3810M Switch - acting as an access layer switch, providing PoE.
* 1 x Aruba UAP303HR Access Point - to enable wireless connectivity.



##### Network diagram





