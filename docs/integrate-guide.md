# 运行Google Play、Google Service
- 如果您手机上已经有谷歌相关服务，不需再安装，但是国内大部分手机都没有谷歌相关服务，需要您安装这些服务，最快捷的安装方式是在应用宝上搜索go谷歌安装器，它会帮助您安装4个谷歌套件：Google服务框架、Google账户管理程序、Google Play服务、Google Play商店。
- 手机和电脑都需要翻墙。您可以在手机和电脑上安装蓝灯，在github上搜索lantern下载安装即可。如果蓝灯效果不好，还可以使用shadowsocks，自己百度设置方法。或者网上搜索依米、天行加速器等，一般只有一天免费试用，以后就要收费了。
# 在您的module或应用里进行配置
- 项目的build.gradle里添加`classpath 'com.google.gms:google-services:4.0.2'`
	
	```groovy
	buildscript {
    dependencies {
        classpath 'com.google.gms:google-services:4.0.2'
        classpath 'com.android.tools.build:gradle:3.1.4'
    	}
	}
	```
- 在模块里的build.gradle里最后一行添加`apply plugin: 'com.google.gms.google-services'`

	```groovy
	apply plugin: 'com.google.gms.google-services'
	```

- 在模块的根目录下，与模块的build.gradle同级别下，添加`google-services.json`文件。json文件从哪里来？见下面说明。

# 使用Firebase控制台
- 点击跳转到Firebase控制台：[Firebase控制台](https://console.firebase.google.com/u/0/)
- 点击右上角，登录Google帐号。
- 创建项目，或者进入已有的项目。
- 下载`google-services.json`文件放到您的项目里的模块的目录下，比如项目为EagleFCM，则放到模块EagleFCMModule文件夹下。
- 点击左侧Cloud messaging。
- 点击新建消息，新建好后点击发送就可以推送到手机上（手机别忘了翻墙和谷歌服务）。
- 如果需要传参数，在新建消息里，自定义数据，根据键值对配置参数。这些字段最终会在"data"下。

# 消息的格式
消息格式如下
```json
{
 "to":"elzLX-ph1Ss:APA91bHVMT-gCQ8v0UbA062_Mvmgbrkq_SE7ftjZfcSYtS-cLmldh8UOfyVOr0hWvGvabRo6r3XLNmBcON0tlzuxwD6MDabYjENcjYNJjGKUnqRWV4f2FaYElRwCkZy0tW8fCfbfoHEu",
 "data":{
 "type":1,
 "address":"0x11111",
 "orderNo":"10000"
 },
 "notification":{
 "title":"This is a FCM Device Group Message",
 "body":"Message",
 "icon":"myicon",
 "color":"#ffffff"
 }
}
```

 其中to代表接受者token
 data为数据内容
 norification为通知定义

# 自定义接收消息的处理
`MessageBridge`类是EagleFCM sdk中消息接收与集成EagleFCM的模块之间沟通的桥梁，使用`setMessagingInterface()`方法，
并实现您想要实现的方法，做自己的业务逻辑。
例如，我们可以在`TestModuleApplication`和`ModuleManager`里进行FCM的初始化。具体的方法，可以参考[FCM官方文档](https://firebase.google.com/docs/android/setup?authuser=0)

	```java
	private void initFCM() {
     //初始化推送
     MessageBridge.getInstance().setMessagingInterface(new MessageBridge.MessagingInterface() {

         @Override
         public void scheduleJob(Map<String, String> map) {
         }

         @Override
         public void handleNow(Map<String, String> map) {

         }

         @Override
         public void sendRegistrationToServer(String token) {
             //通知h5，该刷新token了
             Log.e("sendRegistration", "sendRegistrationToServer:" + token);
             PushParam pushParam = new PushParam();
             pushParam.setOs("android");
             pushParam.setToken(token);
             pushParam.setPushType("googlefcm");
             EventBus.getDefault().post(pushParam);

         }

         @Override
         public void sendNotification(RemoteMessage.Notification notification, Map<String, String> map) {
             String messageBody = notification.getBody();
             String type = map.get("type");
             Intent intent = null;
             if (map.size() > 0) {
                 if (map instanceof ArrayMap) {
                     Bundle bundle = new Bundle();
                     Set<String> keys = map.keySet();
                     for (String key : keys) {
                         bundle.putString(key, map.get(key));
                     }
                     if ("1".equals(type)) {
                         intent = new Intent(BaseApplication.getDefault(), OrderDetailActivity.class);
                         String address = map.get("address");
                         String orderNo = map.get("orderNo");
                         bundle.putString("address", address);
                         bundle.putString("orderNo", orderNo);
                     }
                     intent.putExtras(bundle);
                 }
             }
    	 intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_CLEAR_TOP);
    	 PendingIntent pendingIntent = PendingIntent.getActivity(BaseApplication.getDefault(), 0 /* Request code */, 	intent,
                PendingIntent.FLAG_ONE_SHOT);
         Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
         NotificationCompat.Builder notificationBuilder =
                 new NotificationCompat.Builder(BaseApplication.getDefault())
                         .setSmallIcon(R.mipmap.ic_launcher)
                         .setContentTitle(map.get("title"))
                         .setContentText(messageBody)
                         .setAutoCancel(true)
                         .setSound(defaultSoundUri)
                         .setContentIntent(pendingIntent);
         Ringtone r = RingtoneManager.getRingtone(BaseApplication.getDefault(), defaultSoundUri);
         r.play();
         NotificationManager notificationManager =
                 (NotificationManager) BaseApplication.getDefault().getSystemService(Context.NOTIFICATION_SERVICE);
         notificationManager.notify(0 /* ID of notification */, notificationBuilder.build());
         SharedPreferenceUtil.setUnreadMessageData(BaseApplication.getDefault(), SharedPreferenceUtil.AutoIncreateData);
            }
        });
    }
	```
# 入口页面加入对payload的处理
app在后台时，点击推送通知只能跳转到首页，payload会放在Bundle里，我们可以拿到Bundle并作处理跳转到想要的页面，例如：
	
	```java
	if (bundle != null) {
        String type = bundle.getString("type");
        if ("1".equals(type)) { //谷歌推送，点击通知传值过来的。如果type=1，跳转到详情
            navigateTo(BCLWalletConstants.ROUTER.BCLWALLETMODULE_ORDERDETAILACTIVITY, bundle);
        }
    }
	```