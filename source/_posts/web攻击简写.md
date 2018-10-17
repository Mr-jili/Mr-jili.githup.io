---
title: web攻击简介
data: 2018/9/10 17:00
categories:
- Diary
tags:
- XSS
- WEB
---
#### Web攻击技术，如何防止被攻击

##### 攻击：

+ XSS（Cross-Site Scripting，跨站脚本攻击）：指通过存在安全漏洞的Web网站注册用户的浏览器内运行非法的HTML标签或者JavaScript进行的一种攻击。
+ SQL 注入攻击：通过表单提交可运行的 sql 语句，以破坏数据库数据。
+ CSRF（Cross-Site Request Forgeries，跨站点请求伪造）：指攻击者通过设置好的陷阱，强制对已完成的认证用户进行非预期的个人信息或设定信息等某些状态更新。
+ dDos 拒绝服务攻击：通过大量请求疯狂占用服务器资源至其瘫痪。
+ CDN 攻击：使用不合理数据发起请求或请求不合理接口。
+ 身份伪造：冒充服务器或用户获取从另一方获取信息。

##### 防御：

+ XSS:
1.输入验证，过滤标签、事件、脚本、SQL
2.http头： X-XSS-Protection
3.cookie保护：set-cookie 头加入 http-only
+ SQL 注入
1.输入验证，过滤标签、事件、脚本、SQL
2.数据库权限最小化
3.使用接口而非 SQL 语句
4.限制文件上传类型
+ CSRF
1.验证码
2.验证 http 头 referer 项
3.在 http 中加入 taken
+ 身份伪造
1.隐藏敏感信息
2.加密
3.session 定期失效
4.权限验证、中间件校验
5.数字签名
6.CA 证书校验
+ dDos 拒绝服务攻击
1.流量防火墙
2.验证码
+ CDN 攻击
1.对版本控制进行Hash验证
2.跳转验证（重定向验证）