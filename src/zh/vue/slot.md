# slot

#### 1. 单个插槽

- 子组件模板==包含至少一个 slot ==插口,否则父组件的内容将会==被丢弃==。

最初在 slot 标签中的任何内容都被视为备用内容,备用内容在子组件的作用域内编译,并且只有在宿主元素为空,且没有要插入的内容

**子组件**

```
    <header>
        <span></span>
        <slot>713</slot>
        <span></span>
    </header>
```

**父组件**

```
//如果此时子组件里面没有slot这个插口的话,父组件里面的b标签将会被丢弃
<my-header>
    <b>标题</b>
</my-header>
```

- 档子组件模板只有一个没有属性的插槽时,父组件传入的整个内容片段将插入到插槽所在的 DOM 位置,并替换掉

```
//整个ul都会替换插槽标签本身
<my-header>
    <ul>
        <li></li>
    </ul>
</my-header>
```

#### 2. 具名插槽

slot 元素可以用一个特殊的特性 name 来进一步配置如何分发内容,多个插槽可以有不同的名字,具名插槽将匹配内容片段中有对应 slot 特性的元素

**子组件**

```
<slot name="插槽名"></slot>
```

父组件

```
<template>
    <!--同一个组件出现多个slot需要使用template-->
    <button></button>//html结构
</template>
```

#### 3. 作用域插槽

作用域插槽就是父组件在调用子组件的时候给子组件传了一个插槽,这个插槽为作用域插槽。

该插槽必须放在 template 标签里面,同时声明从子组件接收的数据放在一个自定义属性内,并定义该数据的渲染方式。

**子组件**

```
<slot :list="list" name="default" :names="11"></slot>
```

**父组件**

```
//obj里面存放的是从插槽获取发哦的所有属性

<template>
    <ul>
        <li v-for="(item,index) in obj.list" :key="index">{{item.title}}</li>
    </ul>
</template>
```
