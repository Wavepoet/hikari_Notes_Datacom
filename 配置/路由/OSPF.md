# OSPF

## OSPFv2配置

```bash
ospf 1 router-id 3.3.3.1 #创建ospf进程，router-id为3.3.3.1
ar 0 #进入区域0
network 2.2.2.0 0.0.0.255 #宣告2.2.2.0/24网段
```

## OSPFv3配置

```bash
router ospfv3 1
router-id 3.3.3.1
```

## **更多命令：**

### 末梢区域配置

```bash
area 1
stub #配置stub区域
q
area 2
stub no-summary #配置为Totally stubby区域
q
area 3 
nssa #配置为nssa区域
  - [translate-always | translate-never] #控制类型7 LSA的转换行为。
  - nssa default-route-advertise #ABR主动注入默认路由（Type 7）
q
area 4
nssa nssa no-summary #配置为Totally nssa区域
```

### OSPF认证

```bash
#配置ospf明文认证
interface [接口名称]
ospf authentication-mode simple [纯文本密码]
#配置ospf MD5加密认证
interface [接口密码]
ospf authentication-mode md5 [钥匙-id] [md5-密码]
#配置ospf区域明文认证
area [区域-id] authentication-mode simple [纯文本密码]

```

### 其他

```bash
#修改OSPF路由器之间的Hello和Dead时间
interface [接口名称]
ospf hello-interval [秒]
ospf dead-interval [秒]
#配置ospf邻居优先级
interface [接口名称]
ospf priority [优先级值]
```
