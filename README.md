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

- v-text: 元素的textContent属性,必须是双标签 跟`{{ }}`效果是⼀样的,使⽤较少。

- v-html: 元素的innerHTML。

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
                msg:"插入值",
                htmlMsg:'<h3>插入的标签</h3>'
            }
        })
    </script>
</body>
</html>
```

- v-if / v-else-if / v-else: 判断是否插⼊这个元素,相当于对元素的销毁和创建。

- v-show: 隐藏元素 如果确定要隐藏, 会给元素的style加 上display:none。是基于css样式的切换。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>条件渲染</title>
</head>

<body>
    <div id='app'>
        <div v-if="isShow">
            显示
        </div>
        <div v-else>
            隐藏
        </div>
        <h3 v-show='show'>显示</h3>
    </div>
</body>

</html>
<script src="./vue.js"></script>
<script>
    // v-if v-else-if  v-else v-show
    new Vue({
        el: '#app',
        data: {
            isShow: Math.random() > 0.5,
            show: true
        }
    })
</script>
```

> v-if 是“真正”的条件渲染，因为它会确保在切换过程中条
件块内的事件监听器和⼦组件适当地被销毁和重建。

> v-if 也是惰性的：如果在初始渲染时条件为假，则什么也
不做——直到条件第⼀次变为真时，才会开始渲染条件块。
相⽐之下， v-show 就简单得多——不管初始条件是什么，
元素总是会被渲染，并且只是简单地基于 CSS 进⾏切换。

> ⼀般来说， v-if 有更⾼的切换开销，⽽ v-show 有更⾼的
初始渲染开销。因此，如果需要⾮常频繁地切换，则使⽤
v-show 较好；如果在运⾏时条件很少改变，则使⽤ v-if
较好

- v-bind 给元素的属性赋值
  - 语法 在元素上 `v-bind:属性名="常量||变量名"`
  - 简写形式 `:属性名="变量名`

- v-on 处理⾃定义原⽣事件的,给按钮添加click并让使⽤变量的
样式改变
  - 普通使⽤ `v-on:事件名="表达式||函数名"`
  - 简写⽅式 `@事件名="表达式"`

- v-model 双向的数据绑定

- v-for 循环渲染
  - 基本语法 `v-for="item in arr"`
  - 对象的操作 `v-for="item in obj"`
  - 如果是数组没有id
    - `v-for="(item,index) in arr" :key="index"`
  - v-for的优先级最⾼

## 四、 监听器 watch

计算属性允许我们声明性地计算衍生值。然而在有些情况下，我们需要在状态变化时执行一些“副作用”：例如更改 DOM，或是根据异步操作的结果去修改另一处的状态。

在选项式 API 中，我们可以使用 watch 选项在每次响应式属性发生变化时触发一个函数。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>侦听器watch</title>
</head>

<body>
    <div id='app'>
        <input type="text" v-model='msg'>
        <h3>{{msg}}</h3>
        <h3>{{stus[0].name}}</h3>
        <button @click='stus[0].name = "Tom"'>改变</button>
    </div>
    <script src="./vue.js"></script>
    <script>
        // 基本的数据类型可以使用watch直接监听，复杂数据类型Object Array 要深度监视
        new Vue({
            el: '#app',
            data: {
               msg:'',
               stus:[{name:'jack'}]
            },
            watch: {
                // key是属于data对象的属性名 value:监视后的行为 newV :新值 oldV:旧值
                'msg':function(newV,oldV){
                    // console.log(newV,oldV);
                    if(newV === '100'){
                        console.log('hello');
                    }
                    
                },
                // 深度监视： Object |Array
                "stus":{
                    deep:'true',
                    handler:function(newV,oldV){
                        console.log(newV[0].name);
                        
                    }
                }
            },
        })
    </script>
</body>

