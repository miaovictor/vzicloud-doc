# 遍历分组

## 接口描述

遍历分组列表。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/stp/user/groups

### PATH参数

无

### URL参数

参数 | 类型 | 必填 | 说明
---|---|---|---
accesskey_id | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
expires | int | 是 | 参见[用户签名认证](/SIGNATURE.md)
signature | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
offset | int | 否 | 参见[遍历接口说明](/SCAN.md)
limit | int | 否 | 参见[遍历接口说明](/SCAN.md)
where | string | 否 | 参见[遍历接口说明](/SCAN.md)

可用于`where`条件筛选的字段有：
- id
- parent_id
- name
- remark
- create_time


### HTTP请求头

无

### 请求参数

无

### 请求示例

```
GET https://api.vzicar.com/v2/stp/user/groups?offset=0&limit=10&where=W3sibmFtZSI6InBhcmVudF9pZCIsInZhbHVlIjowLCJvcGVyIjoiZXEifV0%3D&accesskey_id=7dypI0Pg111567Er2YLD7aNIdoflxZ7N&expires=1569238328&signature=p58TFsf4KB4Dkvs5oM2ROAKzE6M%3D HTTP/1.1
Host: www.vzicar.com
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
offset | int | URL参数中的offset值
limit | int | URL参数中的limit值
total | int | 查询总数
results | array | 查询结果数组
+ id | int | 分组Id
+ parent_id | int | 父分组Id
+ user_id | int | 用户Id
+ name | string | 分组名称
+ remark | string | 分组备注信息
+ create_time | int | 创建时间（Unix时间戳）

### 返回示例

```
{
  "results": [
    {
      "id": 4,
      "parent_id": 0,
      "user_id": 1,
      "name": "测试分组01"，
      "remark": "",
      "create_time": 1568014091
    },
    {
      "id": 9,
      "parent_id": 0,
      "user_id": 1,
      "name": "测试分组02"，
      "remark": "",
      "create_time": 1568788923
    }
  ],
  "limit": 10,
  "offset": 0,
  "total": 2
}
```