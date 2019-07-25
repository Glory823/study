# JSBridge

### 原理

关于 JSBridge，绝大多数同学最早遇到的是微信的 WeiXinJSBridge（现在被封装成 JSSDK），各种 Web 页面可以通过 Bridge 调用微信提供的一些原生功能，为用户提供相关的功能。其实，JSBridge 很早就出现在软件开发中，在一些桌面软件中很早就运用了这样的形式，多用在通知、产品详情、广告等模块中，然后这些模块中，使用的是 Web UI，而相关按钮点击后，调用的是 Native 功能。现在移动端盛行，不管是 Hybrid 应用，还是 React-Native 都离不开 JSBridge，当然也包括在国内举足轻重的微信小程序。

![image](https://user-gold-cdn.xitu.io/2018/3/29/16270f34f02109eb?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

![image](https://user-gold-cdn.xitu.io/2018/3/29/16270f45ca45db54?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

移动端混合开发中的 JSBridge，主要被应用在两种形式的技术方案上

- 基于 Web 的 Hybrid 解决方案：例如微信浏览器、各公司的 Hybrid 方案
- 非基于 Web UI 但业务逻辑基于 JavaScript 的解决方案：例如 React-Native

【注】:微信小程序基于 Web UI，但是为了追求运行效率，对 UI 展现逻辑和业务逻辑的 JavaScript 进行了隔离。因此小程序的技术方案介于上面描述的两种方式之间。

### JSBridge 的用途

JSBridge 简单来讲，主要是 给 JavaScript 提供调用 Native 功能的接口，让混合开发中的『前端部分』可以方便地使用地址位置、摄像头甚至支付等 Native 功能。

JSBridge 就像其名称中的『Bridge』的意义一样，是 Native 和非 Native 之间的桥梁，它的核心是 构建 Native 和非 Native 间消息通信的通道，而且是 双向通信的通道。

![image](https://user-gold-cdn.xitu.io/2018/3/29/16270f744a3e61f2?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- JS 向 Native 发送消息 : 调用相关功能、通知 Native 当前 JS 的相关状态等。
- Native 向 JS 发送消息 : 回溯调用结果、消息推送、通知 JS 当前 Native 的状态等。

1.  JavaScript 调用 Native

- 注入 API
  原理:通过 WebView 提供的接口，向 JavaScript 的 Context（window）中注入对象或者方法，让 JavaScript 调用时，直接执行相应的 Native 代码逻辑，达到 JavaScript 调用 Native 的目的。
- 拦截 URL SCHEME
  原理:Web 端通过某种方式（例如 iframe.src）发送 URL Scheme 请求，之后 Native 拦截到请求并根据 URL SCHEME（包括所带的参数）进行相关操作

2. Native 调用 JavaScript
   Native 调用 JavaScript，其实就是执行拼接 JavaScript 字符串，从外部调用 JavaScript 中的方法，因此 JavaScript 的方法必须在全局的 window 上。

### 通信原理小总结

- JavaScript 调用 Native 推荐使用 注入 API 的方式
- Native 调用 JavaScript 则直接执行拼接好的 JavaScript 代码即可

### 代码实现

```
export default {
  callbackIndex: 0,
  callbackPrefix: '__MCL_CALLBACK_',
  schema: 'chelunJSBridge',
  invoke: function (namespace, api, param) {
    namespace = String(namespace);
    api = String(api);
    var url = this.schema + '://' + namespace + '/' + api;
    if (param && typeof param === 'object') {
      url += this._buildQuery(param);
    }

    this._sendRequest(url);
  },
  _buildQuery: function (param) {
    var seg = [], frag = '', uriSeg = '';
    for (var attr in param) {
      if (param.hasOwnProperty(attr)) {
        if (param[attr] && typeof param[attr] === 'function') {
          var callbackNo = this._createCallbackNo(param[attr]);
          if (attr === 'callback') {
            frag = '#' + callbackNo;
          } else {
            seg.push(encodeURIComponent(attr) + '=' + callbackNo);
          }
        } else {
          var paramValue = String(param[attr]);
          seg.push(encodeURIComponent(attr) + '=' + encodeURIComponent(paramValue));
        }
      }
    }

    seg.length && (uriSeg += '?' + seg.join('&'));
    return uriSeg += frag;

  },
  //生成回调号
  _createCallbackNo: function (fn) {
    var callbackNo = this.callbackIndex;
    window[this.callbackPrefix + callbackNo] = fn;
    this.callbackIndex += 1;
    return callbackNo;
  },
  //发送客户端调用请求
  _sendRequest: function (uri) {
    var i = document.createElement('iframe');
    i.style.display = 'none';
    i.onload = function () {
      i.parentNode.removeChild(i);
    };
    i.src = uri;
    document.body.appendChild(i);
  }
};

```
