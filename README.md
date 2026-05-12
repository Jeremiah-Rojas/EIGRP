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
| R1 | R2 | R3 |
|---|---|---|
| enable<br>conf t<br>hostname R1<br><br>interface g0/0<br>ip address 192.168.1.1 255.255.255.0<br>no shutdown<br><br>interface g0/1<br>ip address 10.0.12.1 255.255.255.252<br>no shutdown<br><br>interface g0/2<br>ip address 10.0.13.1 255.255.255.252<br>no shutdown<br><br>router eigrp 100<br>no auto-summary<br><br>network 192.168.0.0<br>network 10.0.0.0<br>end<br>wr | enable<br>conf t<br>hostname R2<br><br>interface g0/0<br>ip address 192.168.2.1 255.255.255.0<br>no shutdown<br><br>interface g0/1<br>ip address 10.0.12.2 255.255.255.252<br>no shutdown<br><br>interface g0/2<br>ip address 10.0.23.1 255.255.255.252<br>no shutdown<br><br>router eigrp 100<br>no auto-summary<br><br>network 192.168.0.0<br>network 10.0.0.0<br>end<br>wr | enable<br>conf t<br>hostname R3<br><br>interface g0/0<br>ip address 192.168.3.1 255.255.255.0<br>no shutdown<br><br>interface g0/1<br>ip address 10.0.13.2 255.255.255.252<br>no shutdown<br><br>interface g0/2<br>ip address 10.0.23.2 255.255.255.252<br>no shutdown<br><br>router eigrp 100<br>no auto-summary<br><br>network 192.168.0.0<br>network 10.0.0.0<br>end<br>wr |

Understanding the commands:
- “router eigrp 100” enables EIGRP and assigns the number 100 as the AS number; it is just a way of identifying an AS ans since EIGRP is an interior gateway protocol, all the router will be in the same AS.
- “no auto-summary” disables automatic route summarization; route summarization may incorrectly subnet the network causing issues.
- “network #.#.#.#” tells the router which networks should be enabled for EIGRP

<br>
R1 EIGRP details:<img width="1088" height="152" alt="image" src="https://github.com/user-attachments/assets/baa417b4-fc83-458a-8a81-bd7b7981f107" />

Output of “show ip route eigrp”:<img width="1089" height="133" alt="image" src="https://github.com/user-attachments/assets/daed6e37-af65-46d6-a3a1-ab533c299ac6" />



<br>
R2 EIGRP details:<img width="1088" height="159" alt="image" src="https://github.com/user-attachments/assets/8521becc-1aa5-4fee-bd7e-9a25f81991b9" />

Output of “show ip route eigrp”:<img width="1088" height="133" alt="image" src="https://github.com/user-attachments/assets/f13d9ced-c948-4121-96eb-bf8cc16281cf" />



<br>
R3 EIGRP details:<img width="1087" height="160" alt="image" src="https://github.com/user-attachments/assets/ad0d5cb2-dfa8-4aea-808a-c0c1bf8e708e" />

Output of “show ip route eigrp”:<img width="1091" height="134" alt="image" src="https://github.com/user-attachments/assets/7a17c5c6-11b7-4967-bdbc-f6c82883ce88" />



<br>Understanding the output:
- Hold: shows how long (in seconds) before the EIGRP is declared down. This timer is reset every time a “hello” packet is sent from an EIGRP neighbor; if the timer hits 0, the neighbor is declared down.
- SRTT: Stands for “Smooth Round Trip Time” and shows how long (in milliseconds) reliable EIGRP packets take to be acknowledged. Lower is better.
- RTO: is the Retransmission Timeout and shows how long EIGRP waits before retransmitting packets; this is measured in milliseconds. Lower is better.
- Q Cnt: This is the queue count and shows how many packets are waiting to be processed.
- Seq Num: Sequence number is used for packet tracking
- The “D” in the output of “show ip route eigrp” means EIGRP is in use

