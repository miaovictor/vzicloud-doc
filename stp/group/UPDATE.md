# 更新分组

## 接口描述

根据分组ID更新分组信息。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | PUT | /v2/stp/user/groups/:group_id

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

字段 | 值
---|---
Content-Type | application/json

### 请求参数

请求参数以Json格式放置于Body中，如下：

参数 | 类型 | 必填 | 说明 
---|---|---|---
name | string | 否 | 分组名称
parent_id | int | 否 | 父分组ID，默认为0
remark | string | 否 | 分组备注信息

### 请求示例

```
PUT https://www.vzicar.com/v2/stp/user/groups/12?accesskey_id=7dK3qlar1115drSr2ew5N13etydlHlwn&expires=1569300606&signature=%2FLfu88AKh3KkRtaRQROM7zlVcgE%3D HTTP/1.1
Host: www.vzicar.com
Content-Length: 39
Content-Type: application/json

{"name":"测试分组3","remark":"无"}
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
  "remark": "无",
  "create_time": 1569232451
}
```