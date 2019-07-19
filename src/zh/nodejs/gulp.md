# gulp
#### gulp 是一个前端自动化构建工具，基于流的构建系统，主要优点是速度，效率和简化

#### gulp 可以干什么？

    开发服务器，Sass,Less或Stylus文件的预处理器，处理JavaScript的自动化脚本，代码优化工具，压缩，编译或移动文件

##### gulp 的官网：https://www.gulpjs.com.cn/

gulp 类似的工具：grunt webpack

gulp 是基于 node.js 的，gulp 和所有插件都通过 JavaScript 编写并依托 Node.js 平台

#### 1.gulp 优点：

1. 易于使用
2. 构建快速
3. 插件高质
4. 易于学习

#### 2.gulp 的安装

全局安装 -> 使用 gulp 的命令

```
npm install gulp -g (4.0)
npm install gulp@next -g （3.9版本）
```

> 执行 gulp -v 查看 gulp 的版本号

局部安装 -> 配置文件内依赖 gulp

```
在本地下载
npm install gulp --save-dev(4.0)
```

#### 3.gulp api

**1.gulp.task(name,[deps],fn) //建任务**

name:任务名 string

```
任务名为default :  执行 ---> gulp

任务名为minJs : 执行 ---> gulp 任务名
```

**2.gulp.src(globs,[options]) //读文件**

globs 数据类型：string/array 查找文件的规则

- 通配符路径匹配

1. “src/a.js”
   > 指定具体文件；
2. “\*”：匹配所有文件
   > 例：src/\*.js(包含 src 下的所有 js 文件)；
3. “\*\*”：匹配 0 个或多个子文件夹
   > 例：src/\*_/_.js(包含 src 的 0 个或多个子文件夹下的 js 文件)；
4. “{}”：匹配多个属性
   > 例：src/{a,b}.js(包含 a.js 和 b.js 文件) src/\*.{jpg,png,gif}(src 下的所有 jpg/png/gif 文件)；
5. “!”：排除文件
   > 例：!src/a.js(不包含 src 下的 a.js 文件)；

**3.gulp.dest(输出的路径) //输出文件**

**4.gulp.serise(task1,task2,....) 设置任务的执行顺序 串行执行**

**5.gulp.parallel(task1,task2,.....) 设置任务的执行顺序 并行执行**

**6.gulp.watch(globs,gulp.serise/gulp.parallel(task1,task2..)) 监听文件变化，执行任务**

#### gulp 插件

| 插件               | 说明               |
| ------------------ | ------------------ |
| gulp-sass          | 编译 scss          |
| gulp-less          | 编译 less          |
| gulp-autoprefixer  | 自动添加前缀       |
| gulp-concat        | 合并文件           |
| gulp-clean-css     | 压缩 css           |
| gulp-webserver     | 起服务             |
| browser-sync       | 起服务             |
| gulp-htmlmin       | 压缩 html          |
| gulp-imagemin      | 压缩图片           |
| gulp-uglify        | 压缩 js 不支持 ES6 |
| gulp-babel         | ES6--->ES5         |
| gulp-rev           | 生成文件后缀       |
| gulp-rev-collector | 替换文件路径       |

#### 编译 scss 与 sass

```
 "gulp-sass": "^3.1.0"
```

```
var gScss = require('gulp-sass');
gulp.task('scss1', function() {
    return gulp.src('./origin/*.scss') //指定scss文件
        .pipe(gScss())//调用引入的文件 它抛出的是一个函数执行就行
        .pipe(gulp.dest('./detection'));
});
```

#### 编译 less

```
 "gulp-less": "^3.4.0"
```

```
var gLess = require('gulp-less');
gulp.task('less', function() {
    return gulp.src('./origin/*.less')
        .pipe(gLess())
        .pipe(gulp.dest('./detection/'));
});
```

##### 自动添加前缀

```
gulp-autoprefixer
```

```
var autoprefixer = require("autoprefixer");
gulp.task('autopre', function() {
    return gulp.src("src/css/*.css")
        .pipe(autoprefixer({
            browsers: ['last 2 versions'] //离你最近的两个浏览器版本
        ))
        .pipe(gulp.dest("dist")); //生成新文件
})
```

##### 合并文件

```
gulp-concat
```

```
var concats = require('gulp-concat');
gulp.task('concat', function() {
    return gulp.src('./detection/*.css') //需要合并的文件
        .pipe(concats('all.css')) //合并后的文件名
        .pipe(gulp.dest('./dest/')); //合并后存贮的位置
});
```

##### 压缩 css

