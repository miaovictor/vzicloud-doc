# 车牌识别

## 接口描述

车牌识别。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/prs/user/apps/:app_id/plates/detect

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
image | string | 是 | 图片的Base64编码字符串，**切记需要去掉前缀`data:image/jpeg;base64`**

### 请求示例

```
POST https://api.vzicloud.com/v2/prs/user/apps/2/plates/detect?accesskey_id=7fdaq37N1135Q1vK2e503HaLYXd1qVj4&expires=1561541184&signature=mF28sM7%2Fv5arqt4gRO7XLipdKDM%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"image_type":"BASE64","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAw..."}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
location | object | 车牌在图片中的位置信息
+ left | int | 车牌距离图片左边的距离
+ top | int | 车牌距离图片右边的距离
+ width | int | 车牌的宽度
+ height | int | 车牌的高度
plate | string | 检测到车牌号
score | float | 车牌置信度，范围0-1
decode_base64_msec | int | 解码Base64所用时间，单位：毫秒
decode_image_msec | int | 解码图片所用时间，单位：毫秒
detect_plate_msec | int | 车牌识别所用时间，单位：毫秒

### 返回示例

```
{
  "location": {
    "left": 468,
    "top": 877,
    "height": 52,
    "width": 211
  },
  "plate": "ATW5880",
  "score": 0.95580637454987,
  "decode_base64_msec": 1,
  "decode_image_msec": 13,
  "detect_plate_msec": 42
}
```