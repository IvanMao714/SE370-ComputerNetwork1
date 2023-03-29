# Network Control Plane

### 1. Routing Algorithm

#### Dijkstra’s Link-State routing algorithm

```
1  Initialization: 
2    N' = {u}                               /* compute least cost path from u to all other nodes */
3    for all nodes v 
4      if v adjacent to u            /* u initially knows direct-path-cost only to  direct neighbors    */
5          then D(v) = cu,v                   /* but may not be minimum cost!                                                   
6      else D(v) = ∞ 
7 
8   Loop 
9   find w not in N' such that D(w) is a minimum   
10  add w to N'   
11  update D(v) for all v adjacent to w and not in N' : 
12  D(v) = min ( D(v),  D(w) + cw,v  ) 
13  until all nodes in N' 

```

需要输入一个source 和对应的表

<img src=".\img\1.png" style="zoom:75%;" />

shortcoming: 会出现线路拥堵程度的震荡

#### **Distance vector algorithm** 

<img src=".\img\2.png" style="zoom:75%;" />

cons: "好事传播速度快，坏事传播速度慢"

### 2. Intra-ISP routing: OSPF

<img src="img\3.png" style="zoom:75%;" />

- “open”: publicly available

- classic link-state 

  - each router floods OSPF link-state advertisements (directly over IP rather than using TCP/UDP) to all other routers in entire AS

  - multiple link costs metrics possible: bandwidth, delay

  - each router has full topology, uses Dijkstra’s algorithm to compute forwarding table

- *security:* all OSPF messages authenticated (to prevent malicious intrusion) 

**two-level hierarchy:** local area, backbone.

- link-state advertisements flooded only in area, or backbone
- each node has detailed area topology; only knows direction to reach other destinations

![](.\img\4.png)

### 3. Routing among ISPs: BGP

- BGP (Border Gateway Protocol): *the* de facto inter-domain routing protocol
  - “glue that holds the Internet together”

- allows subnet to advertise its existence, and the destinations it can reach, to rest of Internet: *“**I am here, here is who I can reach, and how”*

- BGP provides each AS a means to:

  - eBGP: obtain subnet reachability information from neighboring ASes

  - iBGP: propagate reachability information to all AS-internal routers.

  - determine “good” routes to other networks based on reachability information and *policy*
