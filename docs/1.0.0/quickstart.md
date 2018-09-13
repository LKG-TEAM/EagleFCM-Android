# 快速开始

我们只需在 `index.html` 文件中引入`eagle.sdk.js`文件即可。


## 初始化

在`html` `head`内编写监听sdk初始化完成事件。

```javascript
document.addEventListener("deviceReady", function (e) {});
```

## 引入文件

在`html` `head`引入`eagle.sdk.js`, 即初始化完成。

```javascript
<script src="eagle.sdk.js"></script>
```


*index.html*

```html
<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta charset="UTF-8">
  <script>
    document.addEventListener("deviceReady", function (e) {});
  </script>
  <script src="eagle.sdk.js"></script>
</head>
<body>
</body>
</html>
```

