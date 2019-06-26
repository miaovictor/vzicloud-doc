# 用户签名认证

臻识科技AI开放平台的所有接口使用`AccessKeyId`及`AccessKeySecret`对称加密的方法来验证某个请求的发送者身份。`AccessKeyId`用于标示用户；`AccessKeySecret`是用户用于加密签名字符串和服务器用来验证签名字符串的密钥，且AccessKeySecret必须保密。

当用户想以个人身份向服务器发送请求时，首先需要将发送的请求按照指定的格式生成签名字符串；然后使用`AccessKeySecret`对签名字符串进行加密产生验证码。服务器收到请求以后，会通过`AccessKeyId`找到对应的`AccessKeySecret`，以同样的方法提取签名字符串和验证码，如果计算出来的验证码和提供的一样即认为该请求是有效的；否则，服务器将拒绝处理这次请求，并返回错误。

## 实现方式

### URL签名示例

```
POST https://api.vzicloud.com/v2/prs/user/apps?accesskey_id=7ffG6UFo1135QXbK2gVuiJffadN1YXZC&expires=1561463558&signature=8CXL%2BbRJ%2BWaDQrwg7wWxkdEok0Y%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 28
Content-Type: application/json

{"name":"测试应用","remark":"无"}
```
其中，必须至少包含`expires`、`accesskey_id`、`signature`这三个参数，除此之外根据不同的接口做相应的变化。
- **expires**: 这个参数的值是一个[UNIX时间](https://baike.baidu.com/item/unix%E6%97%B6%E9%97%B4%E6%88%B3/2078227?spm=a2c4g.11186623.2.17.27f86928Bmhme9&fr=aladdin)（自UTC时间1970年1月1号开始的秒数），用于标识该URL的超时时间。如果服务器接收到这个URL请求的时候晚于签名中包含的`expires`参数时，则返回请求超时的错误。为了安全起见，请尽可能设置一个较短的过期时间，比如2分钟。
- **accesskey_id**: 即`AccessKeyId`。
- **signature**: 表示签名信息。

### signature计算方式

```
signature = urlencode(base64(hmac-sha1(AccessKeySecret,
          VERB + "\n" 
          + CONTENT-MD5 + "\n" 
          + CONTENT-TYPE + "\n" 
          + EXPIRES + "\n"
          + CanonicalizedResource)))
```

- **AccessKeySecret**: 表示签名所需要的密钥。
- **VERB**: 表示`HTTP`请求的方法，主要有`GET`、`POST`、`PUT`、`DELETE`等，注意必须是大写。
- **\n**: 表示换行符。
- **CONTENT-MD5**: 表示请求内容数据的`MD5`值，对消息内容（不包括头部）计算`MD5`值获得128比特位数字，对该数字进行`base64`编码而得到。该请求头可用于消息合法性的检查（消息内容是否与发送时一致），如”eB5eJF1ptWaXm4bijSPyxw==”，也可以为空。详情请参见[RFC2616 Content-MD5](https://www.ietf.org/rfc/rfc2616.txt?spm=a2c4g.11186623.2.25.3915734ccG95Ff&file=rfc2616.txt)。
- **CONTENT-TYPE**: 表示请求内容的类型，如”`application/json`”，如果请求中没有数据，则这个值为空，如果请求中携带了数据，则一定要携带这个值。
- **EXPIRES**: 与上面的`expires`一样。
- **CanonicalizedResource**: 表示用户想要访问的资源。

其中有几点规则需要注意：

- 签名的字符串必须为`UTF-8`格式。含有中文字符的签名字符串必须先进行`UTF-8`编码，再与 `AccessKeySecret`计算最终签名。
- 签名的方法用[RFC 2104](http://www.ietf.org/rfc/rfc2104.txt?spm=a2c4g.11186623.2.30.3915734ccG95Ff&file=rfc2104.txt)中定义的`HMAC-SHA1`方法，其中`Key`为`AccessKeySecret`。
- 服务器先验证请求时间是否晚于expires时间，然后再验证签名。
- 将签名字符串放到`URL`时，注意要对`URL`进行`urlencode`。

### 构建CanonicalizedResource的方式

用户发送请求中想访问的服务器目标资源被称为`CanonicalizedResource`。它的构建方法如下：

- 将`CanonicalizedResource`置成空字符串；
- 放入要访问的资源（也就是`URL`里面的`Path`部分，针对上面的签名示例，就是`/v2/prs/user/apps`）；
- 如果用户请求`URL`包含了参数（`QueryString`，也叫`Http Request Parameters`），先在`CanonicalizedResource`字符串尾添加 `?`，**然后再将这些参数名按照字典序，从小到大排列，以 `&` 为分隔符**，按顺序添加到`CanonicalizedResource`中，其中要注意几点：
    - 如果没有包含参数，不需要添加 `?`。
    - 注意参数名的大小写问题。
    - `signature`，`expires`，`accesskey_id`这三个参数不包含在内，`signature`很好理解，因为此时签名还没计算出来，特别注意的是`expires`、`accesskey_id`。
    - 注意，此时**不要**对参数值进行`urlencode`。

针对上面的示例，完整的`CanonicalizedResource`为：`/v2/prs/user/apps`，此示例中并没有请求参数，假如有三个参数`name=名称&age=20&id=1`的话，那么此时，完整的`CanonicalizedResource`为：`/v2/prs/user/apps?age=20&id=1&name=名称`。

### 完整演示

针对前面的示例，接下来演示整个计算步骤：

**0. 前置条件**
- 本示例中，约定AccessKey如下：
    - AccessKeyId: `7ffG6UFo1135QXbK2gVuiJffadN1YXZC`
    - AccessKeySecret: `m4b4gQc0hur8okz7rsR7pLJkoH4OMLYj`
- 本示例中的`Body Data`采用紧凑型的`Json`格式。

**1. 计算CONTENT-MD5**
- `Body Data`为 `{"name":"测试应用","remark":"无"}`
- 按照上面`CONTENT-MD5`相关说明计算出结果为：`J2bREIXRh58BwcSkG9YNQQ==`

**2. 计算CanonicalizedResource**
- 针对以上示例，要访问的资源为：`/v2/prs/user/apps`
- 由于没有其他参数，所以最终结果为： `/v2/prs/user/apps`

**3. 计算CanonicalString**

`CanonicalString`为将要加密的字符串，格式为：

```
VERB + "\n" 
+ CONTENT-MD5 + "\n" 
+ CONTENT-TYPE + "\n" 
+ EXPIRES + "\n"
+ CanonicalizedResource
```
针对这个格式及以上计算出的结果，可以拼接出`CanonicalString`为：
```
POST\nJ2bREIXRh58BwcSkG9YNQQ==\napplication/json\n1561463558/v2/prs/user/apps
```

**4. 计算signature**

- 将`CanonicalString`转换为UTF-8编码，然后进行`HmacSHA1`加密，再进行`Base64`编码，得到结果为：`8CXL+bRJ+WaDQrwg7wWxkdEok0Y=`

**5. 生成完成的URL**

针对以上计算的结果，我们可以生成一个完整的`URL`，注意针对每一个参数值要进行URL编码,最终结果如下：
```
https://api.vzicloud.com/v2/prs/user/apps?accesskey_id=7ffG6UFo1135QXbK2gVuiJffadN1YXZC&expires=1561463558&signature=8CXL%2BbRJ%2BWaDQrwg7wWxkdEok0Y%3D
```
至此，一个完整的步骤就完成了！

