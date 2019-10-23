# 删除分组

## 接口描述

根据分组ID删除分组信息，如果被删除的分组下有子分组，会将这些子分组的`parent_id`置为0，如果被删除的分组下有设备，会将这些设备的`group_id`置为0。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | DELETE | /v2/stp/user/groups/:group_id

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
DELETE https://www.vzicar.com/v2/stp/user/groups/12?accesskey_id=7dK3qlar1115drSr2ew5N13etydlHlwn&expires=1569300606&signature=%2FLfu88AKh3KkRtaRQROM7zlVcgE%3D HTTP/1.1
Host: www.vzicar.com
```

## 返回说明

如果成功，响应状态码为200