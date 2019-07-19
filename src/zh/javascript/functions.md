# 函数

1. 函数的概念

函数是指由事件驱动或可重复调用执行的代码块。

```
btn.onclick = function(){
    alert("OK");
}
function runYear( min , max ){
    for(var i=min;i<=max;i++){
        if( i%4 == 0 && i%100 != 0 || i%400 == 0 ){
            document.write( i + " " );
        }
    }
}
runYear( 2000 , 3000 );
document.write("<hr />");
runYear( 3000 , 4000 );
```

2. 函数的好处

   一次声明多次调用 ==> 节省代码量 ==> 执行效率提高 ==> 页面加载速度提高 ==> 用户体验提高

3. 定义函数的关键字 ==> function

4) 函数分为

   - 有名函数
   - 匿名函数

5) 定义函数的两种方式

   - 函数表达式 ==> 将一个匿名函数赋值给一个变量

   ```
   var num = 10; // num ==> 变量名
   var fn = function(){ // fn ==> 函数名
       alert("OK");
   };

   // 构造函数: var fn = new Function();
   ```

   - 函数声明 ==> 使用最多

   ```
   语法结构 ==> function funName(){ }
       function fn(){
           alert("OK");
       }
   ```

6) 函数表达式和函数声明的区别
   - 函数表达式:先定义后调用 ==> 先调用,报错
   ```
   fn();// 报错:fn is not a function
   var fn = function(){};
   fn();// 成功执行
   ```
   - 函数声明:无论在哪调用都能成功执行 ==> 函数声明有提升的过程
   ```
   fn();// 成功执行
   function fn(){}
   fn();// 成功执行
   ```
7) 函数调用( 执行函数 ) ==> 函数名( 实参 1,实参 2... )

8) 函数参数

   1. 实参 ==> 真实参数
   2. 形参 ==> 形式参数
      规则:
      - 实参与形参是一一对应的 。
      - 如果形参没有接收到传递进来的实参,该形参默认保存 undefined ==>
        声明变量但未赋值。
      - 形参是局部变量,当函数执行完毕会自动销毁。
      ```
      function addNum( num1 , num2 , num3 ){ // num1,num2 形参 num1 = 10,num2 = 20
        console.log( num1 );// 10 ==> 规则 1
        console.log( num2 );// 20 ==> 规则 1
        console.log( num1 + num2 );// 30
        console.log( num3 );//undefined ==> 规则 2
      }
      addNum( 10 , 20 );// 10 , 20 实参
      console.log( num1 );// 报错:num1 is not defined ==> 规则 3
      ```

9. return
   规则:
   - return 有返回值的功能,将值返回到调用函数的那个地方
   - return 后的代码将不会被执行 ==> return 有终止函数的功能 ==> 类似循环语句的 break
   - 每一个函数都有返回值,没有用 return 或者用了 return 但什么都没返回,默认返回 undefined
    ```
    function addNum( num1 , num2 ){
        return num1 + num2;
        alert("OK");// 不会执行
    }
    var sum = addNum( 10 , 20 );
    console.log( sum );// 30
    console.log( addNum( 10 , 20 ) );// 30
    ```
10. 使用 return 的情况
    - 当需要返回值的时候就需要使用 return
    - 当需要强制结束函数时 需要使用 return
    - 修改页面的样式时,就不需要使用 return

11. arguments ==> arguments 是对象,以数组的形式保存着实参的集合,但它并不是数组的实例
    用途:解决传递多个参数
    ```
    arguments.length ==> 传递实参的个数
    function addNum(){
        //_console.log( arguments );// [10,20,30]
        console.log( typeof arguments );//"object"
        // 数组的第一项 ==> 第一个实参
        console.log( arguments[0] );// 10
        // arguments.length ==> 实参的个数
        console.log( arguments.length );// 3
        var sum = 0;
        for(var i=0;i<arguments.length;i++){
            sum += arguments[i];
        }
        return sum;
    }
    var sum = addNum( 10 , 20 , 30 , 40 , 50 , 60 )
    console.log( sum );
    // 面试题
    function fn( num1 , num2 ){
        arguments[0] = 50;
        console.log( num1 );// 50
    }
    fn( 10 , 20 );
    ```
12. JS 没有函数重载 ==> 后声明的函数会覆盖先声明的函数 
```
    fn();
    function fn(){
        alert(1);
    }

    function fn(){
        alert(2);
    }
```
13. 模拟函数重载 ==> 多态 
```
    arguments.length ==> 传递实参的个数
    function fn(){
        if( arguments.length == 1 ){
            alert( arguments[0] );
        }else if( arguments.length == 2 ){
            alert( arguments[0] + arguments[1] );
        }
    }
    fn( 10 );
    fn( 10 , 20 );
```
14. 函数是对象,函数名是指针
```
    function fn(){
        alert("ok");
    }
    console.log( typeof fn );// "function"
    console.log( fn instanceof Function );// true
    console.log( fn instanceof Object );// true

    function sum( num1 , num2 ){
        return num1 + num2;
    }
    console.log( sum( 10 , 20 ) );// 30
    var anotherSum = sum;
    console.log( anotherSum( 20 , 30 ) );// 50

    sum = null;// 解除了 sum 与函数体的指引
    // console.log( sum( 10 , 20 ) );// 报错:sum is not a function
    console.log( anotherSum( 10 , 20 ) );//30
```
15. this ==> 上下文
    this 是指包含他的函数 作为方法被调用时 所属的对象
    ```
    btn.onclick = function(){
        console.log( this );// btn
    }
    ```
16. 闭包 ==> 函数里有函数 
    有权访问另外一个作用域的函数
```
    function fn(){
        var num = 10;
        return function(){
            return num;
        };
    }
    console.log( fn()() );// 10

    // 匿名函数的自我执行
    (function(num1,num2){
        alert(num1+num2);
    })(10,20);
    /*(function(){
        alert("ok");
    }());*/
```
