# Vue入门

## 一、什么是 Vue？ ​

Vue (发音为 /vjuː/，类似 view) 是一款用于构建用户界面的 JavaScript 框架。它基于标准 HTML、CSS 和 JavaScript 构建，并提供了一套声明式的、组件化的编程模型，帮助你高效地开发用户界面。无论是简单还是复杂的界面，Vue 都可以胜任。

## 二、 Vue起步

### 1. 引包

```html
<script src="vue.js"></script>
//也可以直接通过 CDN 来使用 Vue
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

### 2. 启动

```html
<script>
    new Vue({
        el: '#app',//⽬的地
        data: {
            //保存数据的地⽅ 
            msg: 'Hello Vue'
        }
    });
</script>
```

### 3. 差值表达式 `{{}}`

最基本的数据绑定形式是文本插值，它使用的是“Mustache”语法 (即双大括号)：

```html
<div id="app">{{msg}}</div>
```

双大括号标签会被替换为相应组件实例中 msg 属性的值。同时每次 msg 属性更改时它也会同步更新。

整个网页代码：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue 起步</title>
</head>

<body>
    <div id="app">{{msg}}</div>
</body>

</html>
<script src="vue.js"></script>
<script>
    new Vue({
        el: '#app',//⽬的地
        data: {
            //保存数据的地⽅ 
            msg: 'Hello Vue'
        }
    });
</script>
```

效果：

![](https://s2.loli.net/2023/10/15/se731nCVf89zXk2.png)

## 三、 Vue 指令

### 1. 什么是指令

- 在vue中提供了⼀些对于⻚⾯ + 数据的更为⽅便的输出,这些操作就叫做指令, 以v-xxx表示：
    - ⽐如html⻚⾯中的属性 `<div v-xxx ></div>`
- ⽐如在angular中 以ng-xxx开头的就叫做指令。
- 在vue中 以v-xxx开头的就叫做指令。
- 指令中封装了⼀些DOM⾏为, 结合属性作为⼀个暗号, 暗号有对应的值,根据不同的值，框架会进⾏相关DOM操作的绑定。

### 2. Vue 常见指令

- v-text:元素的textContent属性,必须是双标签 跟`{{ }}`效果是⼀样的,使⽤较少。

- v-html:元素的innerHTML。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>指令之v-text和v-html</title>
</head>
<body>
    <div id='app'>
        <h1>{{ msg }}</h1>
        <h2 v-text='msg'></h2>
        <div v-html='htmlMsg'></div>
    </div>
    <script src="./vue.js"></script>
    <script>
        // {{}}和v-text的作用是一样的 都是插入值 直接渲染 innerText
        // v-html既能插入值 又能插入标签 innerHTML
        new Vue({
            el:'#app',
            data:{
                msg:"插入标签",
                htmlMsg:'<h3>小马哥</h3>'
            }
        })
    </script>
</body>
</html>
```

