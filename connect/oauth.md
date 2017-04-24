## OAuth 授权过程

![](https://s.rokidcdn.com/homebase/upload/rJsJRvPCl.jpg)

## 交互过程：

- 用户添加驱动， 发起授权过程
- Homebase 向驱动调用 OAuth Command 接口， 参数为登陆回调页面地址
- HTTP 驱动 OAuth Command 返回 Oauth 登陆地址 `OAuth URL`
- Homebase 打开浏览器， 跳转到转到 `OAuth URL`
- 用户输入用户名和密码， 点击授权
- OAuth 服务授权完成， 跳转回 回调页面 `Callback URL`， 添加URL参数 （userId, userToken, expireTime, refreshToken）
- Homebase 保存授权信息， 下次用户调用 搜索设备和控制设备的时候会带上。


## 刷新 Token
- Homebase 检测到Token即将过期， 将现有的用户授权信息（userId, userToken, expireTime, refreshToken）发送给驱动的 `refreshToken` command
- 驱动返回新的用户授权信息
- Homebase 保存用户的授权信息

### FAQ

** Q: OAuth 返回的URL 参数可以自定义吗？ **

A: 可以自定义 userId, userToken, expireTime, refreshToken， 都可以使用自定义的名字。


** Q： 可以没有 refreshToken 吗？**

A： 可以, expireTime, refreshToken 为可选
