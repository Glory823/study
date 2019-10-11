# 创建 uni-app


### 下载开发工具

uni-app 在 Hbuilder 开发，在微信开发者工具预览

- [ Hbuilder ](https://www.dcloud.io/hbuilderx.html)
- [ 微信开发者工具 ](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)

### 新建项目

> 文件 → 新建 → 项目

![image](https://wiki.alphalawyer.cn/download/attachments/83197961/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-10-10%20%E4%B8%8A%E5%8D%8810.10.39.png?version=1&modificationDate=1570673473000&api=v2)

### 开发设置

> manifest.json 配置

![image](https://wiki.alphalawyer.cn/download/attachments/83197961/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-10-10%20%E4%B8%8A%E5%8D%8810.17.59.png?version=1&modificationDate=1570674000000&api=v2)

### 运行设置

> 运行 → 运行到小程序模拟器 → 运行设置

![image](https://wiki.alphalawyer.cn/download/attachments/83197961/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-10-10%20%E4%B8%8A%E5%8D%8810.22.10.png?version=1&modificationDate=1570674235000&api=v2)

### 微信开发者工具设置

> 设置 → 安全设置，开启服务端口

![image](https://wiki.alphalawyer.cn/download/attachments/83197961/%E6%9C%AA%E5%91%BD%E5%90%8D.png?version=1&modificationDate=1570674780000&api=v2)

### 运行

> 设置完成后，就可以运行了，在 HBuilder X 愉快的编辑代码，保存后会热更新到微信开发者工具

![image](https://wiki.alphalawyer.cn/download/attachments/83197961/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-10-10%20%E4%B8%8A%E5%8D%8810.39.29.png?version=1&modificationDate=1570675181000&api=v2)

### 语法校验

> 工具 → 插件安装，安装插件：stylelint、eslint-plugin-vue、eslint-js

![image](https://wiki.alphalawyer.cn/download/attachments/83197961/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-10-10%20%E4%B8%8B%E5%8D%885.06.27.png?version=1&modificationDate=1570698434000&api=v2)

> 工具 → 插件配置 → eslint-vue → .eslintrc.js

```
//更详细的配置文档请参考：https://github.com/vuejs/eslint-plugin-vue#gear-configs
module.exports = {
    "extends": "plugin:vue/strongly-recommended",
    parserOptions: {
        ecmaVersion: 2017,
        sourceType: 'module'
    },
    "rules":{}
};
```

> 工具 → 插件配置 → eslint-js → .eslintrc.js

```
//详细配置教程请参考：http://eslint.cn/docs/user-guide/configuring
module.exports = {
    "plugins": [
        "html"
    ],
    "extends": "eslint:recommended",
    "parserOptions": {
        "ecmaVersion": 2018,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true
        },
        "allowImportExportEverywhere": false
    }
};
```

> 最后，重启 Hbuilder