# **RIP(Routing Information Protocol，路由信息协议)**

RIP是非常古早的路由协议，现如今应用较少，但学习RIP可以了解动态路由的原理，在实际运用上，能不用RIP就不要用RIP，如必须要使用RIP则尽可能使用RIPv2。

如果部分设备性能不足可以使用OSPF等进行配置，（叠个甲，AI说的）。

RIPv1由RFC-1923定义，RIPv2由RFC-2453定义。

![image1.png](images/RIP_image/image1.png)

- 距离矢量路由协议
- IGP协议
- 基于UDP，目标端口号520
- 周期性更新
- 适用于小型网络，有RIPv1和RIPv2两个版本。
- 周期性更新
- 支持水平分割，毒性逆转等防环特性。
- RIPv2使用组播地址224.0.0.9

---

## **RIP工作原理**

- 跳数

RIP使用跳数作为度量值来衡量到达目的的网络的距离

缺省情况下，直连网络的路由跳数为0，当路由器发送路由更新时，会把度量值加1，

RIP规定超过15跳则为网络不可达。因此RIP难以试用于大型网络。

## **RIPv1与RIPv2**

### **RIPv1**

RIPv1是有类路由协议，不支持VLSM和CIDR。

以广播的形式发送报文

不支持认证

### **RIPv2**

RIPv2为无类路由协议，支持VLSM，支持聚合与CIDR

支持以广播或者组播方式发送报文

组播地址为（224.0.0.9）

支持明文认证和MD5密文认证。

## **RIPv1数据报**

```mermaid
packet-beta
title RIP Packet Format (RIP 数据包格式)
0-7: "Command (命令)"
8-15: "Version (版本)"
16-31: "Must be Zero (必须为0)"
32-47: "Address Family Identifier (地址族标识符)"
48-63: "Must be Zero (必须为0)"
64-95: "IP Address (IP地址)"
96-127: "Must be Zero (必须为0)"
128-159: "Must be Zero (必须为0)"
160-191: "Metric (度量值)"
```

## **RIPv2数据报**

```mermaid
packet-beta
title RIPv2 Packet Format (RIPv2 数据包格式)
0-7: "Command (命令)"
8-15: "Version (版本)"
16-31: "Must be Zero (必须为0)"
32-47: "Address Family Identifier (地址族标识符)"
48-63: "Must be Zero (必须为0)"
64-95: "IP Address (IP地址)"
96-127: "Subnet Mask (子网掩码)"
128-159: "Next Hop (下一跳)"
160-191: "Metric (度量值)"
```

![image2.png](images/RIP_image/image2.png)

## 水平分割和毒性逆转

在距离矢量协议中，路由器之间会定期交换路由表。如果没有保护机制，可能会出现“环路”和“无穷计数”（Count-to-Infinity）的问题。

**水平分割**和**毒性逆转**是RIP和其他距离矢量协议中的广泛运用的两大防环机制，RIP中这两个功能的默认开启的。

### **水平分割**

开启水平分割的路由器从**接口A收到的路由信息，将不会再把这个路由信息发回给这个接口A。**即**从哪学来的路由，就不再从哪发回去**。

- 如果没有水平分割

```mermaid
sequenceDiagram
    participant B as AR-B (拥有 1.1.1.0路由)
    participant A as AR-A

    Note over B, A: 第一次交换路由表
    B->>A: RIP更新(1.1.1.0) (Metric=1)
    Note right of A: A 学习并存入路由表<br/>(下一跳指向 B)

    Note over B, A: 第2次交换路由表
    Note right of B: B 与1.1.1.0断开了连接
    A->>B: RIP更新(1.1.1.0) (Metric=2)
       Note left of B: B以为A有1.1.1.0路由，但实际上没有。
```

第一次交换路由表时，AR-B有1.1.1.0路由。AR-B将1.1.1.0路由条目发送给AR-A。

在第二次时交换路由表时，AR-B断开了1.1.1.0的连接，此时AR-B没有路由，但AR-A仍然有1.1.1.0路由。AR-A将1.1.1.0路由条目发送给AR-B。AR-B便会认为AR-A有1.1.1.0路由。

如果开启水平分割，AR-B将不会再把1.1.1.0路由条目发回给AR-A。便不会发生路由条目错误。

### **毒性逆转**

毒性逆转是水平分割的一种特殊变体。当路由器 A 从路由器 B 学习到一个网络的路由时，路由器A会把这个路由信息发回给路由器B，但是它会将该路由的度量值（Metric/Hop Count）设置为无穷大(不可达)。

在RIP中，跳数达到16则不可达，所以在RIP中度量值为16。

毒性逆转相对于水平分割而言，水平分割是沉默的，而毒性逆转是主动声明不可达的。根本上删除了回环的可能性。在一些特定的故障恢复场景中，毒性逆转能的主动声明比水平分割更快地消除环路。
