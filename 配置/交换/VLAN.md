# VLAN

## 创建VLAN

```bash
# 创建VLAN
vlan <vlan_id(1-4094)>
# 批量创建VLAN
vlan batch <vlan_id(1-4094)> <vlan_id(1-4094)>……

#例如：
vlan 10
vlan batch 10-20
vlan batch 10 20 30 40
```

## VLAN端口组

```bash
# 华为：将端口加入临时组，对组内端口进行批量配置
port-group group-member <interface-list> # 例如 port-group group-member GigabitEthernet 0/0/1 to GigabitEthernet 0/0/10

# H3C 批量端口配置
interface range <interface-list> # 例如 interface range GigabitEthernet 1/0/1 to GigabitEthernet 1/0/10
# 或者使用命名范围
interface range name myPortRange interface GigabitEthernet 1/0/1 to GigabitEthernet 1/0/10
```
