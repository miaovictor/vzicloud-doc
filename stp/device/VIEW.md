# 获取设备信息

## 接口描述

根据设备序列号获取设备信息。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/stp/user/devices/:sn

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
sn | string | 是 | PATH中的`:sn`需要替换为具体的设备序列号

### URL参数

参数 | 类型 | 必填 | 说明
---|---|---|---
accesskey_id | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
expires | int | 是 | 参见[用户签名认证](/SIGNATURE.md)
signature | string | 是 | 参见[用户签名认证](/SIGNATURE.md)

### HTTP请求头

无

### 请求参数

无

### 请求示例

```
GET https://api.vzicar.com/v2/stp/user/device/b43ebdcb-fc88fc2f?accesskey_id=7dypI0Pg111567Er2YLD7aNIdoflxZ7N&expires=1569238328&signature=p58TFsf4KB4Dkvs5oM2ROAKzE6M%3D HTTP/1.1
Host: www.vzicar.com
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
id | int | Id
user_id | int | 用户Id
group_id | int | 分组Id
sn | string | 设备序列号
name | string | 设备名称
ip | string | 设备外网IP
ip_info | object | 设备外网IP的地址信息
+ country_name | string | 国家
+ region_name | string | 省份，区域
+ city_name | string | 城市
proxy | string | 代理服务器名称
board_version | string | 硬件版本
state | string | 设备状态，0：在线，1：离线
addition | object | 设备附加信息
+ version | string | 软件版本号
+ oem | string | oem厂商信息
+ mac | string | MAC地址
series_name | string | 系列名称
product_name | string | 产品名称
remark | string | 备注信息
create_time | int | 创建时间（Unix时间戳）
last_online_time | int | 最近一次上线时间（Unix时间戳）
last_offline_time | int | 最近一次离线时间（Unix时间戳）

### 返回示例

```
{
  "sn": "b43ebdcb-fc88fc2f",
  "id": 53527,
  "series_name": "RX",
  "addition": {
    "oem": "00.00.03.78.78.78.78",
    "mac": "58:e8:76:89:52:28",
    "version": "8.2.1.19082001"
  },
  "last_offline_time": 1567495976,
  "ip": "182.148.222.127",
  "user_id": 1,
  "board_version": 12363,
  "group_id": 0,
  "product_name": "车牌识别",
  "remark": "",
  "proxy": "proxy1",
  "last_online_time": 1567495933,
  "state": 1,
  "create_time": 1566533380,
  "name": "112.133",
  "ip_info": {
    "city_name": "成都",
    "country_name": "中国",
    "region_name": "四川"
  }
}
```