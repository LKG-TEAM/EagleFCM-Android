## 设置导航样式

可以直接通过 EagleSdk 原生的导航栏样式。


```javascript
EagleBridge.setNavBarStyle({
    title: "导航栏标题"          // 导航栏标题
    backgroundColor:"#fff000"   // 导航栏颜色
    isHidden: false             // 是否隐藏  默认false
});
```

### 参数

- title:            `String` | `选填` 导航栏标题
- backgroundColor:  `String` | `选填` 导航栏颜色
- isHidden:         `Boolean` | `选填` | `默认: false` 是否隐藏


> 如果只需要设置标题, 只需要设置`title`属性即可

```javascript
EagleBridge.setNavBarStyle({
    title: "导航栏标题"
});
```

> 如果只需要设置颜色, 只需要设置`backgroundColor`属性即可

```javascript
EagleBridge.setNavBarStyle({
    backgroundColor: "#fff000"
});
```

*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        EagleBridge.setNavBarStyle({
            title: "导航栏标题"          // 导航栏标题
            backgroundColor:"#fff000"   // 导航栏颜色
            isHidden: false             // 是否隐藏  默认false
        });
    });
  </script>
  <script src="eagle.sdk.js"></script>
</head>
<body>
</body>
</html>
```


## 隐藏导航栏

如果想隐藏导航栏, 只需要设置`isHidden`属性即可

```javascript
EagleBridge.setNavBarStyle({
    isHidden: true
});
```

### 参数

- isHidden:`Boolean` | `选填` | `默认: false` 是否隐藏

*index.html*
```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        EagleBridge.setNavBarStyle({
            isHidden: true             // 是否隐藏  默认false
        });
    });
  </script>
  <script src="eagle.sdk.js"></script>
</head>
<body>
</body>
</html>
```


## 设置导航栏右边按钮

可以通过`setOptionMenu`方法来实现。

```javascript
EagleBridge.setOptionMenu({
     expandable: true,          // 是否可以收起
     menus:[{
        title:"标题",             // 文字 （只显示两个字宽度）
        icon:"\ue6aa",          // iconfont Unicode编码,
        size:"16",              //字体大小      `可不传`
        color:"#ff0000",        //图标或字体颜色 `可不传`
        url:"https://www.baidu.com", //跳转url  可直接点击跳转的地址，不传即回调函数接收参数。  `可不传`
     }]
     success: function(resp){}//点击回调函数
});
```

### 参数

- expandable:  `Boolean` | `选填` | `默认: false` 是否可以收起
- menus:       `Array`   | `选填` 数组类型, 可传入多个按钮。
- success:     `Function`| `选填` 回调函数,接收点击传入指定。resp接收的是索引。


>`expandable`属性, 默认false。 传入true后，即右上角变成 `+`，点击弹出窗口，类似微信。

```javascript
EagleBridge.setOptionMenu({
    expandable: true,
});
```

>`menus` 可传入多个按钮。如果传入空数组，则右上角没有按钮。

```javascript
EagleBridge.setOptionMenu({
    menus: []
});
```

>`success`接收点击传入指定。resp接收的是索引。

```javascript
EagleBridge.setOptionMenu({
    success: function(resp){ }
});
```


## 移除导航栏按钮

可以通过`removeOptionMenu`方法来实现。

```javascript
EagleBridge.removeOptionMenu();
```


## 获取应用信息

可以通过`getApplicationInfo`方法来实现。

```javascript
EagleBridge.getApplicationInfo({
    success: function(resp){
    }
});
```

### 参数

- success:     `Function`| `选填` 回调函数。接收应用信息。


## 获取系统信息

可以通过`getSystemInfo`方法来实现。

```javascript
EagleBridge.getSystemInfo({
    success: function(resp){
    }
});
```

### 参数

- success:     `Function`| `选填` 回调函数。接收系统信息。



## 获取设置信息

可以通过`getSettings`方法来实现。 settings由移动平台

```javascript
EagleBridge.getSettings({
    path: "modules.name"
    success: function(resp){
    }
});
```


### 参数

- path:        `String`| `选填` 获取制定路径设置信息。中间用`.`连接。
- success:     `Function`| `选填` 回调函数。接收返回设置信息。

>只传入`success`, 则获取全部设置信息。

```javascript
EagleBridge.getSettings({
    success: function(resp){ }
});
```


## 设置下拉刷新

可以通过`setEnableRefresh`方法来实现，`enable` 默认false, 设置为true可执行下拉刷新。

```javascript
EagleBridge.setEnableRefresh({
    enable: false //默认false 设置为true, 则可以下拉刷新。
});
```

### 参数

- enable:      `Boolean`| `选填` | `默认: false` 设置是否可以下拉刷。


## 打开新的页面

可以通过`openWindow`方法来实现。

```javascript
EagleBridge.openWindow({
    url: "eagle://address",
    success: function(resp){
    }
});
```


### 参数

- url:         `String`| `必填`  可以为`http:`页面， 也可以是`eagle:`路由的原生页面。
- success:     `Function`| `选填` 回调函数。希望路由页面返回值，则需要填写回调函数。

> 打开指定页面

```javascript
EagleBridge.openWindow({
    url: "http://address",
});
```

> 打开指定页面并接收返回值

```javascript
EagleBridge.openWindow({
    url: "eagle://address",
    success: function(resp){
    }
});
```



## 关闭当前页面

可以通过`closeWindow`方法来实现。

```javascript
EagleBridge.closeWindow({
   data: "string"  //选填
});
```


### 参数

- data:        `String`| `选填`  传递给前一个页面的值。

> 直接关闭当前页面

```javascript
EagleBridge.closeWindow();
```

> 关闭当前页面并返回值给前一个页面

```javascript
EagleBridge.closeWindow({
   data: "string"
});
```

