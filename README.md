# SAML

企业的SSO方案通常包含2部分:

1. SP
2. IdP

用户在访问SP之前需要认证, 为了避免访问不同的SP时频繁输入密码, SP可以通过配置, 将认证统一转到IdP一侧进行处理. IdP会维护用户的认证状态, 并且将某些用户信息返回给SP. 常用的IdP包括PingFederate, AAD等.

在用户浏览器, SP, IdP三者的交互过程中, 就需要一种规范来规定交互过程中的request和response格式, 以便3者都能正确解析并通信. 这就是所谓的协议, 常用的协议包括SAML, OIDC等.

一个常见的SP发起的访问大致如下:

1. 浏览器访问SP的资源, SP弹出登录页面, 用户可以输入密码或者点击SSO登录.
2. 点击SSO按钮后, SP生成认证请求SAMLRequest返回给浏览器, 请求中包含了IdP的目标地址.
3. 浏览器收到上述认证请求后, 携带SAMLRequest自动重定向到IdP的目的地址.
4. IdP收到认证请求后, 会检查Cookies判断用户是否已经认证. 如果是, 跳到5; 否则让用户输入用户名/密码, 跳到5.
5. IdP解析并验证SAMLRequest, 获取ACS等信息, 生成SAMLResponse.
6. 浏览器收到SAMLResponse, 携带SAMLResponse重定向到SP的ACS.
7. SP验证SAMLResponse, 获取需要的用户信息.

#### Reference

1. [SAML 2.0](https://www.cnblogs.com/xiaosiyuan/p/8080515.html)
2. [How AAD identify user in AuthnRequest](https://stackoverflow.com/questions/70627478)
