[toc]

# Vue的基本指令

[Vue官方网站](https://vuejs.org/ )

[Vue官方网站(中文)](https://cn.vuejs.org/ )

什么是指令？

​		 指令 (Directives) 是带有 `v-` 前缀的特殊特性。指令特性的值预期是**单个 JavaScript 表达式** (`v-for` 是例外情况，稍后我们再讨论)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。 

## 编写第一个HelloWorld

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>Helloworld</title>
</head>
<body>
<h1>Hello World</h1>
<hr>
<div id="app">
    {{message}}
</div>

<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        }
    })
</script>
</body>
</html>
```

运行后显示结果为

![image-20191207103438165](./assets/img/readme/helloworld.png)

```html
<div id="app">
    {{message}}
</div>
```

{{message}}用的是插值表达式获取到实例中的数据

```javascript
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        }
    })
</script>
```

这里创建了一个vue实例

el:里填写的则是一个页面上已存在的DOM元素作为Vue实例的挂载目标。可以是CSS选择器，也可以是一个HTMLElement实例。

el:'#app'则相当于让Vue接管这片区域

data:{...}中则是定义数据

___写代码时别忘记导入vue.js___

[Vue官方文档: 声明式渲染](https://cn.vuejs.org/v2/guide/#%E5%A3%B0%E6%98%8E%E5%BC%8F%E6%B8%B2%E6%9F%93)

## v-if & v-show

**`v-if`的使用：**

**v-if:是vue 的一个内部指令，指令用在我们的html中。**

**v-if 用来判断是否加载html的DOM，比如我们模拟一个用户登录状态，在用户登录后现实用户名称。**

*`v-show` 功能与v-if类似，都是判断是否显示某个值，可v-show是通过样式修改*

~~~html
<body>
<h1>v-if&v-else&v-show</h1>
<hr>
<div id="app">
    <div v-if="isLogin">你好,欢迎 这是v-if</div>
    <div v-else>请登陆!</div>

    <div v-show="isLogin">你好,欢迎 这是v-show</div>
</div>

<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            isLogin: true
        }
    })
</script>
</body>
~~~

除了`v-if`还有`v-else`，若`v-if`和`v-else`同时出现，当`v-if`不满足条件时则会显示`v-else`。

当isLogin为true时，显示结果为

![Image text](./assets/img/readme/v-if&v-show.png)



当isLogin为false时，显示结果为

![Image text](./assets/img/readme/v-if&v-show2.png)

***v-if如果为false   则不加载       可以减轻服务器的压力，在需要时加载***

***v-show为false则是修改css样式display="none"  仍然加载    可以使客户端操作更加流畅***

![Image text](./assets/img/readme/v-ifvsv-show.png)

[Vue官方文档: 条件渲染](https://cn.vuejs.org/v2/guide/conditional.html )

## v-for

 `v-for` 指令基于一个数组来渲染一个列表。`v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 `items` 是源数据数组，而 `item` 则是被迭代的数组元素的**别名**。 

~~~html
<body>
    <h1>v-for</h1>
    <hr>
    <div id="app">
        <ul>
            <li v-for="item in array" >
                {{item}}
            </li>
        </ul>
    </div>
    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data :{
                array:[1,2,3,'aaa','bbb'],
            }
        })
    </script>
</body>
~~~

运行结果:

![Image-text](./assets/img/readme/v-for1.png)

`v-for`还支持一个可选的第二个参数，即当前项的索引。例：

~~~html
<ul>
    <li v-for="(item,index) in array" >
        array[{{index}}] = {{item}}   
    </li>
</ul>
~~~

运行结果:

![Image-text](./assets/img/readme/v-for2.png)

`v-for`遍历对象的属性

~~~html
<body>
<h1>v-for</h1>
<hr>
<div id="app">
    <ul>
        <li v-for="value in map" >
            value
        </li>
    </ul>
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data :{
            map: {
                no:20,
                name:'小明',
                gender:'男'
            }
        }
    })
</script>
</body>
~~~

运行结果:

![Image-text](./assets/img/readme/v-for3.png)

正如上面所说v-for还支持第二个参数(property名称 即键名)

~~~html
<ul>
    <li v-for="(value,key) of map" >
        {{key}} : {{value}}
    </li>
</ul>
~~~

运行结果:

![Image-text](./assets/img/readme/v-for4.png)

~~~html
<body>
<h1>v-for</h1>
<hr>
<div id="app">
    <ul>
        <li v-for="student in students" >
            {{student.name}}
        </li>
    </ul>
</div>
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data :{
            students:[{
                name:'小明',
                age:12,
                sex:'男'
            },{
                name:'小红',
                age:13,
                sex:'女'
            },{
                name:'小蓝',
                age:14,
                sex:'男'
            }],
        }
    })
</script>
</body>
~~~

运行结果：

![Image-text](./assets/img/readme/v-for5.png)

**Vue官方文档写明： 你也可以用 `of` 替代 `in` 作为分隔符，因为它更接近 JavaScript 迭代器的语法：** 

`item in items`也可以写成`item of items`

[Vue官方文档: 列表渲染](https://cn.vuejs.org/v2/guide/list.html )

## v-text&v-html

### v-text

v-text :  更新元素的 `textContent`。如果要更新部分的 `textContent` ，需要使用 `{{ Mustache }}`(插值表达式) 插值。 

```html
<span>{{ message }}</span>
<!--上面和下面效果是一样的-->
<span v-text="message"></span>
```

但两者之间又有着部分差异

若vue对象创建出错，或者由于网络过慢，下面的script还没加载出来

{{ message }}是会直接显示成 {{ message }}  而不是 hello Vue而

**<span v-text="message"></span>** 则不会显示出来，而是等vue对象加载出来才显示

[Vue官方文档 : v-text](https://cn.vuejs.org/v2/api/#v-text)

### v-html

v-html :  更新元素的 `innerHTML` 。**注意：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译** 。如果试图使用 `v-html` 组合模板，可以重新考虑是否通过使用组件来替代。 

~~~html
<body>
    <h1>v-text & v-html 案例</h1>
    <hr>
    <div id="app">
        <span v-html="vHtml"></span>
    </div>

    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data: {
                vHtml: '<h2>hello Vue!</h2>'
            }
        })
    </script>
</body>
~~~

![Image-text](./assets/img/readme/v-html.png)

