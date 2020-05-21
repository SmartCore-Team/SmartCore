# SmartCore
一个智能家居设备管理平台。   
只负责管理设备并提供口子，不提供任何功能。

## 前言&设计初衷
玩智能家居有一段时间了，用了很多平台，也折腾了很多，但是始终不是我想要的。
其实只是想要一个：
1. 能把所有设备都接入其中，并且本身很轻量级的平台;
2. 通过上层app做加法提供功能，而不是平台本身很重有一堆功能让用户去做减法;
3. 配置自由灵活可以融入任何设备、任何类型、任何属性、任何规则。

## 架构
![](https://raw.githubusercontent.com/SmartCore-Team/SmartCore/master/images/framework.png)

## 名词解释
1. SmartCore: 指本平台。
2. Plugin: 插件，平台通过插件实现控制设备，是平台和设备之间沟通的桥梁。
3. Action: 接口，平台提供的服务，上层应用可以通过接口和平台交互。
4. Notify: 通知，平台主动推送消息。
5. App: 应用，使用平台资源的上层应用。

## 接口文档
### v1
||type|method|pluginList|deviceIdList|propertyIdList|operation|value|描述|例(json格式)|
|:-:|:-|:-|:-|:-|:-|:-|:-|:-|:-|
|1|info||||||||获取系统信息|{"type": "info"}|
|2|config||||||||获取配置信息|{"type": "config"}|

## Q&A
1. 为什么使用Java开发？
因为群里的Java程序员最多。

2. Java如何解决jar hell问题？
程序加载plugin未使用默认的class loader，查找class规则为优先查找jar包本身，后找其他。所以plugin开发者若使用向下兼容有问题的依赖jar时，请打包成uber jar(fat jar)。
   
3. 为什么暂时不开源？
目前程序还属于验证设计是否合理的测试阶段，规范可能随时会变，甚至会大变，所以暂时不开源。