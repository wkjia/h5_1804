Vue 的核心库只关注视图层
Vue是数据驱动框架
Vue一切的开端都是以Vue开始的，必须要有一个实例
#Vue是一个前端js框架，由尤雨溪（尤小右）开发，是个人项目
只要做Vue的东西，必须要有一个实例
Vue可以有多个作用域，既是可存在多个实例，多次new

在实例创建选项，el创建实例的地盘，不能直接把body作为自己的地盘
#el(element的简写)
{{}}叫表达式，mustach  ，在表达式中可以写入js表达式去实现 取值 计算等等，注意表达式不是js代码

如果el指向的元素有多个，默认只会选择第一个元素，其他不产生作用，所以Vue的元素一般使用id名称，不使用类名
#data
1、里面数据可以存放数据，除了函数，其他数据类型都可以存放，通过表达式{{}}使用
2、在配置中同过设置data属性来为实例绑定数据
数据 - 属性

#{{}}
{{}}代替jquery的$(").text()的用法
#：（冒号）
:代替jquery的$(").attr()的用法
如果在属性值前面加了冒号，就会去找data存储的数据里面的属性值替换

|x|x|
|-|-|
|jQuery|节点驱动|
|Vue|数据驱动|

{{}}代替$("").text()
:代替$("").attr()
@事件名称 代替$("").click


```js
    data{
        mwssage:`heillo world`
    }
```
# mvc mvvm mvp ，这些东西都是设计思想、设计模式

    应用于设计应用结构的思想，就是思想

    MVC觉得，应用应该分为三层：Mode（数据模型）、View（视图）、Controller（控制层）

    MVC其实是一个后端的思想，所以完全套入到前端的时候会有些不协调
    通过controler层控制M层数据在V层进行显示

    把数据与视图连接好之后，建立之后就不用担心，数据如何显示是到视图了，只需要想把发更改数据就可以了
    只要数据更新，视图也就更新

    伪MVC

    更改数据、渲染数据都应该在控制器中

## mvvm

```
1、首先，M层的数据是挂靠在VM上的，VM利用表达式等东西与V层进行双向绑定，就能达到这样的效果：
    数据可以直接在视图上显示，当视图产生用户操作的时候，会直接去更新VM对应的数据，数据更新之后，
    VM得知了，然后视图也会马上再去进行更新

2、所以说，MVVM的核心就在VM层和V层是双向绑定的，只要数据变化后，VM得知后，V层就会马上更新，V层接收到指令后也会立即将VM对应的数据更新

    V层和VM层很多方面都是双向的。


```
### mvvm的原理

Vue中使用了一个叫做Object.defineproperty的ES5的api(不能兼容ie8及以下版本)


# 缩写

## v-bind 缩写
```js
  <!--完整写法-->
  <img v-bind:src="'../imgs/red.jpg'" alt="" />
  <!--缩写-->
  <img :src="src" alt="" />

  当属性为 style、class时，注意接收的对象
  <p :style={color:red,fontSize:30px}></p>
```

## v-on 缩写

- [事件处理](https://cn.vuejs.org/v2/guide/events.html)

1、事件处理方法：
示例：
```js
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})

// 也可以用 JavaScript 直接调用方法
example2.greet() // => 'Hello Vue.js!'

```
2、内联处理器的方法

除了直接绑定到一个方法，也可以在内联 JavaScript 语句中调用方法：
```js
<div id="example-3">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>
new Vue({
  el: '#example-3',
  methods: {
    say: function (message) {
      alert(message)
    }
  }
})
```

有时也需要在内联语句处理器中访问原始的 DOM 事件。可以用特殊变量 $event 把它传入方法：

```js
<button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>
// ...
methods: {
  warn: function (message, event) {
    // 现在我们可以访问原生事件对象
    if (event) event.preventDefault()
    alert(message)
  }
}


//事件监听
  <!--完整语法-->
  <button v-on:click="greet">Greet</button>
  <!--缩写语法-->
  <button @click="greet">Greet</button> 
//事件委托
  事件源对象 $event  

//阻止事件冒泡：
<button @click.stop='maopao'></button>

```
# 事件修饰符
```js
在事件处理程序中调用 event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。

为了解决这个问题，Vue.js 为 v-on 提供了事件修饰符。之前提过，修饰符是由点开头的指令后缀来表示的。

.stop
.prevent
.capture
.self
.once
.passive

<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 v-on:click.prevent.self 会阻止所有的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。

2.1.4 新增

<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>
不像其它只能对原生的 DOM 事件起作用的修饰符，.once 修饰符还能被用到自定义的组件事件上。如果你还没有阅读关于组件的文档，现在大可不必担心。




```
# 指令

指令（Directive），换句话说就是元素的自定义属性，在 Vue 中是以 v- 为前缀的自定义属性，属性值为对象或 js 表达式

## 文本
```js
v-text 相当于$().text()

v-html 相当于$().html()

v-show  相当于$().show() 接受布尔值

v-if 相当于$().append() $().remove()  增加或则删除节点 只接受布尔值

v-else-if  类似上一条

v-else 不接收事件 一般跟v-if连在一起用  限制：前一兄弟元素必须有 v-if 或 v-else-if。

v-for  谁要重复就在谁上面写v-for,重复多少次取决于遍历数组元素的长度

v-model 相当于jquery的$(.val() 双向数据绑定  只能用在三个标签里面 input select textarea
```
v-model 双向数据绑定 实现的是一个功能，而mvvp是一个双向绑定的原理

### 修饰符

<input v-model.lazy = 'num' type="text">
<input v-model.number = 'num' type="text">
<input v-model.trim = 'num' type="text">
```js
 // Vue实现MVVM的特点是 双向绑定 
        
        //v-model 可以让input的value和某一个数据进行完全的对应
        //v-model实现的是一个功能: 双向数据绑定
        //.lazy 就是把底层使用的input事件改成了change事件
        //.number将输入的内容转换成number，转换不了的话就用原来的值
        //trim去掉首尾空格
```
```js
v-bind 相当于jquery的$().attr()/css()、$().addclass()

//声明式渲染||数据驱动

        // 视图中所有的显示变化的情况，都应该有一条数据来与之对应
实现功能的思路：
        //给某一个按钮加上red类名
        // 1. 定义关键数据
        // 2. 让数据与视图建立联系
        // 3. 在适当的情况下去更改数据
```

# v-for

## 可以遍历数组，也可以遍历对象

## 数组
```js

在 v-for 块中，我们拥有对父作用域属性的完全访问权限。v-for 还支持一个可选的第二个参数为当前项的索引。

<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```
## 对象
```js
你也可以用 v-for 通过一个对象的属性来迭代。
1、
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>

2、
你也可以提供第二个的参数为键名：

<div v-for="(value, key) in object">
  {{ key }}: {{ value }}
</div>

3、
第三个参数为索引：

<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }}: {{ value }}
</div>

```
# vue-for_key
```js
div id="app">
      <ul>
         
          <li  v-for = '(num, i) in numbers' :key = 'i' > {{num}} </li>

      </ul>
    </div>
    <!-- <script src="https://cdn.bootcss.com/vue/1.0.22/vue.js"></script> -->
    <script src="./base/vue.js"></script>
    <script>
 ```
  当数据中有重复数据的时候，可能会引起报错
  数据变化之后，vue要进行重新的循环渲染，这个时候为了能达到复用（有的数据没有改变），所以就会去对比，这次的数据和上次的数据哪里发生了变化，vue在对比的时候，需要我们去添加一个属性key
    
  所以在循环的时候需要给dom添加动态的key ,保证key都不相同，这样的话能提高vue对比的效率，提高性能

```js
    var vm = new Vue({
          el:'#app',
          data: {
             numbers: [1,1,2,2,3,3,4,5,6,6]
          }
      })

```
# v-for_template
```js

    <div id="app">
        {{ 1+2 }}
        <template v-for = 'phone in phones '>
            <h1>{{phone.name}}</h1>
            <p>价格：{{phone.price}} </p>
        </template>
        
    </div>
    <script src="./base/vue.js"></script>
    <script>
    // vue提供了template标签供我们使用，在渲染视图的时候其实不会渲染template
    // 记住，body中写的假的！！！！！！
    // 当我们在#app中编写实例的结构之后，其实vue会将这些东西重新编译之后进行重新的渲染
        var vm = new Vue({
            el:'#app',
            data:{
                phones: [
                    { name: 'iphoneX', price: 8000 },
                    { name: '小米8', price: 4000 },
                    { name: '华为V10', price: 5000 },
                    { name: 'oppo R11', price: 3000 }
                ]
            }
        })
    </script>

```
## 在vue中，提供了v-for工具来帮助我们去循环数据
v-for其实是一个指令
1. 带v-的都是指令 2. vue有很多指令
3. 指令是用在视图中标签上的
4. 指令的作用就是（根据数据）操作dom

```
```
## v-clock
```
这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 [v-cloak] { display: none } 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。
```
## v-pre
```
跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

就是不会编译html中{{}},会以原始{{}}显示
```
# 计算属性和侦听器

## 计算属性： 根据一个现有的数据，生成一个新的数据，并且新数据与原有数据建立联系，当原有数据变化的时候，新数据也会变化

模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。例如：

<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
在这个地方，模板不再是简单的声明式逻辑。你必须看一段时间才能意识到，这里是想要显示变量 message 的翻转字符串。当你想要在模板中多次引用此处的翻转字符串时，就会更加难以处理。

所以，对于任何复杂逻辑，你都应当使用计算属性。

## 计算属性
本质就是：计算后把旧的值变成新的值
computed

## 计算属性缓存 vs 方法

我们可以通过在表达式中调用方法来达到同样的效果：

```js
<p>Reversed message: "{{ reversedMessage() }}"</p>
// 在组件中
methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}

```
我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是计算属性是基于它们的依赖进行缓存的。只在相关依赖发生改变时它们才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。

这也同样意味着下面的计算属性将不再更新，因为 Date.now() 不是响应式依赖：

```js
computed: {
  now: function () {
    return Date.now()
  }
}
```
相比之下，每当触发重新渲染时，调用方法将总会再次执行函数。

我们为什么需要缓存？假设我们有一个性能开销比较大的计算属性 A，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 A 。如果没有缓存，我们将不可避免的多次执行 A 的 getter！如果你不希望有缓存，请用方法来替代。

# 组件

组件是可复用的Vue实例，且带有一个名字

组价的意义在于：封装html、js，方便管理

组件的特性：自己封闭的王国，只会影响自己，每个组件高度独立
```js

这里有一个 Vue 组件的示例：

// 定义一个名为 button-counter 的新组件
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
组件是可复用的 Vue 实例，且带有一个名字：在这个例子中是 <button-counter>。我们可以在一个通过 new Vue 创建的 Vue 根实例中，把这个组件作为自定义元素来使用：

<div id="components-demo">
  <button-counter></button-counter>
</div>
new Vue({ el: '#components-demo' })

```

# Vue cli

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统,依赖node环境

用npm run serve 能打开服务器是因为我们在生成package.json中定义了一个scripts
```js
"scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint"
  }
  ```

## 全局安装手脚架

```js
npm install -g @vue/cli

验证它是否安装成功：vue --version

```
## 第二步 在一个文件夹下，打开命令行，输入以下的命令来初始化一个项目
```js
vue  create 项目名字(英文，比如v-project)

```
使用图形化界面
你也可以通过 vue ui 命令以图形化界面创建和管理项目

```js
vue ui

```

## 第三步
```js
cd vue-project //定位到我们的项目文件夹位置
npm run serve
```
## 组件样式的作用范围

scoped 限定样式只作用于自身组件范围内的html


## 组件复用：
## Prop

Prop 是你可以在组件上注册的一些自定义特性。当一个值传递给一个 prop 特性的时候，它就变成了那个组件实例的一个属性。

  通过Prop向子组件传递数据

  在子组件的标签中，写入属性
  在组件中，通过Prop引入属性 Prop:['type']

  意义：组件复用时，想复用的组件呈现不同的状态



# 路由（Vue-router)

安装：

```bash
npm install vue-router

```
- [vue网址](https://cn.vuejs.org/v2/guide/routing.html)
- [vur-router](https://router.vuejs.org/installation.html#direct-download-cdn)

（脚手架中）配置路由：

在main.js里面引入:
```js
import VueRouter from 'vue-router'
Vue.use(VueRouter)
```
getting started:
```
定义路由组件
```js
```
定义路由：
(点击不同的路由，进入到不同的页面)
```js
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]
```

创建实例
```js
const router = new VueRouter({
  routes // short for `routes: routes`
})
```

# 生命周期
```
```
## watch(监听数据的变化)
```js
 watch: {
        todos: {
            deep: true,//深度监听
            handler() {//监听数据的变化
                localStorage.todo_id = this.todo_id;
                localStorage.todos = JSON.stringify(this.todos);
            }
        }
    }
```
# CDN(课外知识点)
- [了解CND](https://blog.csdn.net/qq_21891743/article/details/79642605)

CND概况

CDN的全称是Content Delivery Network，即内容分发网络。

CND加速主要是加速静态资源，如网站上面上传的图片、媒体，以及引入的一些Js、css等文件。

CND加速需要依靠各个网络节点，例如100台CDN服务器分布在全国范围，从上海访问，会从最近的节点返回资源，这是核心。

CND服务器通过缓存或者主动抓取主服务器的内容来实现资源储备。


