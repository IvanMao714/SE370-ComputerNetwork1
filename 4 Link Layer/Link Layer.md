# **Link Layer**

Responsibility: transferring datagram from one node to physically adjacent node over a link

Datagrams: frames

Different link protocols over different links

- Wired: Ethernet, token ring
- Wireless: WIFI, Bluetooth

Network scope: LAN

### **Error Detection/Correction**

#### Single bit parity

![](C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\1.png)

加一个检验比特，使得总共1的个数为偶数个，若检测到为奇数个则出错

只能检验出出错个数为奇数

#### Two-dimensional bit parity

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\2.png" style="zoom:67%;" />

- detect and correct single bit errors
- detect two bits errors, but cannot correct 

#### Cyclic Redundancy Check (CRC)

- D: data bits (given, think of these as a binary number)
- G: bit pattern (generator), of *r+1* bits (given)

给定一个G和一个R，使得G可以整除<D, R>

![](C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\3.png)

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\4.png" style="zoom:75%;" />

- receiver knows G, divides <D,R> by G. If non-zero remainder: error detected!
- can detect all burst errors less than r+1 bits
- widely used in practice (Ethernet, 802.11 WiFi)

#### **Multiple Access Protocols**

#### Collision

Two or more simultaneous transmissions by nodes on a shared channel

#### Collision domain

Hosts that on a shared broadcast medium, where collisions may occur

#### Taxonomy of MAC protocols

##### Channel of partitioning (collision-free)

TDMA, FDMA

##### Random access (need to handle collisions)

**Slotted ALOHA**

![](C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\5.png)

把时间分成时间间隙

- When the node has a fresh frame to send, it waits until the beginning of the next slot and transmits the entire frame in the slot. 
- If there isn’t a collision, the node has successfully transmitted its frame and thus need not consider retransmitting the frame. (The node can prepare a new frame for transmission, if it has one.) 
-  If there is a collision, the node detects the collision before the end of the slot. The node retransmits its frame in each subsequent slot with probability p until the frame is transmitted without a collision.

**ALOHA**

没有将时间分成间隙，直接立即发送

![](C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\6.png)

**CSMA/CD**

- Listen before speaking. If someone else is speaking, wait until they are finished. In the networking world, this is called carrier sensing—a node listens to the channel before transmitting. If a frame from another node is currently being transmitted into the channel, a node then waits until it detects no transmissions for a short amount of time and then begins transmission. 
- If someone else begins talking at the same time, stop talking. In the networking world, this is called collision detection—a transmitting node listens to the channel while it is transmitting. If it detects that another node is transmitting an interfering frame, it stops transmitting and waits a random amount of time before repeating the sense-and-transmit-when-idle cycle.



##### Taking turns (collision free, with more flexibility but with overhead)

##### Polling

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\8.png" style="zoom:75%;" />

##### token pass

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\9.png" style="zoom:75%;" />

### **LAN**

#### Addressing

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\10.png" style="zoom:50%;" />



#### ARP: IP address => MAC address

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\11.png" style="zoom:50%;" />

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\12.png" alt="12" style="zoom:50%;" />

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\13.png" alt="13" style="zoom: 50%;" />



Self-learning mechanism

##### Routing to another subnet

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\14.png" style="zoom:50%;" />

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\16.png" style="zoom:50%;" />



<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\18.png" alt="18" style="zoom:50%;" />

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\19.png" alt="19" style="zoom:50%;" />

### **Ethernet**

<img src="C:\Users\65151\Desktop\Computer Network\4 Link Layer\img\20.png" style="zoom:75%;" />