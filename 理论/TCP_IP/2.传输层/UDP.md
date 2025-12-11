# **UDP协议：**

UDP是基于IP的简单的面向无连接的协议. 提供不可靠传输。

与TCP相比，UDP极为简单。它没有什么win机制，重传机制……,传输数据只会“尽力而为”。我发送了数据，但不保证对方一定能收到，也不保证送达顺序。但是换来的是速度快且省事。

UDP常用在不需要保证数据完整性但需要速度快的场景中，例如打视频电话。

## **UDP数据报**

UDP数据报主要由**用户数据**和**UDP首部**组成，其中UDP首部由**源端口、目的端口、UDP长度和UDP校验**和组成。其中UDP长度的最小值为8，表示只有UDP首部而没有数据部分。

```mermaid
packet-beta
title UDP Header
0-15: "源端口 (Source Port)"
16-31: "目标端口 (Destination Port)"
32-47: "长度 (Length)"
48-63: "校验和 (Checksum)"
```

源端口和目的端口，端口号理论上可以有2^16这么多。因为它的长度是16个bit。

**Length**:占用2个字节，标识UDP头的长度，包括首部长度和数据长度。

**Checksum（校验和）**:包含UDP头和数据部分。发送端应该计算检验和。UDP检验和覆盖UDP协议头和数据，这和IP的检验和是不同的，IP协议的检验和只是覆盖IP数据头，并不覆盖所有的数据。UDP和TCP都包含一个伪首部，这是为了计算检验和而设置的。

```mermaid
packet-beta
title UDP 伪首部与头部结构 (Pseudo Header & UDP Header)
0-31: "源 IPv4 地址 (Source IPv4 Address)"
32-63: "目标 IPv4 地址 (Destination IPv4 Address)"
64-71: "零 (Zero)"
72-79: "协议 (Protocol)"
80-95: "UDP 长度 (UDP Length)"
96-111: "源端口 (Source Port)"
112-127: "目标端口 (Destination Port)"
128-143: "长度 (Length)"
144-159: "校验和 (Checksum)"
160-191: "数据 (Data)"
```

伪首部甚至还包含IP地址这样的IP协议里面都有的信息，目的是让UDP两次检查数据是否已经正确到达目的地。如果发送端没有打开检验和选项，而接收端计算检验和有差错，那么UDP数据将会被丢掉（不保证送达），而不产生任何差错报文。
