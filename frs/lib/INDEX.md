# 人脸库管理

人脸库相关接口，要完成1：N的人脸搜索，首先需要构建一个人脸库，用于存放所有人脸特征，相关接口如下：

### 用户组
* [创建用户组](group/CREATE.md)
* [修改用户组](group/UPDATE.md)
* [删除用户组](group/DELETE.md)
* [查看用户组](group/VIEW.md)
* [遍历用户组](group/SCAN.md)

### 用户
* [创建用户](user/CREATE.md)
* [修改用户](user/UPDATE.md)
* [删除用户](user/DELETE.md)
* [查看用户](user/VIEW.md)
* [遍历用户](user/SCAN.md)

### 人脸
* [创建人脸](face/CREATE.md)
* [删除人脸](face/DELETE.md)
* [遍历人脸](face/SCAN.md)
* [人脸注册（百度云接口）](face/REGISTER.md)
* [人脸更新（百度云接口）](face/UPDATE.md)
* [人脸图片预览](face/IMAGE.md)

人脸库（应用）、用户组、用户、用户的人脸这四者的**层级关系**如下所示：
```
|- 人脸库(app_id)
   |- 用户组一（group_id）
      |- 用户01（uid）
         |- 人脸（faceid）
      |- 用户02（uid）
         |- 人脸（faceid）
         |- 人脸（faceid）
         ....
       ....
   |- 用户组二（group_id）
   |- 用户组三（group_id）
   ....
```
关于人脸库的限制：
- 每个开发者账号可以创建100个人脸库（应用）
- 每个应用对应一个人脸库，且不同应用之间，人脸库互不相通；
- 每个人脸库下，可以创建多个用户组，用户组（group）数量没有限制；
- 每个用户组（group）下，可添加无限个用户（user）；
- 每个用户（user）下，可以添加无限个人脸（face）；