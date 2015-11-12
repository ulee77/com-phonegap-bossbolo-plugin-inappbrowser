# com-phonegap-bossbolo-plugin-inappbrowser
打开新链接插件，打开方式有：调用本地浏览器、新建标签页、当前标签页打开


### 插件的安装、卸载
```sh
phonegap plugin add https://github.com/ulee77/com-phonegap-bossbolo-plugin-inappbrowser.git
```
卸载命令
```sh
phonegap plugin rm com-phonegap-bossbolo-plugin-inappbrowser
```

### 平台支持
- phoengap 5+
- Android 4+
- IOS 5+

### 通用接口说明

## open——打开新链接
```sh
var ref = cordova.InAppBrowser.open(url, target, options, header);
var ref = window.open(url, target, options, header)
```
# 参数说明

- __ref__: 返回打开新页面窗口引用；

- __url__: 打开的链接地址，如果字符中包含`Unicode`字符，需要先进行`encodeURI()`；

- __target__: 指定 URL 链接的打开方式：
    - `_self`: 使用应用当前webView打开；
    - `_blank`: 通过 当前插件创建新的浏览器窗口打开；
    - `_system`: 使用系统默认浏览器打开；

- __options__: 参数设置
    - `location`: 是否显示标题栏，使用方法与默认值：`location=yes`；
    - `hidde`: 是否显示标题栏，使用方法与默认值：`hidde=no`；

- __header__: 仅当`target`设置为`_blank`时有效，设置标题栏中显示的文字，默认为显示链接地址。


## 其他接口

- addEventListener
- removeEventListener
- close
- show
- executeScript
- insertCSS

# addEventListener——页面加载事件监听
```sh
ref.addEventListener(eventname, callback);
```

- __eventname__: 事件名如下

  - `loadstart`: 开始载入页面.
  - `loadstop`: 停止加载页面.
  - `loaderror`: 页面载入错误.
  - `exit`: 页面窗口关闭.

- __callback__: 事件回调，回调参数如下

  - `type`: 事件名
  - `url`: 引发事件的URL
  - `code`: 错误码
  - `message`: 错误信息

# removeEventListener——移除监听
参数同 addEventListener
```sh
ref.removeEventListener(eventname, callback);
```

- __事件示例__
```sh
var ref = cordova.InAppBrowser.open('http://www.baidu.com', '_blank', 'location=yes');
var myCallback = function(event) { alert(event.url); }
ref.addEventListener('loadstart', myCallback);
ref.removeEventListener('loadstart', myCallback);
```

# close——关闭打开链接的窗口
```sh
ref.close();
```

# show
打开已隐藏InAppbrowser窗口，配合`hidden=yes`options使用
```sh
var ref = cordova.InAppBrowser.open('http://apache.org', '_blank', 'hidden=yes');
//TODO something
ref.show();
```

# executeScript——js脚本注入

```sh
ref.executeScript(details, callback);
```

- __details__: 注入的JS脚本内容，可以2种方式注入：
  - __file__: JS文件的路径.
  - __code__: JS脚本代码.

- __callback__: 注入脚本执行完成后的回调函数.
    - 如果注入脚本为`code`类型, 则得到其返回值并以`Array`类型返回单一参数. 如果执行的是多行脚本，则返回其最后一条语句返回值，或者最后一个表达式的值。

- __ 示例代码

    var ref = cordova.InAppBrowser.open('http://www.baidu.com', '_blank', 'location=yes');
    ref.addEventListener('loadstop', function() {
        ref.executeScript({file: "myscript.js"});
    });

# insertCSS——CSS注入

```sh
ref.insertCSS(details, callback);
```

- __details__: 注入的样式表内容，可以2种方式注入：
  - __file__: 注入样式表的文件路径.
  - __code__: 注入样式表的代码.

- __callback__: 当样式表嵌入完成时的回调.

- __ 示例代码

    var ref = cordova.InAppBrowser.open('http://www.baidu.com', '_blank', 'location=yes');
    ref.addEventListener('loadstop', function() {
        ref.insertCSS({file: "mystyles.css"});
    });

