# SmartCore
[![npm version](https://img.shields.io/badge/releases-0.0.1-blue.svg)](https://github.com/SmartCore-Team/SmartCore/tree/master)
[![npm version](https://img.shields.io/badge/dev-0.0.1-yellow.svg)](https://github.com/SmartCore-Team/SmartCore/tree/dev)
   
一个智能家居设备管理平台。   
只负责管理设备并提供口子，不提供任何功能。

## 前言&设计初衷
玩智能家居有一段时间了，用了很多平台，也折腾了很多，但是始终不是我想要的。   
其实只是想要一个：
1. 能把所有设备都接入其中，并且本身很轻量级的平台;
2. 通过上层app做加法提供功能，而不是平台本身很重有一堆功能让用户去做减法;
3. 配置自由灵活可以融入任何设备、任何类型、任何属性、任何规则。

## 架构图
![](https://raw.githubusercontent.com/SmartCore-Team/SmartCore/master/images/framework.png)

## 名词解释
1. SmartCore: 指本平台。
2. Plugin: 插件，平台通过插件实现控制设备，是平台和设备之间沟通的桥梁。
3. Action: 接口，平台提供的服务，上层应用可以通过接口和平台交互。
4. Notify: 通知，平台主动推送消息。
5. App: 应用，使用平台资源的上层应用。

## 接口文档
### v1 (已json为例)
#### 获取平台信息
```
{
    "type": "info"
}
```
#### 获取配置信息
```
{
    "type": "config"
}
```
#### 获取当前平台加载插件
```
{
    "type": "plugin",
    "method": "list"
}
```
#### 加载插件
```
{
    "type": "plugin",
    "method": "load",
    "pluginList": ["smartcore-plugin-mqtt-0.0.1.jar", "smartcore-plugin-demo-0.0.1.jar"]
}
```
#### 卸载插件
```
{
    "type": "plugin",
    "method": "unload",
    "pluginList": ["smartcore-plugin-mqtt-0.0.1.jar", "smartcore-plugin-demo-0.0.1.jar"]
}
```
#### 载入设备服务
```
{
    "type": "device",
    "method": "init",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 关闭设备服务
```
{
    "type": "device",
    "method": "close",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 获取所有设备ID
```
{
    "type": "device",
    "method": "list"
}
```
#### 获取设备所有信息
```
{
    "type": "device",
    "method": "getDevice",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 获取设备FriendlyName
```
{
    "type": "device",
    "method": "getDeviceFriendlyName",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 获取设备类型
```
{
    "type": "device",
    "method": "getDeviceType",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 获取设备硬件信息
```
{
    "type": "device",
    "method": "getDeviceInfo",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 获取设备所有属性的全部信息
```
{
    "type": "device",
    "method": "getDeviceProperties",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 获取设备所有属性的值
```
{
    "type": "device",
    "method": "getPropertyValueMap",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```
#### 获取设备某些属性的全部信息
```
{
    "type": "device",
    "method": "getProperty",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"],
    "propertyIdList": ["power", "mode"]
}
```
#### 获取设备某些属性的值
```
{
    "type": "device",
    "method": "getPropertyValue",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"],
    "propertyIdList": ["power", "mode"]
}
```
#### 获取设备某些属性的FriendlyName
```
{
    "type": "device",
    "method": "getPropertyFriendlyName",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"],
    "propertyIdList": ["power", "mode"]
}
```
#### 设置设备某些属性的值
```
{
    "type": "device",
    "method": "setPropertyValue",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"],
    "propertyIdList": ["power"],
    "value": true
}
```
#### 设置设备某些属性的值2
```
{
    "type": "device",
    "method": "setPropertyValue",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"],
    "value": {
        "power": true,
        "mode": 3
    }
}
```
#### 操作设备
```
{
    "type": "device",
    "method": "operation",
    "operation": "open",
    "deviceIdList": ["AABBCCDDEEFF", "123456789"]
}
```

## Q&A
1. 为什么使用Java开发？   
因为群里的Java程序员最多。

2. 如何解决平台与插件/插件与插件之间的jar hell问题？   
程序加载plugin未使用默认的class loader，查找class规则为优先查找jar包本身，后找其他。所以plugin开发者若使用向下兼容有问题的依赖jar时，请打包成uber jar(fat jar)。
   
3. 为什么暂时不开源？   
目前程序还属于验证设计是否合理的测试阶段，规范可能随时会变，甚至会大变，所以暂时不开源。