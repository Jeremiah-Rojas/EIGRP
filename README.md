# EIGRP

## Network Topology
<img width="875" height="582" alt="image" src="https://github.com/user-attachments/assets/5c4c39be-4a9a-4f81-af69-2d1c8effe744" />

<br>The (EIGRP) Enhanced Interior Gateway Routing Protocol works within an autonomous system (AS); an AS is a collection of networks under a single administrative domain. Similar to OSPF, EIGRP will automatically detect link failures and re-route traffic for optimal network performance/reliability. EIGRP is different because it is easier to configure, has very fast convergence time (quickly updates routing table), and is ideal for a network consisting of all Cisco devices; although EIGRP is no longer Cisco-proprietary. This lab shows EIGRP in action and how to configure it.

### Devices Used:
- Cisco IOSvL2 15.2.1 switch
- GNS3 Software
- Ubuntu Container (running on VMware machine)


## Configurations

Note: It is recommended to copy and paste these commands into the routers. Because of the limited width of the table, some commands, which should be treated as one line, are broken into two lines and entering these commands as two lines will throw an error.

