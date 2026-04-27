# BGP MPLAS IP VPN

MPLS VPN 是一种基于MPLS技术的IP VPN。（MPLS不等于MPLS VPN，只是MPLS VPN是MPLS比较知名的运用而已）

## MP-BGP/BGP-4+与MPLS

MP-BPG也叫BGP4+，是BGP-4的一种扩展，使其支持IPv6在内的其他非IPv4协议的网络层协议。RFC-2858和RFC-4760定义了MP-BGP协议。

详细可见``Datacom/理论/路由技术/BGP4+.md``

## MPLS VPN的构成

MPLS VPN可以分成控制平面和数据平面两部分：

控制平面由VRF,RD,RT等组成，数据平面由MPLS标签和IP数据包组成。

