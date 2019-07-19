# DOM

1. DOM ==> 文档对象模型 document object model

   提供了与页面进行交互的 API(应用程序接口)

2. DOM 级别

   DOM0 DOM2 DOM3

3. 标签 ==> 元素 ==> 节点

4. 获取节点的方法
   - document.getElementById( "idName" );
     功能: 获取页面下指定 ID 名的节点
     ==> 如果存在,只能获取一个,因为 ID 是唯一的
     ==> 如果不存在,返回 null


    - dom.getElementsByTagName( "tagName" );

    	功能: 获取标签的集合 ==> 伪数组

    	- 获取页面下所有li的集合
    		```
    		document.getElementsByTagName( "li" );
    		```
    	- 获取指定节点下所有li的集合
    		```
    		document.getElementById("ulId").getElementsByTagName("li");
    		```

    - dom.getElementsByName()

    	功能: 获取一组元素通过 name 属性 ==> 伪数组


    - dom.getElementsByClassName()

    	功能: 获取一组元素通过class类名 ==> 伪数组


    - document.querySelector()

    	功能: 获取页面下第一个指定的ID或者类或者标签名的节点


    - document.querySelectorAll()

    	功能: 获取页面下所有的类或者ID或者标签名的节点

5. 什么是节点( node )

   标签 ==> 元素 ==> 节点
   DOM 节点

   - 根据 W3C 的 HTML DOM 标准，HTML 文档中的所有内容都是节点：
   - 整个文档是一个文档节点
   - 每个 HTML 元素是元素节点
   - HTML 元素内的文本是文本节点
   - 每个 HTML 属性是属性节点
   - 注释是注释节点

6. DOM 树

   HTML DOM 将 HTML 文档视作树结构。这种结构被称为节点树
   **html 是 根元素**

7)  节点的分类

    Node.ELEMENT_NODE (1) ==> 元素节点
    Node.ATTRIBUTE_NODE (2) ==> 属性节点
    Node.TEXT_NODE (3) ==> 文本节点
    Node.COMMENT_NODE (8) ==> 注释节点
    Node.DOCUMENT_NODE (9) ==> 文档节点

        	```

     <div id="box" class="active">hello world</div>
    		```
     div ==> 元素节点   
    		id , class ==> 属性节点  
    		hello world ==> 文本节点

8. 节点的三个属性

   - nodeName ==> 节点名
   - nodeType ==> 节点类型
   - nodeValue ==> 节点值

| 节点类型 | nodeName         | nodeType | nodeValue         |
| -------- | ---------------- | -------- | ----------------- |
| 元素节点 | tagName(大写)    | 1        | null              |
| 属性节点 | attrName(属性名) | 2        | attrValue(属性值) |
| 文本节点 | #text            | 3        | 文本内容          |


9. 节点层级关系
- 标准浏览器下识别空白文本节点
   // 标准浏览器: 谷歌 火狐 IE8 以上版本
   - firstChild ==> 第一个子节点
   - lastChild ==> 最后一个子节点
   - nextSibling ==> 下一个同胞节点
   - previousSibling ==> 上一个同胞节点
   - childNodes ==> 子节点集合

- 不识别空白文本节点
    - firstElementChild ==> 第一个元素子节点
    - lastElementChild  ==> 最后一元素个子节点
    - nextElementSibling ==> 下一个元素同胞节点
    - previousElementSibling ==> 上一个元素同胞节点
    - children ==> 元素子节点集合


- 父节点
    - parentNode ==> 父节点
