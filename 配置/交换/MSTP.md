# MSTP

开启MSTP

```bash
stp mode mstp
```

配置MSTP

```bash
# 进入MSTP区域配置模式
stp region-configuration
# 将vlan和MSTI绑定
instance 1 vlan 10 # 将VLAN 10绑定到实例 1
instance 2 vlan 20 # 将VLAN 20绑定到实例 2
qu
# 配置MSTP优先级
stp instance 1 root primary  # MSTI 1为主根
stp instance 2 root secondary  # MSTI 2为备根

# 开启边缘端口和BPDU保护
int g 0/0/0
stp edged-port enable
stp bpdu-protection
```
