## 打开相机

可以通过`openCamera`方法来实现。

```javascript
EagleBridge.openCamera({
    cropX: 320,
    cropY: 320,
    ratioX: 1,
    ratioY: 1,
    success: function(resp){
    }
});
```

### 参数

- cropX:       `Number` | `选填` 指定宽度固定值。
- cropY:       `Number` | `选填` 指定高度固定值。
- ratioX:      `Number` | `选填` 指定宽度比例。
- ratioY:      `Number` | `选填` 指定高度比例。
- success:     `Function`| `选填` 回调函数resp 中接收图片base64转码字符串。

> 按照裁剪宽度高度

```javascript
EagleBridge.openCamera({
    cropX: 320,
    cropY: 320,
    success: function(resp){
    }
});
```

?> `cropX` 指定宽度固定值 //非必传。 `cropY` 指定高度固定值 //非必传。 如果传入需要cropX，cropY同时传入。


> 按照裁剪宽度高度比例

```javascript
EagleBridge.openCamera({
    ratioX: 1,
    ratioY: 1,
    success: function(resp){
    }
});
```

?> `ratioX` 指定宽度比例 //非必传。`ratioY` 指定高度比例 //非必传。 如果传入需要ratioX，ratioY同时传入。


*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        //可以不写在deviceReady中。如果sdk没初始化，则执行无效。
        EagleBridge.openCamera({
            ratioX: 1,
            ratioY: 1,
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




## 打开相册

可以通过`openAlbum`方法来实现。

```javascript
EagleBridge.openAlbum({
    cropX: 320,
    cropY: 320,
    ratioX: 1,
    ratioY: 1,
    success: function(resp){
    }
});
```

### 参数

- cropX:       `Number` | `选填` 指定宽度固定值。
- cropY:       `Number` | `选填` 指定高度固定值。
- ratioX:      `Number` | `选填` 指定宽度比例。
- ratioY:      `Number` | `选填` 指定高度比例。
- success:     `Function`| `选填` 回调函数resp 中接收图片base64转码字符串。

> 按照裁剪宽度高度

```javascript
EagleBridge.openAlbum({
    cropX: 320,
    cropY: 320,
    success: function(resp){
    }
});
```

?> `cropX` 指定宽度固定值 //非必传。 `cropY` 指定高度固定值 //非必传。 如果传入需要cropX，cropY同时传入。


> 按照裁剪宽度高度比例

```javascript
EagleBridge.openAlbum({
    ratioX: 1,
    ratioY: 1,
    success: function(resp){
    }
});
```

?> `ratioX` 指定宽度比例 //非必传。`ratioY` 指定高度比例 //非必传。 如果传入需要ratioX，ratioY同时传入。


*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        //可以不写在deviceReady中。如果sdk没初始化，则执行无效。
        EagleBridge.openAlbum({
            ratioX: 1,
            ratioY: 1,
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



## 扫描二维码

可以通过`openQRCode`方法来实现。Android需要引入`EagleQRCode` 模块。


```javascript
EagleBridge.openQRCode({
    success: function(resp){
    }
});
```



### 参数

- success:     `Function`| `选填` 回调函数resp 接收二维码识别后的值。

?> 传入`success`回调函数, 则扫描得到的数据，直接返回给js。 不传入则SDK内部处理，如果扫描得到的是url, 则直接打开页面。

*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <script>
    document.addEventListener("deviceReady", function (e) {
        EagleBridge.openQRCode();
    });
  </script>
  <script src="eagle.sdk.js"></script>
</head>
<body>
</body>
</html>
```

