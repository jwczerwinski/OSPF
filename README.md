# OSPF

<h2>Description</h2>
Confgiure OSPF on R1, R2, R3 & R4.

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b> (2.2.43) <br />

- <b>Cisco IOS PT1000 Software, Version 12.2(28) <br />

<h2>Diagram </h2>
<img src="https://i.imgur.com/lic34L9.png" height="80%" width="80%" />

<h2>Walk-through:</h2>
Configurations on R1 for loopback interface, OSPF area 0 including all IPv4 addresses. Configure R1 as area border router. <br />
R1(config)#int l0 <br />
R1(config-if)#ip address 1.1.1.1 255.255.255.255 (loopback interface IP address will always be OSPF device identifier from other routers routing tables) <br />
R1(config-if)#router ospf 1 (OSPF process ID doesn't need to match between routers) <br />
R1(config-router)#net 0.0.0.0 255.255.255.255 area 0 (OSPF "0.0.0.0 255.255.255.255" includes all addresses) <br />
R1(config-router)#passive-interface l0 (prevents interface from needlessly sending OSPF messages) <br />
R1(config-router)#default-information originate (configures R1 as autonomous system boundary router) <br />
R1(config-router)#exit <br />
R1(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.2 (default route to ISP) <br />
<img src="https://i.imgur.com/tHeU3fH.png" height="80%" width="80%" />
<br />
<br />
Configurations on R2 for loopback interface and OSPF area 0 including exact IPv4 address connected subnetworks. <br />
R2(config)#int l0 <br />
R2(config-if)#ip address 2.2.2.2 255.255.255.255 <br />
R2(config-if)#router ospf 1 <br />
R2(config-router)#net 10.0.12.2 0.0.0.0 area 0 (enables interfaces with exact subnetwork) <br />
R2(config-router)#net 10.0.24.1 0.0.0.0 area 0 <br />
R2(config-router)#passive-interface l0 <br />
<img src="https://i.imgur.com/mSbZfyg.png" height="80%" width="80%" />
<br />
<br />
Configurations on R3 for loopback interface and OSPF area 0 including a broader IPv4 address subnetwork. <br />
R3(config)#int l0 <br />
R3(config-if)#ip address 2.2.2.2 255.255.255.255 <br />
R3(config-if)#router ospf 1 <br />
R3(config-router)#net 10.0.0.0 0.0.255.255 area 0 (enables interfaces within subnetwork range) <br />
R3(config-router)#passive-interface l0 <br />
<img src="https://i.imgur.com/qd1Ohel.png" height="80%" width="80%" />
