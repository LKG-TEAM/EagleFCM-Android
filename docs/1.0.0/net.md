## Http配置

可以通过`fetchData`方法来实现。

```javascript
EagleBridge.requestConfig({
    contentType: "application/json"
});
```

### 参数

- contentType:         `String` | `选填`。


## Http请求

可以通过`fetchData`方法来实现。

```javascript
EagleBridge.fetchData({
    url: "http://api.com",
    param: {},
    method: "POST",
    success: function(resp){
    },
    error: function(msg){
    }
});
```

### 参数

- url:         `String` | `选填` 请求地址。
- param:       `Object` | `选填` 请求参数。
- method:      `String` | `选填` | `POST` 请求。
- success:     `Function`| `选填` 请求成功回调函数！
- error:       `Function`| `选填` 请求失败回调函数！

> `GET`请求

```javascript
EagleBridge.fetchData({
    url: "http://api.com",
    param: {},
    method: "GET",
    success: function(resp){
    },
    error: function(msg){
    }
});
```

> `POST`请求

```javascript
EagleBridge.fetchData({
    url: "http://api.com",
    param: {},
    success: function(resp){
    },
    error: function(msg){
    }
});
```


*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        //可以不写在deviceReady中。如果sdk没初始化，则执行无效。
        EagleBridge.fetchData({
            url: "http://api.com",
            param: {},
            success: function(resp){},
            error: function(msg){}
        });
    });
  </script>
  <script src="eagle.sdk.js"></script>
</head>
<body>
</body>
</html>
```