[Vue官方文档 : v-html](https://cn.vuejs.org/v2/api/#v-html )

[HTML](https://cn.vuejs.org/v2/guide/syntax.html#原始-HTML)

## v-on

 v-on : 绑定事件监听器。  事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略。 

 用在普通元素上时，只能监听[**原生 DOM 事件**](https://developer.mozilla.org/zh-CN/docs/Web/Events)。用在自定义元素组件上时，也可以监听子组件触发的**自定义事件**。 

```html
<body>
    <h1>v-on</h1>
    <hr>
    <div id="app">
        <button v-on:click="test">测试</button>
    </div>

    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data: {
                vHtml: '<h2>hello Vue!</h2>'
            },
            methods:{
                test:function () {
                    alert("v-on能监听到click事件");
                }
            }
        })
    </script>
</body>
```

![Image-text](./assets/img/readme/v-on.png)

![Image-text](./assets/img/readme/v-on1.png)

v-on能缩写成@

```html
<button v-on:click="test">测试</button>
<!--与下面相同-->
<button @click="test">测试</button>
```

- 修饰符

  -  `.stop` - 调用 `event.stopPropagation()`。 
  -  `.prevent` - 调用 `event.preventDefault()`。 
  - `.capture` - 添加事件侦听器时使用 capture 模式。
  - `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
  - `.{keyCode | keyAlias}` - 只当事件是从特定键触发时才触发回调。
  - `.native` - 监听组件根元素的原生事件。
  - `.once` - 只触发一次回调。
  - `.left` - (2.2.0) 只当点击鼠标左键时触发。
  - `.right` - (2.2.0) 只当点击鼠标右键时触发。
  - `.middle` - (2.2.0) 只当点击鼠标中键时触发。
  - `.passive` - (2.3.0) 以 `{ passive: true }` 模式添加侦听器

  更多样例可前去Vue官网观看

  [Vue官方文档 : v-on](https://cn.vuejs.org/v2/api/#v-on )

## v-model

v-model :  在表单控件`<input>` 、`<textarea>`及`<select>`或者组件上创建双向绑定。细节请看下面的教程链接。 

```html
<body>
    <h1>v-model</h1>
    <hr>
    <div id="app">
        <p>message = {{message}}</p>
        <h3>文本框</h3>
        <p>v-model:<input type="text" v-model="message"></p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data: {
                message:'hello Vue!'
            }
        })
    </script>
</body>
```

![image-20191207145134968](./assets/img/readme/v-model.png)

![image-20191207145226852](./assets/img/readme/v-model1.png)

- 修饰符
  - [`.lazy`](https://cn.vuejs.org/v2/guide/forms.html#lazy) - 取代 `input` 监听 `change` 事件
  - [`.number`](https://cn.vuejs.org/v2/guide/forms.html#number) - 输入字符串转为有效的数字
  - [`.trim`](https://cn.vuejs.org/v2/guide/forms.html#trim) - 输入首尾空格过滤

```html
<body>
    <h1>v-model 双向数据绑定</h1>
    <hr>
    <div id="app">
        <p>message = {{message}}</p>
        <h3>文本框</h3>
        <p>v-model:<input type="text" v-model="message"></p>
        <p>v-model.lazy:<input type="text" v-model.lazy="message"></p><!--延迟加载-->
        <p>v-model.number:<input type="text" v-model.number="message"></p><!--只显示数字   若最开始就输入其他文本 则就没用了 仍会显示其他文本-->
        <p>v-model.trim=<input type="text" v-model.trim="message"></p><!--去除前后空格-->
        <hr>

        <h3>文本域</h3>
        <textarea cols="20" rows="20" v-model="message"></textarea>
        <hr>

        <h3>多选框绑定一个值</h3>
        <input type="checkbox" id="isSelected" v-model="isSelected">
        <label for="isSelected">{{isSelected}}</label>
        <hr>

        <h3>多选框绑定数组</h3>
        <input type="checkbox" id="red" value="小红" v-model="student_names">
        <label for="isSelected">小红</label>
        <input type="checkbox" id="yellow" value="小黄" v-model="student_names">
        <label for="isSelected">小黄</label>
        <input type="checkbox" id="blue" value="小蓝" v-model="student_names">
        <label for="isSelected">小蓝</label>
        <p>
            {{student_names}}
        </p>
        <hr>

        <h3>单选框绑定</h3>
        <p>
            <input type="radio" id="one" value="男" v-model="gender">
            <label for="one">男</label>
            <input type="radio" id="two" value="女" v-model="gender">
            <label for="two">女</label>
            <p>选择的性别为:{{gender}}</p>
        </p>
    </div>

    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!',
                isSelected:true,
                student_names:[],
                gender:''
            }
        })
    </script>
</body>
```

[Vue官方文档 v-model](https://cn.vuejs.org/v2/api/#v-model )

[Vue官方文档 表单输入绑定](https://cn.vuejs.org/v2/guide/forms.html )

[Vue官方文档 将原生事件绑定到组件](https://cn.vuejs.org/v2/guide/forms.html )(可以等看完组件后再看)

## v-bind

v-bind : 可用于绑定标签的属性

- 修饰符
  - `.prop` - 被用于绑定 DOM 属性 (property)。([差别在哪里？](https://stackoverflow.com/questions/6003819/properties-and-attributes-in-html#answer-6004028))
  - `.camel` - (2.1.0+) 将 kebab-case 特性名转换为 camelCase. (从 2.1.0 开始支持)
  - `.sync` (2.3.0+) 语法糖，会扩展成一个更新父组件绑定值的 `v-on` 侦听器。

v-bind 的缩写为:

例如绑定img的src      a标签的href

```html
<body>
<h1>v-bind 实例</h1>
<hr>
<div id="app">
    <img v-bind:src="imgUrl">
    <!--v-bind 缩写 :-->
    <hr>
    <a :href="url" target="_blank">跳转</a>
</div>

<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            imgUrl:"https://www.baidu.com/img/bd_logo1.png?where=super",
            url:"https://www.baidu.com" 
        }
    })
