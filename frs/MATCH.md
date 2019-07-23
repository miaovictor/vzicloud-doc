# 人脸比对

## 接口描述

该请求用于比对**两张图片**中的人脸相似度并返回比对的得分，可用于判断两张脸是否是同一人的可能性大小。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/frs/user/apps/:app_id/faces/match

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
images | array | 是 | 图片数组
+ image_type | string | 是 | 图片类型，固定为`BASE64`
+ image | string | 是 | 图片的Base64编码字符串，**切记需要去掉前缀`data:image/jpeg;base64`，并且确保图片大小在2M以内，分辨率小于等于1920(宽)x1080(高)！**

### 请求示例

```
POST https://api.vzicloud.com/v2/frs/user/apps/2/faces/match?accesskey_id=7fdaq37N1135Q1vK2e503HaLYXd1qVj4&expires=1561541184&signature=mF28sM7%2Fv5arqt4gRO7XLipdKDM%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"images":[{"image_type":"BASE64","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAw..."},{"image_type":"BASE64","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAw..."}]}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
score | float | 比对得到的分数，范围0-1

### 返回示例

```
{
  "score": 0.74614328145981
}
```