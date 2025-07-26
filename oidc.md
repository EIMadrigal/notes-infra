# OIDC

OIDC作为另外一种认证协议, 也有3个参与者: 浏览器, SP, IdP. 一个典型的场景如下:

#### Step 1

用户在浏览器访问`https://app.com`, SP收到浏览器请求, 首先要对用户进行认证.

#### Step 2

如果SP配置了第三方认证, 通常会返回一个重定向的response给浏览器, 重定向的目标URL大致如下:

```
https://login.microsoftonline.com/common/oauth2/v2/authorize?response_type=code&client_id=12345&redirect_uri=https://app.com/v1/api/oidc/callback&scope=openid,profile,email&state=syl
```

1. `client_id`是SP预先在IdP上注册获得的编号.
2. `redirect_uri`是IdP返回授权码给浏览器后, 浏览器应该重定向到哪个地址, `redirect_uri`也需要提前在IdP注册.
3. `response_type`

#### Step 3

浏览器自动访问上述的重定向URL, 用户可能需要输入用户名/密码, 或者利用MFA, Primary Refresh Token等方式, 向IdP验证自己的身份. 如果IdP能直接从Cookies获取到用户身份, 就无需验证.

#### Step 4

IdP验证成功后, 返回另外一个重定向URL给浏览器, 即上面的`redirect_uri`, 并且包含了授权码authorization code:

```
https://app.com/v1/api/oidc/callback?code=pkzdZumQi1&state=syl
```

浏览器自动访问该URL, 向SP发起请求.

#### Step 5

SP从请求中获取授权码, 向IdP发起POST请求:

```
https://login.microsoftonline.com/common/oauth2/v2/token
```

Request body:

```
{
  grant_type: authorization_code,
  code: pkzdZumQi1,
  redirect_uri: https://app.com/v1/api/oidc/callback,
  client_id: 12345,
  client_secret: gravitational
}
```

1. `client_secret`用于SP向IdP表明自己的身份, 也可以用证书.

#### Step 6

IdP验证上述请求, 生成response给到SP:

```
{
  "id_token": "FW6AlBeyalZtDIRXxA0u5XBbZkLzj",
  "access_token": "IEZKr6ePPtxZBEd",
  "refresh_token": "xxxxxxx",
  "token_type": "bearer",
  "scope": "read:org",
  "expires_in": 3600
}
```

1. `id_token`是IdP签发的一种JWT, SP可以通过解码获取当前的用户信息.
2. `access_token`对当前认证的用户是透明的, 用于SP向其他的resource server请求资源时携带.
3. `refresh_token`

#### Step 7

SP解析上述的`id_token`, 获取当前用户信息:

```
{
  "sub": "steven",
  "email": "steven@google.com",
  "email_verified": "true"
}
```

如果通过`id_token` 获取的信息不够, SP可以利用`access_token` 访问IdP的userinfo endpoint, 获取更多的信息.



