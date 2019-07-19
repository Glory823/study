# 数据类型

1、ECMAScript 数据类型：5 种基本数据类型(简单数据类型或原始类型) 和 1 种复杂数据类型

5 种基本数据类型：

```
    undefined 未定义 10:22 2018/8/30 类型
    null 空类型
    boolean 布尔类型
    number 数值型
    string 字符串类型
```

1 种复杂数据类型：

```
    object —— 对象类型
```

- 栈内存和堆内存

  **栈内存**:5 种基本数据类型的值保存在栈内存中

  **堆内存**:对象类型的值保存在堆内存中

- Undefined -- 未定义类型 （就保存一个值）

  Undefined 类型只有一个值，即特殊的 undefined。

```
  1)使用 var 声明变量但未赋值(未初始化)时，这个变量的值就是 undefined。检测其类型也是 undefined。
    var a;
    console.log(a);//a=undefined
    console.log(typeof a);//"undefined"

  注意：一般不需要显示的将变量设置为 undefined。
    var a = undefined;
    var a;//undefined

  2)变量从未定义过 ，他的类型为 undefined ，值报错。
    console.log(e); //报错 e is not defined
    console.log(typeof e);//"undefined"（相当于隐式声明了个 e 但没有报错）
```

- Null -- 空类型 （就保存一个值）

Null 类型是第二个只有一个值的类型，这个特殊值是 null。null 值表示一个空对象指针。
Null 是特殊的对象类型：object

```
    var  car = null;
    console.log(car);//null
    console.log(typeof car);//"object"
```

注意:实际上 undefined 值是派生自 null 值的，因此 ECMA-262 规定对它们的相等性测试要返回 true。

alert(undefined == null); //true 真

- Boolean -- 布尔类型

Boolean 类型是 ECMAScript 中使用得最多的一种类型,用于表示真假的数据类型。

转 boolean 值为 false 的 6 个

```
null false NAN undelined "" 0 除了这 6 个其他转 boolean 为真
```

Boolean 类型只有两个值：true(真) \ false(假)。

```
    var flag = true;//false
    console.log(flag);//true
    console.log( typeof(flag) );//"boolean"
```

- Number -- 数值类型 分为整数和浮点数

  - 整数 100、22、11、3

  - 浮点数值(有些语言中被称为双精度数值) 4.522 3.1415926

          浮点数值的最高精度是17位小数。特殊：0.1+0.2=0.30000000000000004

  数值类型中一种特殊的数值: NaN: not a Number 不是一个数字==非数值 特殊的数值类型（检测 NaN 的数据类型返回 number）

        ==表示判断     =表示赋值        ===表示全等

        表示一个本来要返回数值的操作数未返回数值的情况。

        console.log( 5 - "hello" );//NaN

  NaN 特点： 1)任何涉及 NaN 的操作都会返回 NaN。 NaN + 4 // NaN 2)

  **NaN 与任何值都不相等，包括 NaN 本身**

  ```
  alert( NaN == NaN ) //false 自我否定
  ```


isNaN(参数 n)

判断参数 n 是否是"非数值"。如果是数值返回 false,不是数值返回 true;

说明：isNaN()在接收到一个值之后，会尝试将这个值转换为数值。

```

    alert(isNaN(NaN)); //true
    alert(isNaN(10)); //false(10是一个数值)
    alert(isNaN("10")); //false(可以被转换成数值10)
    alert(isNaN("hello")); //true(不能转换成数值)
    alert(isNaN(true)); //false(可以被转换成数值1)

```

- String -- 字符串类型 （存放在堆内存当中）

  字符串可以由双引号或者单引号表示。
```
  var str = "hello world";
  var str = 'hello world';
```
数据类型包含一些特殊的字符字面量，也叫转义序列(字符)，用于表示非打印字符

        \n  换行
        \t  制表
        \b  空格
        \r  回车
        \f  换页

查看字符串的长度：length 属性

```

var str = "hello world";
console.log(str.length);//11

```

查看字符串相应位置的字符。

```

var str = "hello world";
console.log(str[1]);//e

```

- Object -- 类型 ：ECMAScript 中的对象其实就是一组数据和功能的集合

```

var o = {}; \\对象字面量方法创建

var o = new Object(); \\构造函数方法创建

```

2、typeof 操作符

作用:检测变量的数据类型 返回结果都是 string 类型

typeof 两种使用法:

    typeof 变量名

    typeof(变量名)

可能返回以下字符串: 少了个 null 多了个 function（函数）

    "undefined" ==>  如果这个值未定义
    "boolean"   ==>  如果这个值是布尔值
    "number"    ==>  如果这个值是数值
    "string"    ==>  如果这个值是字符串
    "object"    ==>  如果这个值是对象或null
    "function"  ==>  如果这个值是函数

数据类型有哪些?

 5 种基本数据类型
```
undefined null boolean number string
```
1 种复杂数据类型  object


typeof 操作符会返回哪些值?
```
"undefined" "number" "boolean" "string" "object" "function"
```
