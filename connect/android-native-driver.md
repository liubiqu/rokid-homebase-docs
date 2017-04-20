# Android Native Driver

Native Driver 主要是针对 **第三方厂商** 采用Android SDK的方式来对接 , 如是其他方式,请联系 [Smart Home Connect](mailto:smarthomeconnect@rokid.com)。

Native Driver 驱动 作为 Http Server 实现 获取/控制 设备。

本文档主要用针对第三方开发者开发可运行在Rokid设备上提供智能家居服务。

智能家居 通讯 交互图
<div align="center">
	<img src="../images/android_driver.jpeg" width="30%" height="30%"/>
</div>

1. Driver 通过 Url 请求 Core 获取端口号。
2. Core   返回端口号给 Driver, 后续通过该端口通讯。
3. Core   发送 登录授权/获取设备/控制请求。
4. Driver 返回 登录结果/设备列表/控制结果。

