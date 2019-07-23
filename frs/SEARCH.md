# 人脸搜索

## 接口描述

在指定的集合中搜索用户人脸。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/frs/user/apps/:app_id/faces/search

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

### HTTP请求头

字段 | 值
---|---
Content-Type | application/json

### 请求参数

请求参数以Json格式放置于Body中，如下：

参数 | 类型 | 必填 | 说明 
---|---|---|---
image_type | string | 是 | 图片类型，固定为`BASE64`
image | string | 是 | 图片的Base64编码字符串，**切记需要去掉前缀`data:image/jpeg;base64`*，并且确保图片大小在2M以内，分辨率小于等于1920(宽)x1080(高)！**
group_id_list | string | 是 | 分组Id，多个分组用;分割
max_user_num | int | 否 | 查找后返回的用户数量，默认为1

### 请求示例

```
POST https://api.vzicloud.com/v2/frs/user/apps/2/faces/search?accesskey_id=7fdaq37N1135Q1vK2e503HaLYXd1qVj4&expires=1561541184&signature=mF28sM7%2Fv5arqt4gRO7XLipdKDM%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"image_type":"BASE64","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAw...","group_id_list":"test_group_01"}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
user_list | array | 找到用户列表
+face_id | string | 比对的人脸ID
+group_id | string | 用户所属分组ID
+user_id | string | 用户ID
+user_name | string | 用户名称
+user_info | string | 用户信息
+user_remark | string | 用户备注
+score | float | 比对得到的分数，范围0-1

### 返回示例

```
{
  "user_list": [
    {
      "face_id": "43ae4662140edfb735c2294b78e6f0bf",
      "group_id": "test_group_01",
      "user_id": "guan_xiao_tong",
      "user_name": "关晓彤",
      "user_info": "关晓彤",
      "user_remark": "关晓彤",
      "score": 0.42928117513657
    }
  ]
}
```