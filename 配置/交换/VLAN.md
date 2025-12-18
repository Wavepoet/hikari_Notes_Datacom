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

## VLNA组

```bash
#可以将端口加入组，对组内端口进行批量配置
port-group group-member
#H3C批量配置 
interface range name myEthPort int e1/0/1 to e1/0/12
interface range name myEthPort
```
