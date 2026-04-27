# MSTP

开启MSTP

```bash
stp mode mstp
```

配置MSTP

```bash
# 进入MSTP区域配置模式
stp region-configuration
# 将vlan和MSIT绑定
instance 1 vlan 10 #vlan 1绑定MSTI 10
instance 2 vlan 20
qu
# 配置MSTP优先级
stp instance  1 root  primary  #MSTI 1为主跟
stp instance  2 root  secondary  #MSTI 2 为备根

# 开启EB保护
int g 0/0/0
stp edged-port enable
stp bpdu-protection
```
