# 人脸图片预览

## 接口描述

预览指定人脸图片。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/frs/user/apps/:app_id/faces/image/:image_name

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID
image_name | string | 是 | PATH中的`:image_name`需要替换为具体的人脸图片文件名

**注意**: 人脸图片的文件名为: `${face_id}.${format}`

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
GET https://api.vzicloud.com/v2/frs/user/apps/2/faces/image/142b44786b680dce4de760aa45598597.jpeg?accesskey_id=7iO02agl1165hSHT2vlTVgQpbZ3PE4ia&expires=1563531349&signature=k9r95GP4hquQPHDWP2CU9OwPvjw%3D HTTP/1.1
Host: www.vzicloud.com
```

## 返回说明

成功即可看到图片。