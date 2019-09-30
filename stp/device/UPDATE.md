# 更新设备

## 接口描述

更新设备信息，可一次性更新多台。。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | PUT | /v2/stp/user/devices

### PATH参数

无

### URL参数

参数 | 类型 | 必填 | 说明
---|---|---|---
accesskey_id | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
expires | int | 是 | 参见[用户签名认证](/SIGNATURE.md)
signature | string | 是 | 参见[用户签名认证](/SIGNATURE.md)

### HTTP请求头

字段 | 值
---|---
Content-Type | application/json

### 请求参数

请求参数以Json格式放置于Body中，如下：

参数 | 类型 | 必填 | 说明 
---|---|---|---
devices | array | 是 | 设备数组
+ sn | string | 是 | 设备序列号
+ group_id | int | 否 | 分组Id
+ remark | string | 否 | 备注信息

### 请求示例

```
PUT https://api.vzicar.com/v2/stp/user/groups?accesskey_id=7dK3qlar1115drSr2ew5N13etydlHlwn&expires=1569300606&signature=%2FLfu88AKh3KkRtaRQROM7zlVcgE%3D HTTP/1.1
Host: www.vzicar.com
Content-Length: 39
Content-Type: application/json

{"devices":[{"sn":"2a835e70-324a98ed","group_id":0,"remark":""}]}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
successes | array | 成功列表
+ sn | string | 设备序列号
+ group_id | int | 分组Id
+ remark | string | 备注信息
failures | array | 失败列表
+ sn | string | 设备序列号
+ group_id | int | 分组Id
+ remark | string | 备注信息
+ error | object | 错误
++ code | int | 错误码
++ message | string | 错误信息

### 返回示例

```
```
{
  "successes": [
    {
      "remark": "",
      "sn": "2a835e70-324a98ed",
      "group_id": 0
    }
  ],
  "failures": []
}
```