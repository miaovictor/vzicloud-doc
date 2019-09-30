# 绑定设备

## 接口描述

绑定设备到当前用户下，可一次性绑定多台。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/stp/user/devices

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
+ group_id | int | 否 | 分组Id，提供此值可将设备绑定到指定分组下，否则绑定到默认分组
+ remark | string | 否 | 备注信息

### 请求示例

```
POST https://api.vzicar.com/v2/stp/user/devices?accesskey_id=7dypI0Pg111567Er2YLD7aNIdoflxZ7N&expires=1569239651&signature=UQXtHLLxUkUW%2BO1oEmM06SuzM1Q%3D HTTP/1.1
Host: www.vzicar.com
Content-Length: 50
Content-Type: application/json

{"devices":[{"sn":"b43ebdcb-fc88fc2f","group_id":4,"remark":"测试"},{"sn":"2a835e70-324a98ed","group_id":0,"remark":""},{"sn":"2a835e70-324a98et","group_id":0,"remark":"sfdfd"}]}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
successes | array | 成功列表
+ sn | string | 设备序列号
+ group_id | int | 分组Id，提供此值可将设备绑定到指定分组下，否则绑定到默认分组
+ remark | string | 备注信息
failures | array | 失败列表
+ sn | string | 设备序列号
+ group_id | int | 分组Id，提供此值可将设备绑定到指定分组下，否则绑定到默认分组
+ remark | string | 备注信息
+ error | object | 错误
++ code | int | 错误码
++ message | string | 错误信息

### 返回示例

```
{
  "successes": [
    {
      "remark": "",
      "sn": "2a835e70-324a98ed",
      "group_id": 0
    }
  ],
  "failures": [
    {
      "error": {
        "code": 5101,
        "message": "Device group is not exist!"
      },
      "remark": "测试",
      "sn": "b43ebdcb-fc88fc2f",
      "group_id": 4
    },
    {
      "error": {
        "code": 1103,
        "message": "Request params error!Param [sn] format error!"
      },
      "remark": "sfdfd",
      "sn": "2a835e70-324a98et",
      "group_id": 0
    }
  ]
}
```