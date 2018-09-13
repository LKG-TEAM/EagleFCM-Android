# 快速开始


## About EagleFCM

EagleFCM是依赖Google Firebase 云消息传递 (FCM) 开发的一个用于推送消息的模块。
FCM的官方地址为：

[https://firebase.google.com/docs/cloud-messaging/](https://firebase.google.com/docs/cloud-messaging/)


## ProGuard
不需要配置

## Add EagleFCM to your project
相关配置(这些配置由移动平台完成，不需手动更改)
在project根目录的build.gradle里
```groovy
    repositories {
        jcenter()
        maven { url 'https://maven.google.com' }
        maven { url "http://192.168.2.94:10080/repertory/maven/dependency/raw/master/" }
    }

    dependencies {
        classpath 'com.google.gms:google-services:4.0.2'
    }
```
在module的build.gradle里
```groovy
compile 'com.linkstec.common.eaglefcm:EagleFCM:1.0.0
```
其中1.0.0换成最新的版本，或者使用1.+的形式。