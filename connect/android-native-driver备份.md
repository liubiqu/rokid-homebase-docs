# Rokid Native Driver

我们主要针对的是**第三方厂商**用的 sdk. 如是其他方式,请联系 [Smart Home Connect](mailto:smarthomeconnect@rokid.com)
Native Driver 驱动 作为 http server 实现 获取/控制 设备
本文档主要用针对第三方开发者开发可运行在Rokid设备上提供智能家居服务。


##Rokid驱动介绍
- 驱动要作为一个httpserver存在,用于接收Rokid智能家居系统的相关请求。
- 驱动需要在用户使用Rokid手机app进行账号授权的时候提供验证账号的功能。
- 驱动需要在收到控制请求的时候去控制智能设备。
- 驱动需要在收到请求设备列表的时候返回当前所有设备信息。
- 以上操作均需按照Rokid文档返回Json格式数据的执行结果。


##Rokid驱动介绍
- [http server]()
- [/list]()
- [/get]()
- [/execute]()
- [/command]()


##Rokid驱动开发流程

- 获取端口号,默认的端口号获取地址是:<http://127.0.0.1:4201/native-driver/get-port?vendor=%1$s>,
  其中%1$s需要替换，如换成lifesmart
- 完成httpserver端开发,可以参考sample代码,开发好了后,联系Rokid人员发布驱动dev版本。[sample]()
- 配置Rokid设备智能家居开发环境:adb shell setprop persist.system.rokid.homebase.env dev 。
- 在浏览器打开Rokid智能家居开发者页面（Rokid设备IP地址+端口号）,如:<10.88.8.88:4201/>;按照提示登录Rokid开发界面,添加驱动,添加账号,搜索设备。[开发者页面](../develop/develop.md)
- 配合开发者页面实现驱动的控制、登录请求等开发。[开发者页面](../develop/develop.md)


#驱动开发提示
需要提供 3个文件给rokid人员,
- driver.json
- README_zh.md
- README_en.md

- package.json 
	- apkDependencies : 表示驱动依赖的其它apk文件,无依赖可不填写
	- name : 驱动的apk文件名
	- version : 驱动当前的版本
	- main : 主驱动的apk文件
	- files : 主驱动 和 依赖 apk 的文件名称

```JSON
{
	"apkDependencies":["Robot-release.apk","UpnpService-release.apk"],
	"name":"driver-sample",
	"version":"1.0.0",
	"main":"native-driver-sample.apk",
	"files":["native-driver-sample.apk","Robot-release.apk","UpnpService-release.apk"]
}
```

```
2、需提供三个文件,目前需要给到rokid这边。分别是:driver.json,README_en.md,README_zh.md,具体如下图
   一定要注意,driver.json里面的vendor属性和驱动获取端口号的vendor需保持一致,且actionName需要与驱动
   manifest配置的驱动入口的action保持一致,packageName也需要与驱动的包名保持一致！！！
```
 - driver.json 说明: 
	 - vendor : 厂商英文名称 ,vendor属性和 驱动获取端口号的vendor需保持一致;
	 - type : 驱动类型 ,安卓默认为 native ;
	 - maxAccount : 最大登录账号数量 0 表示不限制;
	 - authType : 授权类型 ;
	 - icon : 图标 ;
	 - zh : 中文名称 ; 
	 - ch : 英文名称 ; 
	 - actionName : 需要与驱动 manifest配置的驱动入口的action保持一致,
	 - packageName : 也需要与驱动的包名保持一致 ;

```JSON
{
	  "vendor": "sample",
	  "type": "native",
	  "maxAccount": 1,
	  "authType": "password",
	  "icon": "https://www.xxxx.com",
	  "i18n": {
	    "zh": {
	      "name": "样本"
	    },
	    "en": {
	      "name": "sample"
	    }
	  },
	  "actionName": "com.rokid.homebase.driver.sample",
	  "packageName": "com.rokid.homebase.driver.sample"
}
```
 
 - README_zh.md 和 README_en.md 

 说明 : 填写Driver 支持的设备类型,以及产品名称 的中英文版

```
目前支持的设备
- 灯
   - 智能灯泡
   - 幻彩灯带
- 开关
   - 流光开关
- 插座
   - WiFi插座
   - 入墙插座
- 空气净化器
- 红外发射器
   - 电视
   - 空调
   - 风扇
```