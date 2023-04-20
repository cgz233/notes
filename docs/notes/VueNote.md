# uni-app Notes

# Vue

## Vue基础指令

**使用Vue：**

1. `<script src= "Vue.js" type= "text/javascript"></script>`
2. `<script src= "https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>`

3. 通过npm安装

**Vue实例：**

Vue.js应用的创建很简单，通过构造函数Vue就可以创建一个Vue的根实例，并启动Vue应用。创建Vue实例代码如下所示：

```javascript
var vm = new Vue({
    el:'#app',
    data:{
        name:'Hello Vue!'
    },
    methods:{

    }
})
```

- el：element 缩写 挂载，挂载域 可以理解实例关联到哪个元素上 或者说这个new的这个对象作用到哪个元素上

  \#app（选择器）作用到id是app的这个元素上，这样ViewModel层和View就产生了关联

- 数据（data）

  data选项可以声明应用内需要双向绑定的数据。通常所有应用中需要用到的数据都会在data内声明，避免数据散落在业务逻辑中，难以维护，真正实现数据和视图的分离

- 方法（methods）

  在方法属性/选项中，我们定义一些方法，在组件或模板中调用这些方法

**数据绑定：**

- 文本绑定：通过使用`{{}}`标签来绑定数据

  ```html
  <!DOCTYPE html>
  <html lang="zh">
  	<head>
  		<meta charset="UTF-8">
  		<script type="text/javascript" src="js/v2.6.10/vue.js" charset="utf-8"></script>
  		<title>Document</title>
  	</head>
  	<body>
  		<div id="app">
  			{{msg}}<br />
  			{{message}}
  		</div>
  		<script>
  			var vm = new Vue({
  				el: '#app',
  				data: {
  					//vue 中的model
  					message: '你好，世界!',
  					msg: 'hello world!'
  				},
  				methods: {
  
  				}
  			})
  		</script>
  	</body>
  </html>
  ```

**基本指令：**

- **v-text和v-html指令**

  - v-text主要用来更新textContent，将实例中的数据当成纯文本输出，可以等同于JavaScript的text属性
  - v-html会将实例中的数据当成HTML标签解析后输出，它等同于JavaScript的innerHtml属性

  实例：

  ```html
  <body>
      <div id="app">
          <p v-text="html"></p>
          <p v-html="html"></p>
      </div>
      <script>
          var vm = new Vue({
              el:'#app',
              data:{
                  html : '<input type="date" />'
              }
          })
      </script>
  </body>
  ```

  效果：

  <img src="https://image.cgz233.cn/images/202304091648961.png" alt="image-20230409164813848" style="zoom:50%;" /> 

- **v-if、v-else和v-show指令**

  - v-if可以实现条件渲染，Vue会根据表达式的值的真假条件来渲染元素

    `<a v-if="ok">yes</a>`如果属性值ok为true，则显示。否则，不会渲染这个元素

  - v-else是搭配v-if使用的，它必须紧跟在v-if或者v-else-if后面，否则不起作用

  - v-if指令用于条件性地渲染一块内容，这块内容只会在指令的表达式返回 true 值的时候被渲染。v-show不管条件是否成立，都会渲染html

    检查页面元素发现：v-if是注释，v-show是设置CSS样式display的值为none

  ```html
  <!DOCTYPE html>
  <html>
  	<head>
  		<meta charset="utf-8">
  		<title></title>
  		<script type="text/javascript" src="js/v2.6.10/vue.js"></script>
  	</head>
  	<body>
  		<div id="app">
  			<p v-if="status==1">当status为1显示该行</p>
  			<p v-else-if="status==2">当status为2显示该行</p>
  			<p v-else>当status不为1和2显示该行</p>
  			
  			<p v-show="status==2">v-show</p>
  		</div>
  		
  		<script type="text/javascript">
  			let vm = new Vue({
  				el:'#app',
  				data:{
  					status : 3
  				}
  			})
  		</script>
  	</body>
  </html>
  ```

