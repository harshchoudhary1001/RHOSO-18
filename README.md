# RHOSO-18

Vlan Information of Infra

| Sr No | Network Name         | VLAN | VLAN Mode | Start IP    | End IP       | Gateway    | Subnet        |
| ----: | -------------------- | ---: | --------- | ----------- | ------------ | ---------- | ------------- |
|     1 | designate            |  101 | tagged    | 10.101.1.10 | 10.101.1.254 | 10.101.1.1 | 10.101.1.0/24 |
|     2 | Internal Network     |  103 | tagged    | 10.103.1.10 | 10.103.1.254 | 10.103.1.1 | 10.103.1.0/24 |
|     3 | designateexternal    |  104 | tagged    | 10.104.1.10 | 10.104.1.254 | 10.104.1.1 | 10.104.1.0/24 |
|     4 | Tenant Network       |  105 | tagged    | 10.105.1.10 | 10.105.1.254 | 10.105.1.1 | 10.105.1.0/24 |
|     5 | Storage Network      |  106 | tagged    | 10.106.1.10 | 10.106.1.254 | 10.106.1.1 | 10.106.1.0/24 |
|     6 | ControlPlane and OCP Network |  100 | untagged  | 10.100.1.10 | 10.100.1.254 | 10.100.1.1 | 10.100.1.0/24 |
|     7 | Octavia              |  102 | tagged    | 10.102.1.10 | 10.102.1.254 | 10.102.1.1 | 10.102.1.0/24 |
|     8 | Provider Admin 1     |  200 | tagged    | 172.16.1.10 | 172.16.1.250 | 172.16.1.1 | 172.16.1.0/24 |



Preparing the Infra on KVM server.
------------------------------------------------
Lab OS: Rocky -8

Install Package - yum install libvirt vim wget virt-* -y

##Create below network on KVM server:
network1
network2
network3

Network Details for Openshift Node
--------------------------------------------------------
Network1 for enp1s0  --> ctlplane                  (Recommend to bond0)
Network2 for enp7s0 ---> Storage network            Recommend to bond1)
Network1 for enp8s0  --> Internal,ctlplane,Tenant,Octavia,Designate and Designate_External (Recommend to bond2)

Note: As we do not require provider on OCP nodes so we can utilise bond2 for extra network required for OSP and we are providing one dedicated bond for openshift.


Network Details for Openstack Compute/DataPlane Node
--------------------------------------------------------
Network1 for bond0 --> Internal,ctlplane,Tenant
Network2 for bond1 ---> Storage network
Network3 for bond2  --> Provider Network



