# nodejs

#### 1.简述npm是什么

NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：

- 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
- 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
- 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

#### 2. 安装npm

- 新版的nodejs已经集成了npm，所以之前npm也一并安装好了。同样可以通过输入 "npm -v" 来测试是否成功安装
```
npm -v
```
- 如果你安装的是旧版本的 npm，可以很容易得通过 npm 命令来升级
```
npm install npm -g
```

#### 3.使用 npm 命令安装模块

1. npm install Module Name 
2. npm install Module Name --save
3. npm install Module Name -S

会在package.json中生成dependencies依赖(**生产环境**)

1. npm install Module Name 
2. npm install Module Name --save-dev
3. npm install Module Name -D

会在package.json中生成devDependencies依赖(**开发环境**)

1. npm install Module Name --global
2. npm install Module Name -g

**全局安装**，会安装到npm root –g所指向的路径里

**注意**:加-g参数的全局安装，只能保证将包安装到npm root –g所指向的路径中，并不能使包被全局访问到，要想包被全局访问到，则必须配置NODE_PATH环境变量

#### 配置NODE_PATH环境变量

- 通过npm config ls 查找到.npmrc文件的位置直接更改
- 通过命令进行修改
    - npm config set cache “路径”
    - npm config set prefix “路径”

提示：修改了npm全局路径后，NODE_PATH的变量值也要随之修改

**注意事项**
1. 发布的包中必须有package.json文件

2. package.json文件中必须有name和version两个字段

3. 发布的包不得与npm服务器上已存在的包重名

4. 发布的包24小时之内予以卸载

5. 卸载包后须过24小时之后再重新发布，且必须修改其版本号
