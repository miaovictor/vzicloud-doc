# 错误码

所有接口如果调用成功，则响应的HTTP状态码为200，并视具体接口而定是否返回数据；反之，响应的HTTP状态为非200（视具体错误而定），并返回如下结构的错误信息：
```
{
  "error_code": 1000,
  "error_message": "Request url is not exist!"
}
```
关于错误码的定义参见下表：

错误码 | 错误信息 | 错误分析
---|---|---
1000 | Request url is not exist! | 检查请求的URL是否正确
1001 | Authorization params missing! | `expires`、`signature`、`accesskey_id`三个参数缺一不可
1002 | Authorization expired! | 验证过期，可能是`AccessKey`过期，也可能是`expires`过期
1003 | Authorization params [expires] error! | 检查此参数格式是否正确
1004 | Authorization params [signature] error! | 签名计算错误，参考[用户签名认证](SIGNATURE.md) 章节
1005 | Authorization params [accesskey_id] error! | 请使用正确的`accesskey_id`
1006 | AccessKey has been disabled! | `AccessKey`被禁用了，联系ROOT用户更换
1007 | AccessKey refresh failed! | 刷新`AccessKey`失败，请确保一定是在登录后的1小时30分钟至2小时这个刷新窗口期执行刷新操作
1008 | Account is not exist! | 一般不会出现这个问题
1009 | Account has been disabled! | 账号被禁用了，联系ROOT用户吧
1010 | Access module is not exist! | 一般不会出现这个问题
1011 | Access module has been disabled! | 模块被禁用了，一般不会出现这个问题
1012 | Access module denied! | 无权访问这个模块，很可能你没开通这个模块
1013 | Access action is not exist! | 一般不会出现这个问题
1014 | Access action has been disabled! | 功能被禁用了，一般不会出现这个问题
1015 | Access action denied! | 无权访问这个功能，很可能你的ROOT用户没给你这个权限
1016 | Request rate exceed max qps limit! | 超出了QPS限制，您可能要放慢请求速率了
1017 | Request count exceed total limit! | 超出了总的请求次数，请联系臻识科技销售进行充值
1018 | Request count exceed daily limit! | 超出了每日免费次数，请联系臻识科技销售进行充值
1101 | Parse request content to json failed! | 你发送的Json数据很可能有问题
1102 | Decode base64 failed! | 解码Base64出错了，对照API协议文档认真检查一下
1103 | Request params error! | 发送的数据有问题，错误信息后面会跟上具体是哪个参数有问题，对照API协议文档认真检查一下
1104 | Login failed! | 登录失败，为了防止恶意登录，我不会告诉你具体错误原因的
1105 | This user is not allowed to login! | 不允许登录，联系ROOT用户吧
1106 | Request failed! | 请求失败，对照API协议文档认真检查一下
1107 | Not support! | 某些功能可能暂时没有提供支持
1108 | No compute server is available! | 没用计算服务器可用，联系臻识科技技术支持吧
1109 | Request compute server failed! | 请求计算服务器失败，联系臻识科技技术支持吧
1110 | Image decode failed! | 解码图片失败，请检查上传的图片格式是否正确
2101 | User is not exist! | 操作的用户不存在
2102 | User has been disabled! | 操作的用户被禁用了
2103 | User name was used! | 用户名已被使用
2104 | User email was used! | 用户邮箱已被使用
2201 | Module is not exist! | 操作的模块不存在
2202 | Module has been disabled! | 操作的模块被禁用了
2301 | Action is not exist! | 操作的功能不存在
2302 | Action has been disabled! | 操作的功能被禁用了
2401 | AccessKey is not exist! | 操作的AccessKey不存在
2402 | AccessKey has been disabled! | 操作的AccessKey被禁用了
3001 | Face detect failed! | 人脸检测失败
3002 | Face not detected! | 没有检测到人脸
3003 | Face feature extract failed! | 提取人脸特征失败
3004 | Face feature compare failed! | 对比人脸特征失败
3005 | Save image failed! | 保存人脸图片失败
3006 | View image failed! | 浏览人脸图片失败
3101 | Face app is not exist! | 人脸应用不存在
3201 | Face group is not exist! | 人脸分组不存在
3202 | Face group is already exist! | 人脸分组已经存在
3301 | Face user is not exist! | 人脸用户不存在
3302 | Face user is already exist! | 人脸用户已经存在
3401 | Face is not exist! | 人脸不存在
4001 | Plate detect failed! | 车牌检测失败
4002 | Plate not detected! | 没有检测到车牌
4101 | Plate app is not exist! | 车牌应用不存在
5001 | Device was bound! | 设备已经被绑定到其他账户了
5002 | Device is not exist! | 设备不存在
5003 | Device is not bind! | 设备还没有绑定
5101 | Device group is not exist! | 设备分组不存在
5201 | Board is not exist! | 硬件不存在
5301 | Device config is not exist! | 设备配置不存在
5302 | Device config is already used! | 设备配置已经被应用了
5303 | Device config is already cancelled! | 设备配置已经被取消了
5401 | Device upgrade is not exist! | 设备升级不存在
5402 | Device upgrade is already used! | 设备升级已经被应用了
5403 | Device upgrade is already cancelled! | 设备升级已经被取消了
5501 | Device whitelist is not exist! | 设备白名单不存在
5502 | Device whitelist is already used! | 设备白名单已经被应用了
5503 | Device whitelist is already cancelled! | 设备白名单已经被取消了