</script>
</body>
```

![Image-text](./assets/img/readme/v-bind.png)

还有可以class和style

~~~html
<body>
<h1>v-bind 实例</h1>
<hr>
<div id="app">
    <div :class="className">1.绑定class</div>
    <hr>
    <div :class="{classA:isOk}">2.绑定class中的判断</div>
    <hr>
    <div :class="[classA,classB]">3、绑定class中的数组</div>
    <hr>
    <div :class="isOk?classA:classB">4、绑定class中的三元表达式判断</div>
    <hr>
    <div>
        <input type="checkbox" id="isOk" v-model="isOk">
        <label for="isOk" >isOk = {{isOk}}</label>
    </div>
    <hr>
    <div :style="{color:red,fontSize:font}">5、绑定style</div>
    <hr>
    <div :style="styleObject">6、用对象绑定style样式</div>
</div>

<style>
    .classA{
        color: red;
    }
    .classB{
        font-size: 150%;
    }
</style>

<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            className:"classA",
            isOk:false,
            classA:"classA",
            classB:"classB",
            red:"red",
            font:"20px",
            styleObject:{
                fontSize:'24px',<!--font-size在vue中要变成fontSize的写法-->
                color:'green'
            }
        }
    })
</script>
</body>
~~~

![Image-text](./assets/img/readme/v-bind1.png)

[Vue官方文档 : v-bind](https://cn.vuejs.org/v2/api/#v-bind  )

[Vue官方文档 : Class 与 Style 绑定](https://cn.vuejs.org/v2/guide/class-and-style.html)

## v-pre

v-pre 

- **不需要表达式**

- **用法**：跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

```html
<span v-pre>{{ this will not be compiled }}</span>
```

显示结果将会是      {{ this will not be compiled }} 

[Vue官方文档 : v-pre](https://cn.vuejs.org/v2/api/#v-pre )

## v-cloak

- **不需要表达式**
- **用法**：这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 `[v-cloak] { display: none }` 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。

~~~html
<div v-cloak>渲染完成后 才显示</div>
~~~

只有让Vue渲染完成后才会显示该元素

[Vue官方文档 : v-cloak](https://cn.vuejs.org/v2/api/#v-cloak)

## v-once

- **不需要表达式**
- **详细**：只渲染元素和组件**一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。

```html
<body>
<h1>v-pre & v-cloak & v-once 实例</h1>
<hr>
    <div id="app">
        <div v-once>{{message}}</div><!--只进行一次渲染-->
        <div><input type="text" v-model="message"></div>
        <div >{{message}}</div>
    </div>

    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            }
        })
    </script>
</body>
```

![Image-text](./assets/img/readme/v-once.png)

![Image-text](./assets/img/readme/v-once1.png)

# Vue的全局API

全局API是什么？

​	 全局API并不在构造器里，而是先声明全局变量或者直接在Vue上定义一些新功能，Vue内置了一些全局API，比如我们今天要学习的指令Vue.directive。说的简单些就是，在构造器外部用Vue提供给我们的API函数来定义新的功能。 

## Vue.directive 自定义指令

定义一个全局的指令。使用Vue.directive();

~~~javascript
Vue.directive('cr',function (el,binding,vnode) {
    	el.style='color:'+binding.value;
});
~~~

```html
<body>
<h1>vue.directive 自定义指令 实例</h1>
<hr>
<div id="app">
    <div v-cr="color">{{n}}</div><!--自定义指令-->
</div>

<script type="text/javascript">
    Vue.directive('cr',function (el,binding,vnode) {
            el.style='color:'+binding.value;
        }
    );
    var app=new Vue({
        el:'#app',
        data:{
            n:15,
            color:'red'
        }
    })
</script>
</body>
```

效果如图

![image-text](./assets/img/readme/Vue.directive1.png)

自定义指令中传递的三个参数

- el: 指令所绑定的元素，可以用来直接操作DOM。
- binding: 一个对象，包含指令的很多信息。
- vnode: Vue编译生成的虚拟节点。

自定义指令有五个生命周期（也叫钩子函数），分别是 bind,inserted,update,componentUpdated,unbind

```html
<body>
<h1>vue.directive 自定义指令 实例</h1>
<hr>
<div id="app">
    <div v-aa="color">{{n}}</div><!--自定义指令-->
    <div><button @click="add">add</button></div>
    <div><button onclick="unbind()">解绑</button></div>
</div>

<script type="text/javascript">
    Vue.directive('aa',{
            bind:function(){//被绑定
                console.log('1 - bind');
            },
            inserted:function(){//绑定到节点
                console.log('2 - inserted');
            },
            update:function(){//组件更新
                console.log('3 - update');
            },
            componentUpdated:function(){//组件更新完成
                console.log('4 - componentUpdated');
            },
            unbind:function(){//解绑
                console.log('5 - unbind');
            }
        }
    );
    function unbind() {
        app.$destroy();
    }
    var app=new Vue({
        el:'#app',
        data:{
            n:15,
            color:'red'
        },
        methods:{
            add:function () {
                this.n++;
            }
        }
    })
</script>
</body>
```

刚打开页面时

![image-text](./assets/img/readme/Vue.directive2.png)

控制台显示

![image-text](./assets/img/readme/Vue.directive3.png)

点击几次add按钮后

![image-text](./assets/img/readme/Vue.directive4.png)



点击解绑后

![image-text](./assets/img/readme/Vue.directive5.png)且再点击add按钮已经没有任何变化

### 钩子函数

 	一个指令定义对象可以提供如下几个钩子函数 (均为可选)： 

- `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

我们会在[稍后](https://cn.vuejs.org/v2/guide/render-function.html#虚拟-DOM)讨论[渲染函数](https://cn.vuejs.org/v2/guide/render-function.html)时介绍更多 VNodes 的细节。

- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。
- `unbind`：只调用一次，指令与元素解绑时调用。

### 钩子函数参数

 指令钩子函数会被传入以下参数： 

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。
- `binding`：一个对象，包含以下属性：
  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。
- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-接口) 来了解更多详情。
- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

**除了 `el` 之外，其它参数都应该是只读的，切勿进行修改。如果需要在钩子之间共享数据，建议通过元素的 [`dataset`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/dataset) 来进行。**