```
 "gulp-clean-css"
```

```
var miniCss = require('gulp-clean-css');
gulp.task('minicss', function() {
    return gulp.src('./detection/style.css')
        .pipe(miniCss())
        .pipe(gulp.dest('./zlib/'));
});
```

> gulp-webserver

```
port ：配置端口号
open: 自动打开浏览器
livereload: 自动刷新
host: 配置IP
fallback: 指定默认打开的文件
middleware:function(req,res,next){ //拦截前端请求

}
```

#### 压缩 html

```
"gulp-htmlmin": "^4.0.0"
```

```
var miniHtml = require('gulp-htmlmin');
gulp.task('miniH', function() {
    return gulp.src('./detection/index.html')
        .pipe(miniHtml({
            collapseWhitespace: true, //压缩HTML

        }))
        .pipe(gulp.dest('./zlib/'))
});
```

> miniHtml 参数

```
{
    removeComments: true,//清除HTML注释
    collapseWhitespace: true,//压缩HTML
    collapseBooleanAttributes: true,//省略布尔属性的值 <input checked="true"/> ==> <input />
    removeEmptyAttributes: true,//删除所有空格作属性值 <input id="" /> ==> <input />
    removeScriptTypeAttributes: true,//删除<script>的type="text/javascript"
    removeStyleLinkTypeAttributes: true,//删除<style>和<link>的type="text/css"

}
```

##### 压缩图片

```
"gulp-imagemin": "^4.1.0"//压缩jpg  jpeg
```

```
var imagemin = require('gulp-imagemin');
gulp.task('testImagemin', function() {
    return gulp.src('src/img/*.{png,jpg,gif,ico}')
        .pipe(imagemin({
            optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
            progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
            interlaced: true, //类型：Boolean 默认：false 隔行扫描gif进行渲染
            multipass: true //类型：Boolean 默认：false 多次优化svg直到完全优化
        }))
        .pipe(gulp.dest('dist/img'));
});
```

#### 压缩 js

```
"gulp-uglify": "^3.0.0"
```

```
var uglify = require('gulp-uglify');
gulp.task('uglify', function() {
    return gulp.src('./detection/a.js')
        .pipe(uglify())
        .pipe(gulp.dest('./zlib/'));
});
```

> uglify 参数

```
{
    mangle: true,//类型：Boolean 默认：true 是否修改变量名
    mangle: {except: ['require' ,'exports' ,'module' ,'$']}//排除混淆关键字
    compress: true,//类型：Boolean 默认：true 是否完全压缩
    preserveComments: 'all' //保留所有注释
}
```

#### 编译 es6

```
 "gulp-babel": "^7.0.0"
 "babel-core": "^6.26.0"
 "babel-preset-es2015": "^6.24.1"
```

```
var babel = require('gulp-babel');//引入gulp-babel  但是：还得安装 babel-core 和 babel-preset-es2015
gulp.task('babel', function() {
    return gulp.src('./origin/a.js') //需要编译的文件
        .pipe(babel({
            presets: 'es2015' //指定编译后的版本为es5
        }))
        .pipe(gulp.dest('./detection/')); //编译后存放文件的路径
});
```

##### md5 添加前缀

```
 "gulp-rev": "^8.1.1" //对文件名加MD5后缀
 "gulp-rev-collector": "^1.2.4" //路径替换
```

```
var rev = require('gulp-rev');
var collector = require('gulp-rev-collector');
gulp.task('revs', function() {
    return gulp.src('./detection/style.css') //读取css
        .pipe(rev())
        .pipe(gulp.dest('./rev/')) //前缀添加完毕后存放文件的位置
        .pipe(rev.manifest()) // json
        .pipe(gulp.dest('./view/')); //存放json文件的地方
})
gulp.task('cols', function() {
    return gulp.src(['./view/rev-manifest.json', './detection/index.html']) //读取json文件  抓取HTML中对应的文件并且取代
        .pipe(collector({ //参数设置
            replaceReved: true // 是否前缀被改变后可再次被取代
        }))
        .pipe(gulp.dest('./view/')); //存放修改文件链接后的html文件
})
```

##### 代理

```
gulp.task('server',function(){
	return gulp.src('member-ui')
		.pipe(webserver({
			port:8989,
			proxies:[
				{
					source:"/api/add",target:"http://192.168.1.108:3000/api/add"
				},
				{
					source:"/api/del",target:"http://192.168.1.108:3000/api/del"
				},
				{
					source:"/api/detail",target:"http://192.168.1.108:3000/api/detail"
				}
			]
		}));
});
```
