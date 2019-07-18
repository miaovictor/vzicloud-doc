# 遍历用户组

## 接口描述

遍历用户组。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/frs/user/apps/:app_id/groups

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID

### URL参数

参数 | 类型 | 必填 | 说明
---|---|---|---
accesskey_id | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
expires | int | 是 | 参见[用户签名认证](/SIGNATURE.md)
signature | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
offset | int | 否 | 查询的起始位置，参见[遍历接口说明](/SCAN.md)
limit | int | 否 | 查询的条数，参见[遍历接口说明](/SCAN.md)
where | string | 否 | 查询的条件，参见[遍历接口说明](/SCAN.md)

### HTTP请求头

字段 | 值
---|---
Content-Type | application/json

### 请求参数

请求参数以Json格式放置于Body中，如下：

参数 | 类型 | 必填 | 说明 
---|---|---|---
group_id | string | 是 | 用户组Id（由数字、字母、下划线组成），长度限制48
group_name | string | 否 | 用户组名称
remark | string | 否 | 用户组备注

### 请求示例

```
POST https://api.vzicloud.com/v2/frs/user/apps/2/groups?accesskey_id=7fdaq37N1135Q1vK2e503HaLYXd1qVj4&expires=1561541184&signature=mF28sM7%2Fv5arqt4gRO7XLipdKDM%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"group_id":"test_group_01","group_name":"测试分组01","remark":"无"}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
app_id | int | 应用Id
group_id | string | 用户组Id
group_name | string | 用户组名称
remark | string | 用户组备注
create_time | int | 创建时间

### 返回示例

```
{
  "app_id": 2,
  "group_id": "test_group_01",
  "group_name": "测试分组01",
  "remark": "无",
  "create_time": 1563439927
}
```