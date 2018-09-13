# FAQ
- 为什么收不到推送通知？
> 检查是否没有翻墙，是否没有安装谷歌服务。
> 检查是否没有在Firebase控制台配置您的包名，是否下载了google-service.json到模块目录下。
> 检查是否在项目的build.gradle里引用了`classpath 'com.google.gms:google-services:4.0.2'`。
> 检查是否在模块的build.gradle里引用了`apply plugin: 'com.google.gms.google-services'`，且要放到最后一行。

- 为什么点击通知栏，总是跳转到首页？
> 点击通知默认是跳转到首页，您需要在重写跳转逻辑，类似如下，在`sendNotification`里写跳转逻辑。
	
	```java
	MessageBridge.getInstance().setMessagingInterface(new MessageBridge.MessagingInterface() {

        @Override
        public void sendNotification(RemoteMessage.Notification notification, Map<String, String> map) {
		｝
	}
	```

- 为什么app按了home键后，点击通知只能跳转到首页，在Application里写了`sendNotification`方法却没有走？
> 按了home键后，点击通知会跳转到首页，并将payload参数放入Bundle中，可以从bundle获取到数据，并作相应处理，比如，我们可以在模块入口类XXXWebModule里，写如下处理：
	
	```java
	if (bundle != null) {
        String type = bundle.getString("type");
        if ("1".equals(type)) { //谷歌推送，点击通知传值过来的。如果type=1，跳转到详情
            navigateTo(BCLWalletConstants.ROUTER.BCLWALLETMODULE_ORDERDETAILACTIVITY, bundle);
        }
    }
	```