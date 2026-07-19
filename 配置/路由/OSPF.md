# OSPF

## OSPFv2配置

```bash
ospf 1 router-id 3.3.3.1 #创建ospf进程，router-id为3.3.3.1
ar 0 #进入区域0
network 2.2.2.0 0.0.0.255 #宣告2.2.2.0/24网段
```

## OSPFv3配置

```bash
ospfv3 1 # 创建OSPFv3进程
router-id 3.3.3.1 # 配置Router ID
```

## **更多命令：**

### 末梢区域配置

```bash
area 1
stub # 配置stub区域
q
area 2
stub no-summary # 配置为Totally stubby区域
q
area 3 
nssa # 配置为NSSA区域
# 可选附加参数：
# nssa translate-always (强制ABR进行Type-7转Type-5 LSA)
# nssa default-route-advertise (主动向区域内注入默认的Type-7 LSA)
q
area 4
nssa no-summary # 配置为Totally NSSA区域
```

### OSPF认证

```bash
# 配置接口明文认证
interface [接口名称]
ospf authentication-mode simple [纯文本密码]

# 配置接口 MD5 加密认证
interface [接口名称]
ospf authentication-mode md5 [key-id] [md5-密码]

# 配置区域明文认证
area [区域-id]
authentication-mode simple [纯文本密码]
```

### 其他

```bash
# 修改OSPF路由器之间的Hello和Dead时间
interface [接口名称]
ospf hello-interval [秒]
ospf dead-interval [秒]

# 配置OSPF接口的DR优先级
interface [接口名称]
ospf priority [优先级值]
```
