# 人脸检测

## 接口描述

人脸检测。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/frs/user/apps/:app_id/faces/detect

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
POST https://api.vzicloud.com/v2/frs/user/apps/2/faces/detect?accesskey_id=7fdaq37N1135Q1vK2e503HaLYXd1qVj4&expires=1561541184&signature=mF28sM7%2Fv5arqt4gRO7XLipdKDM%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"image_type":"BASE64","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAw..."}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
face_num | int | 检测到的人脸数量
face_list | array | 检测到的人脸列表
+ face_probability | float | 人脸置信度，范围0-1
+ frontal_score | float | 正脸得分。**目前无效**
+ location | object | 人脸位置信息
++ left | int | 人脸区域离左边界的距离
++ top | int | 人脸区域离上边界的距离
++ width | int | 人脸区域的宽度
++ height | int | 人脸区域的高度
+ angel | object | 人脸旋转角度参数。**目前无效**
++ roll | float | 平面内旋转角[-180(逆时针), 180(顺时针)]
++ yaw | float | 三维旋转之左右旋转角[-90(左), 90(右)]
++ pitch | float | 三维旋转之俯仰角度[-90(上), 90(下)]

### 返回示例

```
{
  "face_num": 1,
  "face_list": [
    {
      "face_probability": 0.99989366531372,
      "frontal_score": 0,
      "location": {
        "left": 104,
        "top": 35,
        "width": 116,
        "height": 159
      },
      "angel": {
        "yaw": 0,
        "roll": 0,
        "pitch": 0
      }
    }
  ]
}
```