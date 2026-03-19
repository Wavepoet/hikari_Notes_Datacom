# MP-BGP/BGP-4+

BGP-4的设计主要是针对IPv4的。MP-BPG是BGP-4的一种扩展，使其支持IPv6在内的其他非IPv4协议的网络层协议。RFC-2858和RFC-4760定义了MP-BGP协议。

## TLV

## MP-BGP新增的属性

在 MP-BGP中新引入了两个全新的不可变可选属性：

- MP_REACH_NLRI (Type 14，多协议可达路由信息)

用于发布可达路由信息以及对应的下一跳信息。


- MP_UNREACH_NLRI (Type 15，多协议不可达路由信息)


