# 遍历人脸

## 接口描述

遍历指定用户的人脸列表。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/frs/user/apps/:app_id/groups/:group_id/users/:user_id/faces

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID
group_id | string | 是 | PATH中的`:group_id`需要替换为具体的用户组ID
user_id | string | 是 | PATH中的`:user_id`需要替换为具体的用户ID

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
GET https://api.vzicloud.com/v2/frs/user/apps/2/groups/test_group_01/users/guan_xiao_tong/faces?accesskey_id=7hSdi1Gx11552bwS2EqndCm0XZZHBFS0&expires=1563451115&signature=e6m1Lbd%2FbDOPtZHUVFXl8%2B2ulRM%3D HTTP/1.1
Host: www.vzicloud.com
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
total | int | 查询总数
results | array | 查询结果数组
+ app_id | int | 应用Id
+ group_id | string | 用户组Id
+ user_id | string | 用户Id
+ face_id | string | 人脸Id
+ location | string | 人脸在图片中的位置信息
+ format | string | 人脸图片的格式，比如`png`，`jpeg`
+ create_time | int | 创建时间

### 返回示例

```
{
  "total": 1,
  "results": [
    {
      "app_id": 2,
      "group_id": "test_group_01",
      "user_id": "guan_xiao_tong",
      "face_id": "e76e8a4c5efdd8cb8fad131f0ac5470e",
      "location": "{\"width\":149,\"left\":131,\"height\":204,\"top\":49}",
      "format": "jpeg",
      "create_time": 1563516170
    }
  ]
}
```