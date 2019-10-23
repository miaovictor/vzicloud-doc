# 创建分组

## 接口描述

创建分组。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/stp/user/groups

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
name | string | 是 | 分组名称
parent_id | int | 否 | 父分组ID，默认为0
remark | string | 否 | 分组备注信息

### 请求示例

```
POST https://www.vzicar.com/v2/stp/user/groups?accesskey_id=7dypI0Pg111567Er2YLD7aNIdoflxZ7N&expires=1569239651&signature=UQXtHLLxUkUW%2BO1oEmM06SuzM1Q%3D HTTP/1.1
Host: www.vzicar.com
Content-Length: 50
Content-Type: application/json

{"name":"测试分组3","parent_id":0,"remark":""}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
id | int | 分组Id
parent_id | int | 父分组Id
user_id | int | 用户Id
name | string | 分组名称
remark | string | 分组备注信息
create_time | int | 创建时间（Unix时间戳）
### 返回示例

```
{
  "id": 12,
  "parent_id": 0,
  "user_id": 1,
  "name": "测试分组3",
  "remark": "",
  "create_time": 1569232451
}
```