[Vue官方文档 : Vue.directive](https://cn.vuejs.org/v2/api/#Vue-directive )

[自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html )

## Vue.extend

- **参数**：
  
- `{Object} options`
  
- **用法**：

  使用基础 Vue 构造器，创建一个“子类”。参数是一个包含组件选项的对象。

  **`data` 选项是特例，需要注意 - 在 `Vue.extend()` 中它必须是函数**

```html
<body>
<h1>Vue.extend 扩展实例构造器</h1>
<hr>

<baidu></baidu>
<div id="baidu"></div>

<script type="text/javascript">
    var obj = Vue.extend({
        template:"<p><a :href='url'>{{message}}</a></p>",
        //这里的data不像在构造器里写data直接写   而是要写个匿名方法 return一个对象
        data:function () {
            return{
                message:'百度',
                url:'https://www.baidu.com'
            }
        }
    });

    //所有的扩展实例构造器都需要另一个操作 绑定(加载)到上面才可以用
    //Vue的$mount()为手动挂载
    //可以像jquery一样绑定
    new obj().$mount('baidu');//根据标签绑定
    new obj().$mount('#baidu');//根据id绑定
</script>
</body>
```

![image-text](./assets/img/readme/Vue.extend.png)

[Vue官方文档 : Vue.extend](https://cn.vuejs.org/v2/api/#Vue-extend )

## Vue.set

### 引用构造器外部数据

```javascript
<script type="text/javascript">
    var outDate = {
        count : 1
    } ;
    var app=new Vue({
        el:'#app',
        data : outDate
    })
</script>
```

```html
<div id="app">
    {{count}}
</div>
```

在页面上count能够显示出来

![image-text](./assets/img/readme/v-set1.png)

### 在作用域外部改变数据的三种方法

~~~javascript
function add() {
	Vue.set(outData,'count',3);
}
~~~

~~~javascript
function add() {
	app.count++;
}
~~~

~~~javascript
function add() {
    outData.count++;
}
~~~

### 为什么需要Vue.set

由于JavaScript的限制，Vue中不能检测到数组和对象的两种变化：

- 数组长度的变化 vm.arr.length = 4
- 数组通过索引值修改内容 vm.arr[1] = 'aa' 

由于检测不到所以Vue不会为我们自动更新

例

~~~html
<body>
    <h1>vue.set 全局操作</h1>
    <hr>
    <div id="app">
        <ul>
            <li v-for="item in arr">
                {{item}}
            </li>
        </ul>
    </div>
    <button onclick="add()">add</button>
    <script type="text/javascript">

        var outData = {
            arr:['111','222','333']
        } ;
        var app=new Vue({
            el:'#app',
            data : outData
        })
        function add() {
            console.log("已经执行了add方法");
            outData.arr[1] = '555';
            console.log("arr[1] = " + app.arr[1]);
        }
    </script>
</body>
~~~

![image-20191208104916163](./assets/img/readme/v-set2.png)

所以需要用Vue.set(app.arr,1,'555')设置改变，Vue才会重新渲染。

[Vue官方文档Vue.set](https://cn.vuejs.org/v2/api/#Vue-set )



## Vue的生命周期

Vue一共有十个生命周期函数，我们可以利用这些函数在Vue的每个阶段都进行操作数据或修改内容。

![lifecycle](./assets/img/readme/lifecycle.png)

Vue官网这张图已经很好的诠释了生命周期。可以看下面的程序再理解下

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>构造器的声明周期</title>
</head>
<body>
    <h1>构造器的声明周期</h1>
    <hr>
    <div id="app">
        {{n}}
        <p>
            <button @click="add">add</button>
        </p>
    </div>
    <button onclick="app.$destroy()">destroy</button>

    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data: {
                n: 1
            },
            methods: {
                add: function () {
                    this.n++;
                }
            },
            beforeCreate: function () {
                console.log('1-beforeCreate 初始化之后');
            },
            created: function () {
                console.log('2-created 创建完成');
            },
            beforeMount: function () {
                console.log('3-beforeMount 挂载之前');
            },
            mounted: function () {
                console.log('4-mounted 挂载之后');
            },
            beforeUpdate: function () {
                console.log('5-beforeUpdate 数据更新前');
            },
            updated: function () {
                console.log('6-updated 被更新后');
            },
            activated: function () {
                console.log('7-activated');
            },
            deactivated: function () {
                console.log('8-deactivated');
            },
            beforeDestroy: function () {
                console.log('9-beforeDestroy 销毁之前');
            },
            destroyed: function () {
                console.log('10-destroyed 销毁之后')
            }

        })
    </script>
</body>
</html>
~~~

这是点击两次add后，点击一次destroy的结果

![](./assets/img/readme/生命周期.png)

~~~javascript
<script type="text/javascript">
    var app = new Vue({
        el: '#app',
        data: {
            msg: 'OK'
        },
        methods: {
            add: function () {
                console.log("执行了add方法");
            }
        },
        beforeCreate: function () {
            /*
                这是第一个生命周期函数，表示在Vue实例完全创建出来之前会执行它
                在执行beforeCreate时，data和methods中的数据都还没有被初始化
            */
            console.log(this.msg); // undefined
        },
        created: function () {
            /*
                第二个生命周期函数，在created中，data和methods都已经初始化好了
                如果要调用methods中的方法或data内的数据，最早只能在created中操作
            */
            console.log(this.msg); // OK
            this.add(); //执行了add方法
        },
        beforeMount: function () {
            /*
                这是第三个生命周期函数， beforeMount 挂载之前，此时模板已经在内存中编辑完成了，但尚未把模板渲染到页面中
                也就是在 beforeMount 执行的时候，页面中的元素还没有真正替换过来，只是之前写的模板字符串，即插值表达式
            */
            console.log(document.getElementById('dataId').innerText); //{{msg}}
        },
        mounted: function () {
            /*
                这是第四个生命周期函数，mounted，表示内存中的模板已经真实的挂载到页面中了，用户可以看到渲染好的页面
                注意：mounted是实例创建期间的最后一个生命周期函数，当执行完mounted后，表示实例别完全创建好了
                如果要操作元素的DOM操作，最早在mounted中操作
            */
            console.log(document.getElementById('dataId').innerText); // OK
        },
        beforeUpdate: function () {
            /*
                表示 我们的界面显示还没有更新，但是数据已经更新了
                也就是执行beforeUpdate时，页面中显示的数据还是旧的，但data中的数据已经更新了
            */
            console.log("页面中的值：" + document.getElementById("dataId").innerText);   //OK
            console.log("data中msg的值" + this.msg);   //No
        },
        updated: function () {
            /*
                执行时，页面中的数据与data中的数据已经同步了
            */
            console.log("页面中的值：" + document.getElementById("dataId").innerText);   //No
            console.log("data中msg的值" + this.msg);   //No
        },
        activated: function () {
            console.log('7-activated');
        },
        deactivated: function () {
            console.log('8-deactivated');
        },
        beforeDestroy: function () {
            /*
                执行该函数时，Vue实例已经从执行阶段进入了销毁阶段，
                但是实例上所有的data和methods、过滤器、指令都还可用，此时还没有真正的销毁
            */
        },
        destroyed: function () {
            /*
                当执行了该函数时，组件已经完全被销毁，组件中所有的数据、方法、指令、过滤器都已经不可用了
            */
        }

    })
</script>
~~~

[Vue官方文档-实例生命周期钩子](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期钩子) 

[Vue官方文档-生命周期图示](https://cn.vuejs.org/v2/guide/instance.html#生命周期图示)

## Template制作模板

### 写在选项里的template

在构造器中template选项后面直接编写。但要用反引号`包裹

~~~javascript
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        },
        template: `
			<h1 style="color: red">这是选项中的模板</h1>
        `
    })
</script>
~~~

### template标签中的模板

~~~html
<template id="demo">
	<h1 style="color: red">这是Template标签模板</h1>
</template>
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        },
        template:"#demo"
    })
</script>
~~~

### 在script标签里的模板

 这种写模板的方法，可以让模板文件从外部引入。 

~~~javascript
<script type="x-template" id="demo">
    <h2 style="color: red">Script标签模板</h2>
</script>
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        },
        template:"#demo"
    })
</script>
~~~

在vue-cli的时候还会学到一种xxx.vue的写法。 

[Vue官方文档-template]( https://cn.vuejs.org/v2/api/#template )

## component组件

简单来说，组件就是自定义的标签，即在HYML中没有的标签。

[Vue官方文档-组件注册](https://cn.vuejs.org/v2/guide/components-registration.html )

### 全局组件

全局组件是在构造器外部通过Vue.component注册的.

这是完整代码

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>component-1</title>
</head>
<body>
    <h1>component-1</h1>
    <hr>
    <div id="app">
        这是id为app的
        <cr></cr>
    </div>
    <hr>
    <div id="xxx">
        这是id为xxx的
        <cr></cr>
    </div>
    <hr>
    这是不在vue作用域内的
    <cr></cr>
    <script type="text/javascript">
        Vue.component("cr", {
            template: `<div style="color: red"><h1>这是全局组件</h1></div>`
        });
        var app = new Vue({
            el: '#app'
        });
        var vm = new Vue({
            el: '#xxx'
        });
    </script>
</body>
</html>
~~~

![image-20191219094803960](.\assets\img\readme\component-1.png)

组件就是可以将自定义标签替换成模板。

[全局注册](https://cn.vuejs.org/v2/guide/components-registration.html#全局注册)

### 局部组件

既然有全局组件，那么就有局部组件。

~~~html
<body>
    <h1>component-1</h1>
    <hr>
    <div id="app">
        这是id为app的
        <cr></cr>
        <abc></abc>
    </div>
    <script type="text/javascript">
        Vue.component("cr", {
            template: `<div style="color: red"><h1>这是全局组件</h1></div>`
        });
        var app = new Vue({
            el: '#app',
            components:{
                "abc":{
                    template: `<div style="color: green"><h2>这是局部组件</h2></div>`
                }
            }
        });
    </script>
</body>
~~~

![image-text](.\assets\img\readme\局部组件.png)

局部组件可以直接在components里写多个。

全局组件则要Vue.component一个一个写。

局部组件只能在当前Vue对象作用域作用。

[局部注册](https://cn.vuejs.org/v2/guide/components-registration.html#局部注册)

### props属性设置

 组件接受的选项之一 props 是 Vue 中非常重要的一个选项。 

利用props，可以取到自定义标签中设置的属性。

案例：

~~~html
<body>
    <h1>component-2</h1>
    <hr>
    <div id="app">
        <abc myname="123"></abc>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            components:{
                "abc":{
                    template: `<div style="color: green"><h2>myname is {{myname}}</h2></div>`,
                    props:['myname']
                }
            }
        });
    </script>
</body>
~~~

结果：

![image-20191219133403043](.\assets\img\readme\props.png)

props可以接受的是一个数组，因为可以有多个属性。只有在props里面写了这个属性，才能在模板里用。

如果属性名是带-的写法，例如my-name 是不行的，Vue不支持这种写法。

即如果属性名是my-name，那么在Vue中则要采取大驼峰的写法(MyName)或小驼峰的写法(myName)

~~~html
<body>
    <h1>component-2</h1>
    <hr>
    <div id="app">
        <abc my-name="123"></abc>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            components:{
                "abc":{
                    template: `<div style="color: green"><h2>myname is {{myName}}</h2></div>`,
                    props:['myName']
                }
            }
        });
    </script>
</body>
~~~

my-name="123"my设置除了直接赋值，还可以用v-bind:my-name="mydata"来赋值。mydata就是在vue里定义好的data。

~~~html
<body>
    <h1>component-2</h1>
    <hr>
    <div id="app">
        <abc :my-name="vuedata"></abc>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data:{
                vuedata:"333"
            },
            components:{
                "abc":{
                    template: `<div style="color: green"><h2>myname is {{myName}}</h2></div>`,
                    props:['myName']
                }
            }
        });
    </script>
</body>
~~~

[Vue官方文档-prop](https://cn.vuejs.org/v2/guide/components-props.html)

### 父子组件

- 在构造器外部写局部注册组件 

如果组件的代码量很大，那么组件直接写在构造器里，就很影响构造器的可读性。

组件的代码可以写在构造器外部或者在一个单独的文件里。

例：

~~~html
<body>
    <div id="app">
        <abc></abc>
    </div>
    <script type="text/javascript">
        var abc = {
            template:`<div style="color: aqua"><h1>这是在构造器外部写的组件</h1></div>`
        }
        var app = new Vue({
            el:'#app',
            components:{
                'abc':abc
            }
        });
    </script>
</body>
~~~

- 父子组件的嵌套

如果在父组件中想要用子组件，那么必须在父组件中注册子组件。

~~~html
<body>
    <div id="app">
        <father></father>
    </div>
    <script type="text/javascript">
        var son = {
            template:`
                <div style="color: red">
                    <h1>子组件</h1>
                </div>
            `
        }
        var father = {
            template:`
                <div style="color: aqua">
                    <h1>父组件</h1>
                    <son></son>
                </div>
            `,
            components: {
                "son":son
            }
        }

        var app = new Vue({
            el:'#app',
            components:{
                'father':father,
            }
        });
    </script>
</body>
~~~

### Component标签

component标签是Vue定义的标签。作用是可以动态的使用任何已经注册了的组件。

~~~html
<body>
    <div id="app">
        <component is="componentA"></component>
    </div>
    <script type="text/javascript">
        var componentA = {
            template :`<div style="color:red;"><h1>这是componentA</h1></div>`
        }
        var componentB = {
            template :`<div style="color:green;"><h1>这是componentB</h1></div>`
        }
        var app = new Vue({
            el:'#app',
            components:{
                'componentA':componentA,
                'componentB':componentB
            }
        })
    </script>
</body>
~~~

通过和Vue的普通指令结合，就能够动态更换已经注册的组件了。

[动态组件](https://cn.vuejs.org/v2/guide/components.html#动态组件)

## 构造器选项

### porpsData

porpsData用在全局扩展时进行传递数据。但在实际中，并不经常用全局扩展的方式作自定义标签。这里只是为了演示propsData。

[全局扩展的知识](##Vue.extend)



 我们要在挂载时传递一个数字过去，我们就用到了propsData。 

我们用propsData三步解决传值：

1. 在全局扩展里加入props进行接收。propsData:{a:1}

2. 传递时用propsData进行传递。props:[‘a’]

3. 用插值的形式写入模板。{{ a }} 

   完整代码： 

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>propsData</title>
</head>
<body>

    <h1>propsData</h1>
    <hr>
    <baidu></baidu>

    <script type="text/javascript">
        var obj = Vue.extend({
            template:"<p><a :href='url'>{{a}}{{message}}</a></p>",
            data:function () {
                return{
                    message:'百度',
                    url:'https://www.baidu.com'
                }
            },
            props:['a']
        });

        //propsData是用来传值的
        //用propsData传递时要用props进行接受
        //用插值的形式写入模板
        new obj({propsData:{a:"这是一个"}}).$mount('baidu');//根据标签绑定
    </script>
</body>
</html>
~~~

[Vue官方文档-propsData](https://cn.vuejs.org/v2/api/#propsData )

### computed

模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。 

computed的作用是对原数据进行改造输出。 所以，对于任何复杂逻辑，你都应当使用**计算属性**。 

例： 

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>computed</title>
</head>
<body>
    <h1>propsData</h1>
    <!--computed 的作用主要是对原数据进行改造输出。改造输出：包括格式的编辑，大小写转换，顺序重排，添加符号……。-->
    <hr>
    <div id="app">
        price = {{price}}<br>
        newPrice = {{newPrice}}
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el:'#app',
            data:{
                price:1000
            },
            computed:{
                newPrice:function () {
                    return '￥' + this.price + '元';
                }
            }
        });
    </script>
</body>
</html>
~~~

或者

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>computed</title>
</head>
<body>
    <h1>propsData</h1>
    <hr>
    <div id="app">
        <div>newsList</div>
        <ol>
            <li v-for="item of newsList">{{item.title}}</li>
        </ol>

        <div>reverseNews</div>
        <ol>
            <li v-for="item of reverseNews">{{item.title}}</li>
        </ol>
    </div>
    <script type="text/javascript">
        var newsList = [
            {title:'一箭九星 中国成功发射中巴地球资源卫星04A星等9颗卫星',date:'2019/12/19'},
            {title:'法工委发言人：有意见建议“同性婚姻合法化”写入民法典',date:'2019/12/20'},
            {title:'二手房业主“抱团”抬价 多个楼盘猛涨几十万 官方出手',date:'2019/12/21'}
        ];
        var app = new Vue({
            el:'#app',
            data:{
                price:1000,
                newsList:newsList
            },
            computed:{
                newPrice:function () {
                    return '￥' + this.price + '元';
                },
                reverseNews:function () {
                    return this.newsList.reverse();
                }
            }
        });
    </script>
</body>
</html>
~~~

出现的效果是

![image-20191220153959209](.\assets\img\readme\computed.png)

原来的newsList应该为

![image-20191220154107384](C:\Users\Lemon\WebstormProjects\Vue\assets\img\readme\computed1.png)

之所以会出现上面的情况是因为javascript的reverse()方法会改变原数组

[Vue官方文档-computed](https://cn.vuejs.org/v2/guide/computed.html )

[Vue官方文档- 计算属性](https://cn.vuejs.org/v2/guide/computed.html#计算属性)

### methods

在之前，就已经使用过了构造器中的methods选项了。

下面将介绍下这个选项涉及到的东西。

- 一般正常调用是这样的

~~~html
<button v-on:click="m1('正常')">btn1</button><br>
~~~

- 在实际开发中经常需要把某个按钮封装成组件，然后反复使用，如何让组件调用构造器里的方法，而不是组件里的方法。 则需要记得加.native 修饰器 

~~~html
<abc @click.native="m1('组件')"></abc><br>
~~~

- 如果是在Vue的外部调用

~~~html
<button onclick="app.m1('外部')">btn3</button>
~~~

完整代码

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../assets/js/vue.js"></script>
    <title>methods</title>
</head>
<body>
    <h1>methods</h1>
    <hr>
    <div id="app">
        <div>{{message}}</div>
        <button v-on:click="m1('正常')">btn1</button><br>
        <abc @click.native="m1('组件')"></abc><br>
    </div>
    <button onclick="app.m1('外部')">btn3</button>
    <script type="text/javascript">
        var abc = {
            template : `<button>btn2</button>`
        }
        var app = new Vue({
            el:'#app',
            data:{
                message:'',
            },
            methods:{
                m1:function (msg) {
                    this.message = '这是' + msg + '调用方法'
                }
            },
            components:{
                'abc':abc
            }
        });
    </script>
</body>
</html>
~~~

- methods中的$event参数

 传递的$event参数都是关于你点击鼠标的一些事件和属性。 

~~~html
<button v-on:click="m1('正常',$event)">btn1</button>
~~~

只需要这样就可以将event对象传递进去。

~~~javascript
methods:{
                m1:function (msg,event) {
                    this.message = '这是' + msg + '调用方法';
                    console.log(event);
                }
            },
~~~

 [Vue官方文档-methods](https://cn.vuejs.org/v2/api/#methods)

### watch

**watch，它可以用来监测Vue实例上的数据变动。**

如果对应一个对象，键是观察表达式，值是对应回调，值也可以是方法名，或者是对象，包含选项。

案例：当num为50时输出`num ========== 50`，小于时则输出`num <<<<<<<<<< 50`，大于时则输出`num >>>>>>>>>> 50`

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>watch</title>
</head>
<body>
    <div id="app">
        <div>{{message}}</div>
        <button @click="addnum">add</button>
        <button @click="subnum">sub</button>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el:'#app',
            data:{
                num:50,
                message:'num ========== 50'
            },
            methods:{
                addnum:function () {
                    this.num++;
                },
                subnum:function () {
                    this.num--;
                }
            },
            watch:{
                num:function (newVal,oldVal) {
                    if (newVal == 50){
                        this.message = 'num ========== 50';
                    }else if(newVal > 50){
                        this.message = 'num >>>>>>>>>> 50';
                    }else{
                        this.message = 'num <<<<<<<<<< 50';
                    }
                }
            }
        })
    </script>
</body>
</html>
~~~

~~~javascript
function (newVal,oldVal)
~~~

方法中的参数，则可以取到这个值的新值(newVal)和旧值(oldVal)。

还可以用实例属性写watch监控

~~~javascript
app.$watch('xxx',function(){})
~~~

~~~javascript
app.$watch('num',function (newVal,oldVal) {
	if (newVal == 50){
		this.message = 'num ========== 50';
	}else if(newVal > 50){
		this.message = 'num >>>>>>>>>> 50';
	}else{
		this.message = 'num <<<<<<<<<< 50';
	}
})
~~~

[Vue官方文档-watch](https://cn.vuejs.org/v2/api/#watch)

### mixins

minxins一般有两种用途:

1. 在你写好构造器后，需要增加方法，这时用混入会减少对源代码的污染。
2. 很多地方都会用到的公用方法，用混入的方法可以减少代码
   量，实现代码复用。

混入可以接受的是一个数组。

案例：

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>mixins</title>
</head>
<body>
    <div id="app">
        <div>{{num}}</div>
        <button @click="add">add</button>
    </div>
    <script type="text/javascript">
        var addConsole = {
            updated:function () {
                console.log("num数据发生变化，变成了"+this.num);
            }//这个updated是生命周期的updated   而不是mixins特有
        }
        var app = new Vue({
            el:'#app',
            data:{
                num:10
            },
            methods:{
                add:function () {
                    this.num++;
                }
            },
            mixins:[addConsole]
        })
    </script>
</body>
</html>
~~~



![image-20191220172104088](.\assets\img\readme\mixins.png)

- mixins的调用顺序

 从执行的先后顺序来说，都是混入的先执行，然后构造器里的再执行，需要注意的是，这并不是方法的覆盖，而是被执行了两边。 

如果构造器中增加了updated

~~~javascript
var app = new Vue({
    el:'#app',
    data:{
        num:10
    },
    updated:function(){
        console.log("数据更新了");
    },
    methods:{
        add:function () {
            this.num++;
        }
    },
    mixins:[addConsole]
})
~~~

![image-20191220172716847](.\assets\img\readme\mixins-1.png)

- 全局API混入

我们也可以定义全局的混入，这样在需要这段代码的地方直接引入js，就可以拥有这个功能了。 

 PS：全局混入的执行顺序要优先于混入和构造器里的方法。 

~~~html
<body>
    <div id="app">
        <div>{{num}}</div>
        <button @click="add">add</button>
    </div>
    <script type="text/javascript">

        var addConsole = {
            updated:function () {
                console.log("num数据发生变化，变成了"+this.num);
            }//这个updated是生命周期的updated   而不是mixins特有
        }
        Vue.mixin({
            updated:function () {
                console.log("这是全局混入");
            }
        })
        var app = new Vue({
            el:'#app',
            data:{
                num:10
            },
            updated:function(){
                console.log("数据更新了");
            },
            methods:{
                add:function () {
                    this.num++;
                }
            },
            mixins:[addConsole]
        })

    </script>
</body>
~~~



![image-20191220173120945](.\assets\img\readme\mixins-2.png)

如果mixins中和构造器有相同的方法，则会先执行构造器中的方法。

![image-text](.\assets\img\readme\mixins-3.png)

[Vue官方文档-mixins](https://cn.vuejs.org/v2/api/#mixins)

### extends

 允许声明扩展另一个组件(可以是一个简单的选项对象或构造函数)，而无需使用 `Vue.extend`。这主要是为了便于扩展单文件组件。 

和mixins类似

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>extends</title>
</head>
<body>
    <div id="app">
        <button @click="show">show</button>
    </div>
    <script type="text/javascript">
        var abc = {
            created:function () {
                console.log("这是扩展的create");
            },
            methods:{
                show:function () {
                    console.log("这是扩展的show方法");
                }
            },
        }
        var app = new Vue({
            el:'#app',
            created:function () {
                console.log("这是构造器的create");
            },
            methods:{
                show:function () {
                    console.log("这是原生的show方法");
                }
            },
            extends:abc
        });
    </script>
</body>
</html>
~~~



![image-20191220200227899](.\assets\img\readme\extends.png)

和mixins一样的是，若出现同名方法时，则会执行构造器中的方法。

不过extends只能接受一个对象，而mixins可以接受一个数组。

[Vue官方文档-extends](https://cn.vuejs.org/v2/api/#extends )

###  delimiters 

delimiters 的作用是 改变纯文本插入分隔符。 

即原来用{{message}}取值

可以通过delimiters 修改成${message}取值

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>delimiters</title>
</head>
<body>
    <h1>delimiters</h1>
    <hr>
    <div id="app">
        ${message}
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el:'#app',
            data:{
                message:"你不想努力了？"
            },
            delimiters:['${','}']
        });
    </script>
</body>
</html>
~~~

[Vue官方文档-delimiters](https://cn.vuejs.org/v2/api/#delimiters)

# 实例和内置组件

## Vue和jQuery一起使用

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/jquery-3.4.1.min.js"></script>
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>jQuery</title>
</head>
<body>
    <h1>Hello World</h1>
    <hr>
    <div id="app">
        {{message}}
    </div>

    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            },//只有在mounted和update里才能用jQuery进行工作
            //没挂载前是找不到dom的   所以没法使用
            mounted:function () {//在vue里用jQuery必须在挂载以后
                $('#app').html("jQuery!");
            }
        })
    </script>
</body>
</html>
~~~

## 构造器外部调用方法

~~~html
<script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            },
            methods:{
                show:function () {
                    console.log("调用了show方法");
                }
            }
        })
        app.show();
    </script>
~~~

 PS：我们有可能把`app.show()`的括号忘记或省略，这时候我们得到的就是方法的字符串，但是并没有执行，所以必须要加上括号。 

## 实例方法

### $mount

在[Vue.extend](##Vue.extend)中就已经出现过一次了。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>$mount</title>
</head>
<body>
<h1>$mount</h1>
<hr>
<div id="app">
    {{message}}
</div>

<script type="text/javascript">
    var abc = Vue.extend({
        template:`<h3><p>{{message}}</p></h3>`,
        data:function () {
            return {
                message:'hello abc'
            }
        }
    })
    var app = new abc().$mount('#app');
</script>
</body>
</html>
~~~

[Vue官方文档-$mount](https://cn.vuejs.org/v2/api/#vm-mount)

### $destroy

用$destroy销毁实例。 清理它与其它实例的连接，解绑它的全部指令及事件监听器。 

~~~html
<body>
    <h1>$destroy</h1>
    <hr>
    <div id="app">
        {{message}}
        <div><button @click="add">add</button></div>
        <div><button onclick="destroy()">destroy</button></div>
    </div>

    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            },
            methods:{
                add:function () {
                    this.message += "123"
                }
            }
        })
        function destroy() {
            app.$destroy();
        }
    </script>
</body>
~~~

[Vue官方文档-$destroy](https://cn.vuejs.org/v2/api/#vm-destroy)

### $forceUpdate

 迫使 Vue 实例重新渲染。注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件。 

~~~javascript
app.$forceUpdate()
~~~

[Vue官方文档-$forceUpdate](https://cn.vuejs.org/v2/api/#vm-forceUpdate)

### $nextTick 

当Vue构造器里的data值被修改完成后会调用这个方法，也相当于一个钩子函数吧，和构造器里的updated生命周期很像。 

~~~javascript
function tick(){
    vm.message="update message info ";
    vm.$nextTick(function(){
        console.log('message更新完后我被调用了');
    })
}
~~~

[Vue官方文档-$nextTick](https://cn.vuejs.org/v2/api/#vm-nextTick )

## 实例事件

实例事件就是在构造器外部写一个调用构造器内部的方法。这样写的好处是可以通过这种写法在构造器外部调用构造器内部的数据。

### $on

 **用法**：  监听当前实例上的自定义事件。事件可以由`vm.$emit`触发。回调函数会接收所有传入事件触发函数的额外参数。 

~~~javascript
app.$on('add',function () {
	this.message += "123"
})
~~~

要利用$emit来触发。 

~~~javascript
function add() {
	app.$emit('add')
}
~~~

 [Vue官方文档-$on](https://cn.vuejs.org/v2/api/#vm-on) 

###  $once 

**用法**：

监听一个自定义事件，但是只触发一次。一旦触发之后，监听器就会被移除。

~~~javascript
app.$once('addonce',function () {
    this.message += "addonce"
})
function addonce() {
    app.$emit('addonce')
}
~~~

 [Vue官方文档-$once](https://cn.vuejs.org/v2/api/#vm-once) 

###  $off 

**用法**：

移除自定义事件监听器。

- 如果没有提供参数，则移除所有的事件监听器；
- 如果只提供了事件，则移除该事件所有的监听器；
- 如果同时提供了事件与回调，则只移除这个回调的监听器。

~~~javascript
function off() {
    app.$off('add');
}
~~~

[Vue官方文档-$off](https://cn.vuejs.org/v2/api/#vm-off ) 

### $emit

[Vue官方文档-$emit](https://cn.vuejs.org/v2/api/#vm-emit)

## slot

###  匿名插槽

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>slot</title>
</head>
<body>
    <div id="app">
        <abc><p style="color: green">{{message}}</p></abc>
    </div>
    <template id="tmp">
        <div>
            <h1>
                <slot></slot>
            </h1>
        </div>
    </template>
    <script type="text/javascript">
        var abc = {
            template:'#tmp'
        }
        var app=new Vue({
            el:'#app',
            data:{
                message:'HelloVue'
            },
            components:{
                'abc':abc
            }
        })
    </script>
</body>
</html>
~~~

展示出的效果是

![image-20191222214205885](.\assets\img\readme\slot.png)

只用单个slot标签则会将abc标签中包裹的所有内容都插入。

### 具名插槽

现在Vue构造器里的data放了这些信息：

~~~javascript
data:{
    baidu:{
        netName:'百度',
        url:'https://www.baidu.com'
    }
},
~~~

 我们用`<template></template>`标签的方式定义了组件： 

~~~html
<template id="tmp">
    <div>
        <p>网站地址：</p>
        <p>网站名：</p>
    </div>
</template>
~~~

我们现在就可以用slot功能让组件接收传递过来的值，并在模板中接收显示。

slot的使用需要两步： 1、在HTML的组件中用slot属性传递值。

~~~html
<baidu>
    <span slot="netName">{{baidu.netName}}</span>
    <span slot="url">{{baidu.url}}</span>
</baidu>
~~~

 2、在组件模板中用标签接收值。 

~~~html
<template id="tmp">
    <div>
        <p>网站地址：<slot name="netName"></slot></p>
        <p>网站名：<slot name="url"></slot></p>
    </div>
</template>
~~~

完整代码

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../../assets/js/vue.js"></script>
    <title>slot</title>
</head>
<body>
    <div id="app">
        <baidu>
            <span slot="netName">{{baidu.netName}}</span>
            <span slot="url">{{baidu.url}}</span>
        </baidu>
    </div>
    <template id="tmp">
        <div>
            <p>网站地址：<slot name="netName"></slot></p>
            <p>网站名：<slot name="url"></slot></p>
        </div>
    </template>
    <script type="text/javascript">
        var abc = {
            template:'#tmp'
        }
        var app=new Vue({
            el:'#app',
            data:{
                baidu:{
                    netName:'百度',
                    url:'https://www.baidu.com'
                }
            },
            components:{
                'baidu':abc
            }
        })
    </script>
</body>
</html>
~~~

![image-20191222215448516](.\assets\img\readme\slot1.png)

[Vue官方文档-插槽](https://cn.vuejs.org/v2/guide/components-slots.html)

[Vue官方文档-slot](https://cn.vuejs.org/v2/api/#slot-废弃)

