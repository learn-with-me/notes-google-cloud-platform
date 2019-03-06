# VPC Networks

VPCs are isolated, private partitions for resources. They contain abstractions for routes, rules and IP addresses. VPCs are global, span regions, and are composed of regional subnets. IP addresses, routes and firewall rules all exist inside a VPC network.

##### Types of VPC

* Auto mode
* Custom mode

##### Firewall Rules

These rules control network traffic, set boundries around resources and can even be applied on a per-instance basis. Hence, these rules can regulate internal traffic as well. Two implied firewall rules that cannot be deleted are:

* Implied allow egress - all GCP resources to send traffic to external clients
* Implied deny ingress - by default none of the external can come in network

Additional rules in default VPC

* default-allow-internal
* default-allow-ssh
* default-allow-rdp
* default-allow-icmp

##### Internal DNS



##### Things to remember

* VPC must exist inside a project
* AWS VPCs are confined to a region whereas Google VPCs span across regions
* Google VPCs have subnets \(sub-networks\) that are confined to a single region. A resource \(either on default VPC or custom VPC will also have to be on one of the subnets\)
* You can configure firewall rules to restrict and regulate the network traffic flows in a VPC



