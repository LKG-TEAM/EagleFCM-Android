## 注册JS方法

注册`javascript`方法，提供给原生应用调用。

```javascript
EagleBridge.registerFunction({
    name: "__name",
    success: function(resp){
    }
});
```

### 参数

- name:        `String` | `必填` 指定宽度固定值。
- success:     `Function`| `必填` 原生调用JS方法。

!> `name`方法名定义规则：以`__` `双下划线`开头，驼峰命名。如：__handlerJsMethod

?> `resp`为原生传入的数据。


*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        //可以不写在deviceReady中。如果sdk没初始化，则执行无效。
        EagleBridge.registerFunction({
            name: "__handlerJsMethod",
            success: function(resp){
            }
        });
    });
  </script>
  <script src="eagle.sdk.js"></script>
</head>
<body>
</body>
</html>
```


## 调用Native方法

除`EagleJsSDK`提供的方法外，也可以调用原生提供的指定方法。

```javascript
EagleBridge.invoke({
    name: "_name",
    param: Object
    success: function(resp){
    }
});
```

### 参数

- name:        `String` | `必填` 原生提供的方法。
- param:       `Object` | `选填` 传入给原生方法的参数。
- success:     `Function` | `选填` 接收原生回调函数。

!> `name`方法名定义规则：以`_` `单下划线`开头，驼峰命名。如：_handlerNativeMethod

> 直接调用原生方法。

```javascript
EagleBridge.invoke({
    name: "_toDo",
});
```

> 调用带参数原生方法。

```javascript
EagleBridge.invoke({
    name: "_showToast",
    param: {message: "消息"},
});
```

> 调用原生方法返回值。

```javascript
EagleBridge.invoke({
    name: "_showToast",
    param: {message: "消息"},
    success: function(resp){
    }
});
```

?> `success` 非必填。如果需要接收原生返回的数据，则需要填写`success`函数。


*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        //可以不写在deviceReady中。如果sdk没初始化，则执行无效。
        EagleBridge.invoke({
            name: "_handlerNativeMethod",
            param: {data:1},
            success: function(resp){
            }
        });
    });
  </script>
  <script src="eagle.sdk.js"></script>
</head>
<body>
</body>
</html>
```
