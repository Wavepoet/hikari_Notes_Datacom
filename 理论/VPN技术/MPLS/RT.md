# RT(Route Target,路由目标)

RT是一种BGP扩展团体属性，决定了VPN路由该在哪些VRF之间流动。

在MPLS VPN中，PE为了隔离不同客户的路由，会为每个客户创建独立的VRF,在传递客户的路由时，便需要对路由路由条目进行区分，以可以分辨那条路由条目是哪给VRF的。

## ERT与IRT

### ERT(Export RT)

当本端PE发送某个VRF的路由时，会给这些路由打上特定的 ExportRT标签。

### IRT(Import RT)

当对端PE收到MP-BGP路由时，会检查路由携带的RT。如果该 RT与对端某个VRF配置的Import RT完全匹配，该路由才会被允许注入到该VRF的路由表 中；否则直接丢弃。

## RT tag

RT值的格式通常由“自治系统号(ASN):用户自定义数字”或“IP地址:用户自定义数字”等构成。在设备上，一个VPN实例的典型配置如下：

```bash
ip vrf CUSTOMER_A
 rd 65000:1
 route-target export 65000:100    # 为发出的路由打上标签
 route-target import 65000:100    # 接收并导入带有该标签的路由
```

这个例子定义了一个VPN实例，它发出的路由会携带RT 65000:100，同时也会接收所有带有相同RT值的路由。