- **v-on指令**

  - v-on指令是来绑定事件监听器的，类似原生JavaScript的onclick的用法
  - v-on:click可以简写成@click，以后都会使用这种简写方法

  ```
  • Vue支持以下修饰符
  • <!-- 阻止单击事件冒泡 -->
  • <a v-on:click.stop="doThis"></a>
  • <!-- 提交事件不再重载页面 -->
  • <form v-on:submit.prevent="onSubmit"></form>
  • <!-- 修饰符可以串联 -->
  • <a v-on:click.stop.prevent="doThat"></a>
  • <!-- 只有修饰符 -->
  • <form v-on:submit.prevent></form>
  • <!-- 添加事件侦听器时使用事件捕获模式 -->
  • <div v-on:click.capture="doThis">...</div>
  • <!-- 只当事件在该元素本身（比如不是子元素）触发时触发回调 -->
  • <div v-on:click.self="doThat">...</div>
  • <!-- 点击事件将只会触发一次 -->
  • <a v-on:click.once="doThis"></a>
  ```

  ```html
  <body>
      <div id="app">
          <button @click="say">say</button>
          <p v-show="status">{{counter}}</p>
      </div>
      <script>
          var vm = new Vue({
              el: '#app',
              data: {
                  counter: 'Hello World!',
                  status: false
              },
              methods: {
                  say() {
                      this.status = true
                  }
              }
          })
      </script>
  </body>
  ```

- **v-for指令**

  v-for指令基于一个数组来渲染一个列表，v-for指令需要使用`item in items`形式的特殊语法，其中 items 是源数据数组，而 item 则是被迭代的数组元素的别名

  ```html
  <body>
  	<div id="app">
  		<ul>
  			<li v-for="item in nameList">{{item.name}}</li>
  		</ul>
  	</div>
  	<script>
  		var vm = new Vue({
  			el: '#app',
  			data: {
  				nameList : [
  					{name:'java'},
  					{name:'kotlin'},
  					{name:'javascript'},
  					{name:'vue'}
  				]
  			}
  		})
  	</script>
  </body>
  ```
  
  在 v-for 块中，我们可以访问所有父作用域的属性，v-for 还支持一个可选的第二个参数，即当前项的索引
  
  ```html
  <div id="app">
      <ul>
          <li v-for="(item,index) in nameList">{{index+'-'+item.name}}</li>
      </ul>
  </div>
  ```
  
  在 v-for 里使用对象，用 v-for 来遍历一个对象的属性，也可以提供第二个的参数为 property 名称 (也就是键名)
  
  ```html
  <body>
      <div id="app">
          <ul>
              <li v-for="(item,name) in obj">{{name+':'+item}}</li>
          </ul>
      </div>
      <script>
          var vm = new Vue({
              el: '#app',
              data: {
                  obj : {
                      name : '李华',
                      age : '18',
                      sex : '男'
                  }
              }
          })
      </script>
  </body>
  ```
  
  也可以用 of 替代 in 作为分隔符，因为它更接近 JavaScript 迭代器的语法
  
  ```html
  <li v-for="(item,name) of obj">{{name+':'+item}}</li>
  ```
  
- **v-bind指令**

  缩写：`:`

  ```html
  <!DOCTYPE html>
  <html lang="zh">
  <head>
  	<meta charset="UTF-8">
  	<script type="text/javascript" src="js/v2.6.10/vue.js" charset="utf-8"></script>
  	<title>Document</title>
  	
  	<style>
  		.box1{
  			width: 200px;
  			height: 200px;
  			border: 1px #333 solid;
  		}
  		.red{
  			background-color: red;
  		}
  	</style>
  </head>
  <body>
  	<div id="app">
  		<img v-bind:src="imgSrc">
  		<div :class="[classA,classB]"></div>
  	</div>
  	<script>
  		var vm = new Vue({
  			el:'#app',
  			data:{
  				imgSrc:'img/6e3b79bc0b38caafb1485faa1f501a8e_1.jpg',
  				classA:'box1',
  				classB:'red'
  			}
  		})
  	</script>
  </body>
  </html>
  ```

- **双向数据绑定**

  双向数据绑定，简单来说，就是当数据发生变化时，相应的视图会进行更新，当视图更新时，数据也会跟着变化。这样开发者就不用再去操作DOM对象，能够把更多的精力投入到业务逻辑上

  双向数据绑定在Vue里简便的实现方法就是直接使用v-model。例如：`<input type= "text" v-model= "name">`

  ```html
  <!DOCTYPE html>
  <html lang="zh">
  <head>
  	<meta charset="UTF-8">
  	<title>Document</title>
  	<script type="text/javascript" src="js/v2.6.10/vue.js" charset="utf-8"></script>
  </head>
  <body>
  	<div id="app">
  		<input type="text" v-model="inputVal">
  		<p v-once>{{inputVal}}</p>
  		<p>{{inputVal}}</p>
  	</div>
  	<script>
  		var vm = new Vue({
  			el:'#app',
  			data:{
  				inputVal:'初始数据'
  			}
  		})
  	</script>
  </body>
  </html>
  ```

- **v-once指令**

  v-once指令只渲染元素和组件一次，随后的渲染，使用了此指令的元素/组件及其所有的子节点，都会当作静态内容并跳过，这可以用于优化更新性能。v-once指令也不需要表达式



