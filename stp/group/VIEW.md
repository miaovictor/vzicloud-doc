# 获取分组信息

## 接口描述

根据分组ID获取分组信息。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/stp/user/groups/:group_id

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
group_id | int | 是 | PATH中的`:group_id`需要替换为具体的分组ID

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
GET https://www.vzicar.com/v2/stp/user/groups/12?accesskey_id=7dypI0Pg111567Er2YLD7aNIdoflxZ7N&expires=1569238328&signature=p58TFsf4KB4Dkvs5oM2ROAKzE6M%3D HTTP/1.1
Host: www.vzicar.com
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