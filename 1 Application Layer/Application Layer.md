# **Application Layer**

### Two predominant architectural paradigms(体系结构)

**Client-Server paradigm**: Web, Email, Streaming, Messaging, Interactive games

**Peer-Peer paradigm:** P2P file sharing



### The Interface Between the Process and the Computer Network

process sends/receives messages to/from its socket

**identifier = <IP address, port number>**

To send HTTP message to gaia.cs.umass.edu web server:

- IP address: 128.119.245.12

- port number: 80

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\1.png)



### Web: HTML

Web page:

- consists of *objects,* each can be stored on different Web servers
- object can be HTML file, JPEG image, Java applet, audio file,…
- each object is addressable by a URL, e.g.,

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\2.png)



### **Basics of HTTP**

#### Four steps using TCP

1. 发起一个与服务器的TCP连接
2. 通过TCP发送HTTP请求
3. 通过TCP收到HTTP相应
4. 断开TCP连接

#### HTTP is stateless

HTTP服务器并不保存关于客户的任何信息 -> stateless

ex; If a particular client asks for the same object twice in a period of a few seconds, the server does not respond by saying that it just served the object to the client; instead, the server resends the object, as it has completely forgotten what it did earlier

#### Non-persistent/Persistent HTTP (1.1)

- Non-persistent: 每个请求/响应对是经过一个单独的TCP连接发起的
- Persistent：每个请求/响应对是经过相同的TCP连接发起的**（HTTP 1.1 使用）**

**RTT (Round-Trip Time)(往返时间)**：The time it takes for a small packet to travel from client to server and then back to the client. The RTT includes packet-propagation delays, packetqueuing delays in intermediate routers and switches, and packet-processing delays.

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\3.png)



### **HTTP request** message

Two types of HTTP messages: *request*, *response*

**HTTP request message:**  ASCII (human-readable format)

<img src="C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\4.png" style="zoom:75%;" />

**HTTP request message: general format**

<img src="C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\5.png" style="zoom:75%;" />

**Other HTTP request** **messages**

1. **POST method:** 

   - web page often includes form input

   - **user input sent from client to server in entity body of HTTP POST request message**，Get的通常为空的
   - 用户提交表单
   - Web页面的特定内容依赖于用户在表单输入的内容，Web的页面请求

2. **GET method:**
   - Include user data in URL field of HTTP GET request message (following a ‘?’)，**所请求的URL中包括输入的数据**:![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\6.png)

3. **HEAD method:**
   - Requests headers (only) that would be returned *if* specified URL were requested with an HTTP GET method. 
   - 服务器收到HEAD请求时，会返回一个HTTP响应，但不返回请求对象
   - 常用来调试跟踪

4. **PUT method:**
   - uploads new file (object) to server
   - completely replaces file that exists at specified URL with content in entity body of POST HTTP request message



#### **HTTP response** **message**

<img src="C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\7.png" style="zoom:75%;" />

**HTTP response** **status codes**

status code appears in 1st line in server-to-client response message.

some sample codes:

- 200 OK

  request succeeded, requested object later in this message

- 301 Moved Permanently

  requested object moved, new location specified later in this message (in Location: field)

- 400 Bad Request

  request msg not understood by server

- 404 Not Found

  requested document not found on this server

- 505 HTTP Version Not Supported

### **HTTP: Advanced Issues**

##### Cookies

- Purpose: to solve the stateless issue
- Four components
  - A cookie header line in the HTTP response message
  - A cookie header line in the HTTP request message
  - A cookie file kept on the user’s end system and managed by the user’s browser
  - A back-end database at the Web site

<img src="C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\8.png"  />

##### Web caches

- Purpose: satisfy client requests without involving origin server(保存最近请求过的对象的副本)

- Also known as proxy server

- Conditional Get: **If-modified-since: <date>, HTTP/1.0 304 Not Modified**

  1. proxy cache代表一个请求浏览器，向Web服务器发送请求报文：

  ![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\9.png)

  2. Web服务器向缓存器发送具有被请求的对象的响应报文：

     ![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\10.png)

  3. 一星期后对象仍储存在本地，再向其发送请求报文，询问对象是否被修改（日期为一星期前访问的日期）

     ![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\11.png)

  4. 如果没有修改，则返回无entity的报文，否则更新

     ![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\12.png)

     

### **Email, SMTP, IMAP**

Three major components： **user agents, mail servers, SMTP protocol**

<img src="C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\13.png" style="zoom:75%;" />

#### SMTP procedure

1. Alice invokes her user agent for e-mail, provides Bob’s e-mail address (for example, bob@someschool.edu), composes a message, and instructs the user agent to send the message. 
2. Alice’s user agent sends the message to her mail server, where it is placed in a message queue.
3. The client side of SMTP, running on Alice’s mail server, sees the message in the message queue. It opens a TCP connection to an SMTP server, running on Bob’s mail server. 
4. After some initial SMTP handshaking, the SMTP client sends Alice’s message into the TCP connection. 
5. At Bob’s mail server, the server side of SMTP receives the message. Bob’s mail server then places the message in Bob’s mailbox. 
6. Bob invokes his user agent to read the message at his convenience.

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\14.png)

#### client STMP => server STMP

1. Open a TCP connection

2. SMTP handshaking

3. SMTP transfer of messages

4. SMTP closure

   <img src="C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\15.png" style="zoom:76%;" />

### **Comparison with HTTP**

##### Different

- HTTP: client pull

  SMTP: client push

- HTTP: each object encapsulated in its own response message(对象可能存储在不同的主机上)

  SMTP: multiple objects sent in multipart message（在同一主机）

**Same**

- Both have ASCII command/response interaction, status codes

  

### **Domain Name System (DNS)**

Application-layer protocol： hosts, DNS servers communicate to *resolve* names   (hostname-to-IP-address translation)；core Internet function

Distributed database： implemented in hierarchy of many *name servers*

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\16.png)



#### **Iterated query（迭代查询）:**

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\17.png)

#### **Recursive query（递归查询）:**

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\18.png)

**实践中请求主机到本地DNS服务器的查询是递归的，其余的是迭代的**

#### **DNS records**

![](C:\Users\65151\Desktop\Computer Network\1 Application Layer\img\19.png)

- **Type=A: Name is a hostname, Value is the IP address for the hostname.** Thus, a Type A record provides the standard hostname-to-IP address mapping. As an example, (relay1.bar.foo.com, 145.37.93.126, A) is a Type A record.
- **Type=NS: Name is a domain (such as foo.com), Value is the hostname of an authoritative DNS server that knows how to obtain the IP addresses for hosts in the domain.** This record is used to route DNS queries further along in the query chain. As an example, (foo.com, dns.foo.com, NS) is a Type NS record. **Value是获得该域主机IP地址的权威DNS服务器的主机名**
- **Type=CNAME: Value is a canonical hostname for the alias hostname Name**. This record can provide querying hosts the canonical name for a hostname. As an example, (foo.com, relay1.bar.foo.com, CNAME) is a CNAME record. **Value是别名为Name 的主机对应的规范主机名**
- **Type=MX: then Value is the canonical name of a mail server that has an alias hostname Name.** As an example, (foo.com, mail.bar.foo.com, MX) is an MX record. MX records allow the hostnames of mail servers to have simple aliases. Note that by using the MX record, a company can have the same aliased name for its mail server and for one of its other servers (such as its Web server). To obtain the canonical name for the mail server, a DNS client would query for an MX record; to obtain the canonical name for the other server, the DNS client would query for the CNAME record. **Value是别名为Name 的邮件服务器对应的规范主机名**

