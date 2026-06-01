# RT(Route Target,路由目标)

RT是一种BGP扩展团体属性，决定了VPN路由该在哪些VRF之间流动。

在MPLS VPN中，PE为了隔离不同客户的路由，会为每个客户创建独立的VRF,在传递客户的路由时，便需要对路由路由条目进行区分，以可以分辨那条路由条目是哪给VRF的。

## ERT与IRT

### ERT(Export RT)

当本端PE发送某个VRF的路由时，会给这些路由打上特定的 ExportRT标签。

ERT 是一个需要发送出去的 Tag 。

### IRT(Import RT)

当对端PE收到MP-BGP路由时，会检查路由携带的RT。如果该 RT与对端某个VRF配置的Import RT完全匹配，该路由才会被允许注入到该VRF的路由表中；否则直接丢弃。在此过程中不传递 IRT,也就是说 IRT 是一个本地的 Tag ，他不会被发送出去。

那么便有了问题，IRT 是如何产生的？（感觉好 AI）

IRT 是手动配置的，当需要大规模配置 IRT 的时候便只能使用 Ansible、Salt 这类自动化工具去配置或者使用 SD-WAN 控制器去配置了。（很难想象）

AI 说的，有待查证：

> - **Hub-Spoke 拓扑**中，Spoke 希望接收 Hub 的路由（Import RT = Hub 的 Export RT），但**不希望接收其他 Spoke 的路由**（即使那些 Spoke 的 Export RT 与自己 Import RT 相同也不行，因为没配置）。如果自动学习所有看到的 Export RT，就会意外引入其他分支的路由，破坏隔离。
>     
> - **Extranet 场景**中，只有特定伙伴的 Export RT 才被允许导入，而不是所有
## RT tag

RT值的格式通常由“自治系统号(ASN):用户自定义数字”或“IP地址:用户自定义数字”等构成。例如 ``65000：100``，``192.168.1.1：100``。


```bash
ip vrf CUSTOMER_A
 rd 65000:1
 route-target export 65000:100    # 为发出的路由打上标签
 route-target import 65000:100    # 接收并导入带有该标签的路由
```


## RT 约束路由分发（RT Constrained Route Distribution, RTC）

> RT约束路由分发（RT Constrained Route Distribution，简称 RTC）是一种BGP增强功能，用于优化MPLS VPN网络中路由的分发效率，减少不必要的路由更新和资源消耗[](https://www.cisco.com/c/en/us/td/docs/routers/ios-xe/ip-routing/b-ip-routing/m_irg-rt-filter-0.html)。
> 
> 传统的MPLS VPN网络中，路由反射器（RR）习惯把所有的VPNv4/v6路由一股脑地发给所有PE设备[](https://www.cisco.com/c/zh_cn/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.pdf#1#1)。哪怕某个PE上根本没有需要这条路由的VPN，它也得先接收下来，再通过Import RT规则进行过滤丢弃[](https://community.cisco.com/t5/mpls/rt-constrained-route-distribution-restrictions/td-p/3902499)。这不仅浪费了PE设备的内存和处理能力，也占用了带宽[](https://www.cisco.com/c/zh_cn/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.pdf#1#1)。
> 
> RTC的核心思想是变“被动接收并丢弃”为“主动按需索取”[](https://www.cisco.com/c/zh_cn/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.pdf#1#1)。
> 
> RTC的工作流程主要分为三步：
> 
> ### 📢 第一步：PE“订阅”
> 
> PE设备会检查自己所有VRF下配置的**Import RT列表**，汇总成一个“我关心的路由列表”[](https://www.cisco.com/c/zh_cn/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.pdf#1#1)。
> 
> ### 🧾 第二步：PE“下单”
> 
> PE将这个列表通过一个新的BGP地址族——`rtfilter`（路由目标过滤地址族）——打包成一条特殊的**RTC路由**（RT-Constrain路由）发送给它的BGP邻居（比如RR）[](https://community.cisco.com/t5/mpls/rt-constrained-route-distribution-restrictions/td-p/3902499)[](https://www.cisco.com/c/zh_cn/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.pdf#1#1)。
> 
> ### 🔐 第三步：RR“按需发货”
> 
> 当RR收到这条RTC路由后，它会解析出里面包含的RT值，并为发出请求的PE生成一个出站路由过滤器（Outbound Route Filter）。之后，RR只会把携带这些RT值的VPN路由发送给该PE，其他无关路由则不再转发[](https://www.cisco.com/c/zh_cn/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.pdf#1#1)[](https://test-gsx.cisco.com/c/en/us/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.html)。
> 
> 这个机制由**RFC 4684**定义，在VRF数量庞大或PE设备众多的网络中尤其有用，能大幅提升网络的可扩展性[](https://test-gsx.cisco.com/c/en/us/support/docs/multiprotocol-label-switching-mpls/mpls/116062-technologies-technote-restraint-00.html)。