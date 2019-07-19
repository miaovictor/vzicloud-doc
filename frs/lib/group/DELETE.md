# 删除用户组

## 接口描述

删除指定用户组，**此操作会删除该用户组下的所有用户信息，谨慎操作！**

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | DELETE | /v2/frs/user/apps/:app_id/groups/:group_id

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID
group_id | string | 是 | PATH中的`:group_id`需要替换为具体的用户组ID

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
DELETE https://api.vzicloud.com/v2/frs/user/apps/2/groups/test_group_01?accesskey_id=7fdaq37N1135Q1vK2e503HaLYXd1qVj4&expires=1561541184&signature=mF28sM7%2Fv5arqt4gRO7XLipdKDM%3D HTTP/1.1
Host: www.vzicloud.com
```

## 返回说明

如果成功，响应状态码为200