# Datacom 数据通信技术笔记


本目录收录数据通信（Datacom）方向笔记

---

# 目录

目录结构如下：

```text
Datacom/
│
├── 理论/                                 # 理论深度剖析与原理说明
│   ├── 网络基础/
│   │   ├── 企业网络架构基础.md          # 企业网三层/二层架构设计与组件说明
│   │   ├── 网络拓扑.md                  # 常见拓扑结构（星型、网状、树状）与冗余设计
│   │   └── 网络模型.md                  # OSI 七层与 TCP/IP 四/五层模型对比
│   │
│   ├── TCP_IP/                          # 协议栈底层细节
│   │   ├── 1.应用层/                    # HTTP, DNS, DHCP, FTP 等
│   │   ├── 2.传输层/                    # TCP 握手/挥手、滑动窗口、UDP 协议
│   │   ├── 3.网络层/                    # IP, ICMP, ARP 报文格式与工作原理
│   │   ├── 4.数据链路层/                # 以太网帧格式、MAC 地址学习机制
│   │   └── 5.物理层/                    # 传输介质与编码技术
│   │
│   ├── 二层相关技术/                    # 局域网交换与防环
│   │   ├── VLAN.md                      # 802.1Q、Access/Trunk/Hybrid 端口详解
│   │   ├── STP_RSTP.md                  # 生成树协议选举流程、端口状态与收敛优化
│   │   └── MSTP.md                      # 多生成树协议原理与实例映射
│   │
│   ├── 路由技术/                        # 控制平面与数据平面路由协议
│   │   ├── HCIA路由知识.md              # 路由表匹配、AD/Metric 基础
│   │   ├── HCIP路由知识.md              # 路由引入、控制与策略（Route-Policy/Filter）
│   │   ├── RIP.md                       # 距离矢量协议原理与防环机制
│   │   ├── OSPF.md                      # LSA 1~7 型详解、区域划分、DR/BDR 选举与邻居状态机
│   │   ├── IS-IS(LSU待补全).md          # 链路状态协议、Level-1/2 路由与报文格式
│   │   ├── BGP.md                       # BGP 属性、选路规则、IBGP/EBGP 防环与反射器
│   │   ├── BGP4+.md                     # MP-BGP 对 IPv6 的扩展支持
│   │   ├── SR.md                        # Segment Routing 基础架构与控制器协作
│   │   ├── SRv6.md                      # SRv6 报文头、Segment List 与 IPv6 数据平面结合
│   │   └── 组播_IGMP_PIM.md             # 组播架构、IGMPv1/v2/v3 与 PIM-SM/DM 原理
│   │
│   ├── VPN技术/                         # 广域网与安全隧道
│   │   ├── 关于VPN.md                   # VPN 概念分类（L2VPN/L3VPN、Overlaid/Peer-to-Peer）
│   │   ├── IPSec/                       # IKEv1/v2 主模式/野蛮模式、AH/ESP 封装
│   │   └── MPLS/                        # 标签发布（LDP）、LSR 转发与 MPLS L3VPN
│   │
│   └── 网络设备虚拟化技术/
│       └── VRF.md                       # 虚拟路由转发（RD/RT 属性与多实例隔离）
│
└── 配置/                                # 设备命令行实操手册与注意事项
    ├── 注意.md                          # 实验刷题与真实设备配置注意事项
    ├── 交换/
    │   ├── VLAN.md                      # VLAN 划分与 Trunk 基础配置
    │   └── MSTP.md                      # 多生成树组与实例映射 CLI
    └── 路由/
        ├── 静态路由.md                  # 默认路由、浮动静态路由配置
        └── OSPF.md                      # 多区域 OSPF、认证与汇总配置
```