</html>
```

## 五、 计算属性 computed

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>computed</title>
</head>

<body>
    <div id='app'>
        {{reverseMsg}}
        <h3>{{fullName}}</h3>
        <button @click='handleClick'>改变</button>
    </div>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                msg: 'hello world',
                firstName: '小马',
                lastName: '哥'
            },
            methods: {
                handleClick(){
                    this.msg = '计算属性computed';
                    this.lastName = '妹';
                }
            },
            computed: {
                // computed默认只有getter方法
                // 计算属性最大的优点：产生缓存 如果数据没有发生变化 直接从缓存中取
                reverseMsg: function () {
                    return this.msg.split('').reverse().join('')
                },
                fullName: function () {
                    return this.firstName + this.lastName;
                }
            },

        })
    </script>
</body>

</html>
```

## 六、 案例 音乐播放

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>音乐播放</title>
</head>

<style>
    * {
        padding: 0;
        margin: 0;
    }

    ul {
        list-style: none;
    }

    ul li {
        margin: 20px 20px;
        padding: 10px 5px;
        border-radius: 3px;
    }

    ul li.active {
        background-color: #D2E2F3;
    }

    button {
        width: 100px;
        height: 54px;
    }

    button:hover {
        background-color: black;
        color: gold;
    }
</style>

<body>
    <div id="app">
        <audio :src="musicData[currentMusicIndex].songSrc" controls autoplay @ended="endedNext()"></audio>
        <button @click="nextMusic()">下一首</button>
        <ul>
            <li :class="{active:index===currentMusicIndex}" v-for="(item,index) in musicData" :key="index"
                @click="clickMusic(item.id)">
                <h2>{{index+1}}-歌名：{{item.name}}</h2>
                <p>{{item.author}}</p>
            </li>
        </ul>
    </div>
</body>

</html>
<script src="./vue.js"></script>
<script>
    // 数据必须放在前面 new Vue()才能调用
    const musicData = [{
        id: 1,
        name: '葛东琪 - 悬溺',
        author: '葛东琪',
        songSrc: 'http://music.163.com/song/media/outer/url?id=1397345903.mp3'
    },
    {
        id: 2,
        name: '郭顶 - 凄美地',
        author: '郭顶',
        songSrc: 'http://music.163.com/song/media/outer/url?id=436346833.mp3'
    },
    {
        id: 3,
        name: '队长 - 予你',
        author: '队长',
        songSrc: 'http://music.163.com/song/media/outer/url?id=1895330088.mp3'
    },
    {
        id: 4,
        name: '颜人中 - 我只能离开',
        author: '颜人中',
        songSrc: 'http://music.163.com/song/media/outer/url?id=1398283847.mp3'
    },
    {
        id: 5,
        name: '烟(许佳豪) - 删了吧',
        author: '烟(许佳豪)',
        songSrc: 'http://music.163.com/song/media/outer/url?id=1891469546.mp3'

    },
    {
        id: 6,
        name: '于荣光 - 少林英雄',
        author: '于荣光',
        songSrc: './static/于荣光 - 少林英雄.mp3'
    },
    {
        id: 7,
        name: 'Joel Adams - Please Dont Go',
        author: 'Joel Adams',
        songSrc: './static/Joel Adams - Please Dont Go.mp3'
    },
    {
        id: 8,
        name: 'MKJ - Time',
        author: 'MKJ',
        songSrc: './static/MKJ - Time.mp3'
    },
    {
        id: 9,
        name: 'Russ - Psycho (Pt. 2)',
        author: 'Russ',
        songSrc: './static/Russ - Psycho (Pt. 2).mp3'
    }
    ];

    new Vue({
        el: "#app",
        data: {
            musicData,
            currentMusicIndex: 0
        },
        methods: {
            //点击切换
            clickMusic(index) {
                this.currentMusicIndex = index - 1;
            },
            //下一曲
            nextMusic() {
                if (this.currentMusicIndex === this.musicData.length - 1) {
                    this.currentMusicIndex = 0;
                } else {
                    this.currentMusicIndex++;
                }
            },
            endedNext() {
                this.nextMusic();
            }
        },
    });
</script>
```