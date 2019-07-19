# 初探 JavaScript 部分

## 初步认识

- 编写第一个 JavaScript 程序：

```
    <script>
        alert("hello world!");
    </script>
```

- 发展史：

  1. 1992 年前后，Nombas 公司发明了一种嵌入式脚本语言(C--)。

  2. 1995 年，JavaScript 诞生。由 Netscape(网景)的 Brendan Eich 开发。

  3. JavaScript 也叫 JScript。JScript 是由微软(IE)开发的。

  4. 1997 年，由 ECMA(欧洲计算机制造商协会)定义了名为 ECMAScript 的全新脚本语言(规范)。

  **Europen Computer Making Association**

* JavaScript 是一种专门为与网页交互而设计的脚本语言。

- JavaScript 是一种非常松散的面向对象语言 ==> 弱类型语言
  为什么说是面向对象的语言 js 中有一个说法叫一切皆对象
  因为 js 是弱类型语言.不像 c++,C#这类型语言!他不支持函数方法重载.你之前写一个方法.后面再写一个相同名字的方法他默认会把上一个方法覆盖掉!这种情况和 PHP 中相同!
  他不像是 C#等语言支持函数重载.根据不同的参数.返回值调用不同的方法!

1. HTML -- 结构
2. CSS -- 样式
3. JS -- 行为（让你的页面动起来，对页面进行操作验证）

- JavaScript 的解释器被称为 JavaScript 引擎，为浏览器的一部分，广泛用于客户端的脚本语言。-- 也可以用于服务端

* JavaScript 由三部分组成：（**重点 1**）

  1.  ECMAScript 由 ECMA-262 定义，提供核心语言功能 规范 语法要求

          ECMAScript规定了以下组成部分：语法、类型、语句、关键字、保留字、操作符以及对象

  2.  DOM （document object model）文档对象模型 提供访问和操作网页内容的方法和接口

          DOM级别：DOM1 、DOM2、DOM3

  3.  BOM （borwser object model）浏览器对象模型 提供与浏览器交互的方法和接口

- JavaScript 能做什么：

  1. JavaScript 可以将动态的文本放入 html 页面

  2. JavaScript 可以读写 html 元素

  3. JavaScript 可被用来验证数据

  4. JavaScript 可以对事件做出响应

把 JavaScript 插入到 HTML 页面中要使用 script 元素。JavaScript 可以嵌入到 HTML 页面中，也可以

引用外部的 JavaScript 文件(设置 src 属性)。

     可以在head或body中使用 script 嵌入javaScript脚本

```
    <script type="text/javascript" src="jq.js"></script>

    <script>
        alert("Hello world!");// 页面弹出提示信息
    </script>
```

- alert() 系统弹出框 一般用于调试

- confirm（） 确定提示框

      点击确定返回 true 点击取消返回 false

- console.log() 控制台打印/输出 用于调试程序 报错信息的收集

- prompt（ 提示信息 1，提示信息 2，... ） 输入弹出框


     点击确定返回你输入的字符串， 点击取消返回 null（表示空）

- document.write() 打印到页面（文本或标签）

## 语法结构部分

- 区分大小写：ECMAScript 中的一切(变量、函数名和操作符)都严格区分大小写。

- 注释：ECMAScript 有单行注释和多行注释(块级)两种

  样式：//单行注释 方法：ctrl + /

  样式：/_多行注释 _/ 方法：ctrl + shift + /

* JavaScript 注释可用于提高代码的可读性，以及阻止代码的执行(解析代码时过滤)。

* 可选的分号：ECMAScript 中的语句以一个分号结尾;如果省略分号，则由解释器

  确定语句的结尾。这是非严谨语言的特点。(不推荐省略分号)

* 代码规范性：代码规范性好的代码清晰易读，每家公司都有自己的规范性。

* 标识符：指变量、函数、属性的名字，或者函数的参数。

  标识符命名规则：

```
    1)开始字符必须是一个字母、下划线(_)或一个美元符号($);

    2)其他的字符可以是字母、下划线、美元符号或数字;

    3)不能把关键字、保留字用作标识符。

    4）尽量语义化

    5）驼峰命名
        分为大驼峰和小驼峰
        大驼峰（两个首字母都大写）
        小驼峰（第一个首字母不大写）

    6）严格区分大小写
```

```
    var(variable  可变的)

    var name_01; // 合法
    var _name01; // 合法
    var $name01; // 合法
    var 01name;  // 不合法
```

ECMAScript 标识符一般采用驼峰大小写命名格式。
var firstname;// 合法 不是驼峰
var firstName;// 合法 是驼峰
getElementById();//getelementbyid(); 驼峰命名形式
addZero();// 加零

建议标识符具有语义化。

- 变量：ECMAScript 的变量是松散类型的，所谓松散类型就是可以保存任何类型的数据。

        定义变量的关键字:var 变量赋值: = （变量赋值的过程叫初始化）

        格式:

        声明变量：var a

        声明的同时赋值：var 变量名 = 值;

        先声明后赋值：var 变量名;   变量名 = 值   eg:var a;   a=1;

  1. 变量的类型取决于值; var num = 10;

  2. 多个变量之间用逗号隔开;例如:var a = 1,b = 2,c = 3;

  3. 同一变量后赋值会覆盖先赋值;var num = 10 ; num = 30; console.log( num );// 30

  4. var 定义的变量叫显式声明， 省略 var 声明的变量叫隐式声明;

  5. 省略 var 操作符可以定义全局变量(不推荐);

  6. var 定义的变量有变量声明提升的过程（了解：之后课程详细介绍）。
