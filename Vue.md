# Vue

——MVVM模式

了解MVC和MVVM模式

1. MVC模式
   模型（Model）－视图（View）－控制器（Controller）
   MVC是实现的是M和V的代码分离。M专注于数据传递，V专注于表达，C属于两者的桥梁

2. MVVM模式
   
   - View层：
         视图层
         在我们前端开发中，通常就是DOM层。
         主要的作用是给用户展示各种信息。
   - Model层：
         数据层
         数据可能是我们固定的死数据，更多的是来自我们服务器，从网络上请求下来的数据。
   - ViewModel层：
     视图模型层
     视图模型层是View和Model沟通的桥梁。
     一方面它实现了Data Binding，也就是数据绑定，将Model的改变实时的反应到View中
     另一方面它实现了DOM Listener，也就是DOM监听，当DOM发生一些事件(点击、滚动、touch等)时，可以监听到，并在需要的情况下改变对应的Data。
   
   MVVM（模型-视图-视图模型）
   MVVM的主要目的是分离视图层和模型，ViewModel层封装了界面展示和操作的属性和接口，
   通过数据的绑定我们可以实现将View和ViewModel相关联，当ViewModel发生数据变换时，View也会更新

现在比较流行的前端框架技术
       Angular.js   Vue.js和React.js    TypeScript

Vue.js简介
		Vue.js是目前最火的一个前端框架，react也是，它可以开发网站，也可以开发APP
		Vue.js是一套用于前后端数据分离的前端框架，关注视图层，以数据为驱动，组件化，便于和第三方库整合

Vue.js的特点
		属于轻量级框架   双向的数据绑定   指令   插件化

- 解耦视图和数据
- 可复用的组件
- 前端路由技术
- 状态管理
- 虚拟DOM

渐进式框架

-  渐进式意味着你可以将Vue作为你应用的一部分嵌入其中，带来更丰富的交互体验。
-  或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统。



## 创建Vue实例时传入的options对象

- el：

  类型：string | HTMLElement

- data：

  类型：Object | Function （组件中的data必须是一个函数）

- methods：

  类型：{[key:string] : Function}



## Vue生命周期

- Vue实例从创建到销毁的过程，这些过程中会伴随着一些函数的自调用。我们称这些函数为钩子函数


主要阶段：

- 挂载（初始化相关属性）
  1. beforeCreate()  创建前
  2. created()  创建
  3. beforeMount()  挂载前
  4. mounted()  挂载
- 更新（元素或组件的变更操作）     
  1. beforeUpdate()  更改前
  2. updated()  更改
- 销毁（销毁相关属性）
  1. beforeDestroy()  销毁前
  2. destroyed()  销毁

常用的钩子函数

| beforeCreate  | 在实例初始化之后，数据观测和事件配置之前被调用，此时data 和 methods 以及页面的DOM结构都没有初始化   什么都做不了 |
| ------------- | ------------------------------------------------------------ |
| created       | 在实例创建完成后被立即调用，此时data 和 methods已经可以使用  但是页面还没有渲染出来 |
| beforeMount   | 在挂载开始之前被调用，时页面上还看不到真实数据 只是一个模板页面而已 |
| mounted       | el 被新创建的vm.$el替换，并被挂载到实例上去之后调用该钩子函数。数据已经真实渲染到页面上  在这个钩子函数里面我们可以使用一些第三方的插件 |
| beforeUpdate  | 数据更新时调用，发生在虚拟DOM打补丁之前。页面上数据还是旧的  |
| updated       | 由于数据更新导致的虚拟DOM重新渲染和打补丁，在这之后会调用该钩子函数。页面上数据已经替换成最新的 |
| beforeDestroy | 实例销毁之前调用                                             |
| destroyed     | 实例销毁后调用                                               |

### 

## Vue的基本语法

### Mustache语法

#### 插值表达式

绑定的内容主要有文本插值和HTML插值

1. 文本插值
   {{msg}}				有闪动问题

   ```html
   <!-- 有多种写法，直接写变量也可以写表达式 -->
   <h2>{{message}}</h2>
   <h2>{{message}}，Vue</h2>
   <h2>{{firstname + lastname}}</h2>
   <h2>{{firstname + ' ' + lastname}}</h2>
   <h2>{{firstname}} {{lastname}}</h2>
   <h2>{{counter * 2}}</h2>
   ```

   

2. HTML插值
   放标签

   文本插值和HTML插值的区别
   		文本插值中的代码被解释为节点的文本内容
   		HTML插值中的代码被渲染成为视图节点
   		HTML插值是对文本插值的补充和拓展
   		Vue可以解析被绑定的内容  称为DOM节点，从而实现了动态渲染视图，Vue本身也是支持模板的

### 指令

#### v-cloak

用法：

​		1.提供样式：[ v-cloak ]{ display: none; }

​		2.在插值表达式所在位置的标签中添加 v-cloak

​				原理：先隐藏，替换好之后再显示最终的值

以属性的方式定义在元素身上，当vue初始化完毕要渲染的时候会自动取出该标签，
利用这个特性可以解决插值表达式的缺陷。 
插值表达式只会替换自己的内容，不会把整个元素的内容清空

```html
<style>
    [v-cloak] {
    display: none;
    }
</style>
<h2 v-cloak>{{message}}</h2>
```



#### v-text

填充纯文本，没有闪动问题

```html
<h2 v-text="message"></h2>
```

#### v-html

填充 HTML片段

1. 存在安全问题

2. 本网站内部的数据可以使用，来自第三方的数据不可使用

```html
<h2 v-html="url"></h2>
<!-- 该指令后面往往会跟上一个string类型、会将string的html解析出来并且进行渲染
 -->
```

#### v-pre

填充原始信息

显示原始信息，跳过编译过程

```html
<h2 v-pre>{{message}}</h2>
```



#### v-once

只编译一次，显示内容之后不再具有响应式功能

```html
<h2>{{message}}</h2>	<!-- message 发生改变时，会重新渲染页面 -->
<h2 v-once>{{message}}</h2> <!-- message 发生改变时，页面内容不变 -->
```



#### v-model

​	Vue中使用v-model指令来实现表单元素和数据的双向绑定。

​	双向数据绑定

   v-model 绑定的数据默认为 String类型

​	实现原理：利用v-bind 绑定value值 ，v-on 绑定input事件

```html
<input v-bind:value='msg' v-on:input='msg=$event.target.value' />
```

修饰符：

1. ​	lazy	让数据在失去焦点或者敲击回车才会更新

   ```js
   <input type="text" v-model.lazy="message">
   ```

2.    number   可以让在输入框中输入的内容自动转成数字类型

   ```js
   <input type="number" v-model.number="age">
   ```

3. ​    trim     可以过滤内容左右两边的空格

   ```html
   <input type="number" v-model.trim="age">
   ```

   

v-model 与 radio(单选框)

```js
 <label for="male">
     <input v-model="sex" type="radio" name="sex" id="male" value="男">男
</label>
<label for="female">
    <input v-model="sex" type="radio" name="sex" id="female" value="女">女
</label>
```

v-model 与 checkbox(复选框)

1. 单个勾选框：
   - v-model即为布尔值。
   - 此时input的value并不影响v-model的值。
2. 多个复选框：
   - 当是多个复选框时，因为可以选中多个，所以对应的data中属性是一个数组。
   - 当选中某一个时，就会将input的value添加到数组中。

```js
<!-- checkbox单选框 -->
    <label for="agree">
        <input v-model="isAgree" type="checkbox" name="sex" id="agree">同意协议
</label>
<h2>您选择地是：{{isAgree}}</h2>
<button :disabled="!isAgree">下一不</button>
<hr>
<!-- checked多选框 -->

<input type="checkbox" v-model="hobbies" value="篮球">篮球
<input type="checkbox" v-model="hobbies" value="足球">足球
<input type="checkbox" v-model="hobbies" value="代码">代码
<input type="checkbox" v-model="hobbies" value="睡觉">睡觉
<h2>您的爱好是：{{hobbies}}</h2>
data:{
    isAgree: false,
    hobbies: ['篮球', '代码']
}
```

v-model 与 select(下拉菜单)

1. 单选：只能选中一个值。
   - v-model绑定的是一个值。
   - 当我们选中option中的一个时，会将它对应的value赋值到mySelect中
2. 多选：可以选中多个值。
   - v-model绑定的是一个数组。
   - 当选中多个值时，就会将选中的option对应的value添加到数组mySelects中

```js
<!-- 选择一个 -->
<select name="abc" id="" v-model="fruit">
    <option value="苹果" >苹果</option>
    <option value="香蕉" >香蕉</option>
    <option value="菠萝" >菠萝</option>
    <option value="西瓜" >西瓜</option>
    <option value="瑞郎" >瑞郎</option>
</select>

<!-- 选择多个 -->
<select name="abc" id="" v-model="abc" multiple>
    <option value="苹果" >苹果</option>
    <option value="香蕉" >香蕉</option>
    <option value="菠萝" >菠萝</option>
    <option value="西瓜" >西瓜</option>
    <option value="瑞郎" >瑞郎</option>
</select>
```



#### v-bind

简写：  :   

值绑定 就是动态的给value赋值

1. v-bind 指令被用来响应地更新 HTML 属性

    1. v-bind:href    可以缩写为    :href;

       ```html
       //绑定一个属性
       <a v-bind:href="url">百度</a>
       //缩写形式
       <a :href="url">百度</a>
       ```

       

2. 样式处理   class样式处理

    1. 给v-bind:class 一个对象，以动态地切换class。

    2.  v-bind:class指令可以与普通的class特性共存

       ```html
       //对象语法
       //控制 isActive、isError 的值在 true和false之间进行切换
       <div v-bind:class='{active:isActive,error:isError}'></div>
       data:{
                   isActive:true,
                   isError:true
               }
       //数组语法
       <div v-bind:class='[isActive,isError]'></div>
       data:{
                   activeClass:'active',
                   errorClass:'error'
               }
       ```

       样式绑定的相关细节：

       ​	1.对象绑定和数组绑定可以结合使用

       ​	2.class绑定的值可以简化操作

       ​	3.默认的class如何处理？

       ​		默认的class会保留，并与绑定的样式共存
       
       - 对象语法的用法：
       
       ```html
       <!-- 用法一：直接通过{}绑定一个类 -->
       <h2 :class="{'active': isActive}">Hello World</h2>
       
       <!-- 用法二：也可以通过判断，传入多个值 --> 
       <h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>
       
       <!-- 用法三：和普通的类同时存在，并不冲突 
       注：如果isActive和isLine都为true，那么会有title/active/line三个类 --> 
       <h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello World</h2>
       
       <!-- 用法四：如果过于复杂，可以放在一个methods或者computed中
       注：classes是一个计算属性 --> 
       <h2 class="title" :class="classes">Hello World</h2>
       
       ```
       
       - 数组语法的用法：
       
         ```html
         <!-- 用法一：直接通过{}绑定一个类 -->
         <h2 :class="['active']">Hello World</h2>
         
         <!-- 用法二：也可以传入多个值 -->
         <h2 :class=“[‘active’, 'line']">Hello World</h2>
         
         <!-- 用法三：和普通的类同时存在，并不冲突 
         注：会有title/active/line三个类  -->
                                        
         <h2 class="title" :class=“[‘active’, 'line']">Hello World</h2>
         
         <!-- 用法四：如果过于复杂，可以放在一个methods或者computed中 
         注：classes是一个计算属性 -->
         <h2 class="title" :class="classes">Hello World</h2>
         
         ```
       
         

3. style样式处理

   - 我们可以利用v-bind:style来绑定一些CSS内联样式。

   - 在写CSS属性名的时候，比如 font-size 
     - 我使用驼峰式 (camelCase) fontSize 
     - 或短横线分隔 (kebab-case，记得用单引号括起来) ‘font-size’ 

   1.对象语法

   ```html
   <div :style="{border:borderStyle,width:widthStyle,height:heightStyle}">
   </div>
   	data:{  borderStyle: '1px solid black',
               widthStyle: '100px',
               heightStyle: '200px',}
   <!-- 简化操作 -->
   <div :style="objStyles">
   data:{    objStyles: {
                   border:'1px solid green',
                   width:'200px',
                   height:'100px'
               }}
   ```

   2.数组语法

   ```html
   <div :style="[objStyles,overStyles]"></div>
   
   objStyles: {
               border:'1px solid green',
               width:'200px',
               height:'100px'
               },
   overStyles:{
               border:'5px solid red',
               backgroundColor:'blue'
   }
   ```

   

#### 分支循环结构

1. 分支结构

   - v-if		
   - v-else
   - v-else-if
   - v-show

   1. v-if、v-else、v-else-if

      - 这三个指令与JavaScript的条件语句if、else、else if类似；
      - Vue的条件指令可以根据表达式的值在DOM中渲染或销毁元素或组件；
      - v-if后面的条件为false时，对应的元素以及其子元素不会渲染；
      - 也就是根本没有不会有对应的标签出现在DOM中。

      小问题：如果我们在有输入内容的情况下，切换了类型，我们会发现文字依然显示之前的输入的内容。

      1. 这是因为Vue在进行DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。

      2. 解答：如果我们不希望Vue出现类似重复利用的问题，可以给对应的input添加key

         并且我们需要保证 **key** 的不同

   2. v-show

   3. v-if 与 v-show 的区别：

      - v-if 控制元素是否渲染到页面

      - v-show 控制元素是否显示（已经渲染到页面了）

        开发中如何选择呢？

        - 当需要在显示与隐藏之间切片很频繁时，使用v-show

        - 当只有一次切换时，通过使用v-if

        ```
        注意点：
        (1)v-if会在切换中将组件上的事件监听器和子组件销毁和重建
        当组件被销毁时，它将无法被任何方式获取，因为他已经不再我们的DOM中
        (2)在创建父组件的时候，如果子组件的v-if被判定为假的时候，
        Vue不会对子组件做任何事，直到第一次判断为真时
        (3)v-show有更高的初始渲染开销，而v-if有更高的切换开销
        (4)v-show不支持template元素，在vue2.x引用不广泛
        v-if和v-show 都能够实现对一个元素的隐藏和显示操作,
        但是v-if是将这个元素添加或者移除到dom中，而v-show
        是在这个元素上添加 style="display:none"和移除它来
        控制元素的显示和隐藏的
        ```

2. 循环结构

- v-for
  遍历数组

  ```html
  <li v-for='item in list'></li>	<!-- 普通遍历 -->
  <li v-for='(item,index) in list'></li><!-- 有索引 遍历 -->
  <li :key='item' v-for='(item,index) in list'></li>
  <!-- list 代表数组-->
  <!-- index 代表索引号 -->
  <!-- key的作用：帮助Vue区分不同的元素，提高性能 -->
  ```

  ```js
  /*接下来大家需要记住关于数据相关的方法   列表渲染 
  响应式的：通过下面的方法修改数组，数据会响应式地变化  
  名称            描述
  push()            将一个或多个元素添加至数组末尾，并的返回新数组的长度
  pop()            将数组中删除并返回最后一个元素
  shift()          从数组中删除并返回第一个元素
  unshift()        在数组中最前面添加一个或多个元素添加
  splice()         从数组中删除元素或向数组添加元素
  sort()           对数组元素排序，默认按照Unicode编码书，返回排序后的数组
  reverse)()        将数组中的元素位置颠倒，返回调到后的数组 
  Vue中地一个方法：Vue.set(要修改的对象,索引值,修改后的值)
  
  通过索引修改数组中的元素不会响应式地改变
  Vue.set()方法是响应式的
  Vue.set(要修改的对象, 索引值, 修改后的值)
  Vue.set(this.letters,0,'bbb')
  */
  ```
```
  
  遍历对象
  
  ```html
  <li v-for='value in object'></li>	<!-- 只有值 -->
  <li v-for='(value,key) in object'></li><!-- 有值、键 -->
  <div v-for='(value,key,index) in object'></div>
  <!-- 
  value 代表 值
  key   代表 键
  index 代表 索引
  object 代表 对象
在循环对象中我们使用了key 但记号了在组件使用时，必须是vue2.2.x以上的版本
  -->
```

  ```html
  <!-- v-if 和 v-for结合使用 -->
  <div v-if='value==12' 
       v-for='(value,key,index) in object'>
  </div>
  <!-- value 等于 12 的数据才显示 -->
  ```

官方推荐我们在使用v-for时，给对应的元素或组件添加上一个:key属性。

1. 所以我们需要使用key来给每个节点做一个唯一标识
2. Diff算法就可以正确的识别此节点
3. 找到正确的位置区插入新的节点。
4. 所以一句话，**key** 的作用主要是为了高效的更新虚拟 **DOM** 。

补充：

1. v-for可遍历 数组、对象、字符串、指定次数
2. 虚拟DOM中key的作用：key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据新数据生成【新的虚拟DOM】，与【旧虚拟DOM】进行差异比较，规则如下：
   1. 【新的虚拟DOM】与【旧虚拟DOM】有相同的key
      - 若虚拟DOM中内容没变，直接使用之前的真实DOM
      - 若虚拟DOM中内容发生变化，则生成新的真是DOM，替换掉页面中之前的真实DOM
   2. 【新的虚拟DOM】与【旧虚拟DOM】没有相同的key
      - 创建新的真实DOM，随后渲染到页面
   3. key一般为元素的 **唯一标识**



#### 事件的绑定  v-on

 1. v-on

      1. 缩写： @

     2. 用法：<input type='button' v-on:cliclk='say' />

        简写：<input  type='button'  @cliclk='say'  />

        事件函数调用方式：直接绑定函数名 或者  调用函数（可以传参数）

        参数传递：

        ​		1.如果事件直接绑定函数名称，那么默认将原生事件event参数传递进去；

        ​		2.如果事件绑定函数调用，那么事件对象event必须作为最后一个参数显示传递，并且事件对象的名称必须是 $event

        ​			<input  type='button'  @cliclk='say('hi',$event)'  />

        ​			参数可以是：任意数据类型，或者是 data 里面的数据

        事件修饰符：

        ​	.stop	阻止事件冒泡	<a @click.stop='handle'>跳转</a>

        ​	.prevent	阻止默认行为	<a @click.prevent='handle'>跳转</a>

        ​	修饰符可以串联：<a @click.stop.prevent='handle'>跳转</a>

        ​	.enter  键盘敲击回车是才触发	<input type="text" @keyup.enter="keyUp">

        ​	.native - 监听组件根元素的原生事件

        ​	.once - 只触发一次回调(只能点击一次)

        ```
        .stop - 调用 event.stopPropagation()。
        .prevent - 调用 event.preventDefault()。
        .capture - 添加事件侦听器时使用 capture 模式。
        .self - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
        .{keyCode | keyAlias} 只当事件是从特定键触发时才触发回调。
        .native - 监听组件根元素的原生事件。
        .once - 只触发一次回调。
        .left - (2.2.0) 只当点击鼠标左键时触发。
        .right - (2.2.0) 只当点击鼠标右键时触发。
        .middle - (2.2.0) 只当点击鼠标中键时触发。
        .passive - (2.3.0) 以 { passive: true } 模式添加侦听器
        
        ```

        按键修饰符：

        ​	.enter	回车键	<input v-on:key.enter='submitg'>

        ​	.delete	删除键	<input v-on:key.delete='submitg'>

        ```
        .enter
        .tab
        .delete (捕获“删除”和“退格”键)
        .esc
        .space
        .up
        .down
        .left
        .right
        
        自定义按键修饰符：自定义按键修饰符名字是自定义的，但是对应的值必须是按键对应 event.keyCodes 值
        	Vue.config.keyCodes.aa = 65;
        ```




## Vue的常用特性



### 表单操作

- Input		单行文本
  	

  ```html
  <input type="text" v-model='uname'>
  <!-- v-model 双向绑定 -->
  ```

- textarea   多行文本

  ```html
  <textarea v-model='desc'></textarea>
  <!-- v-model 双向绑定 --> -->
  ```

- select       下拉多选

  ```html
  <select v-model='occupation' multiple>
      <option value="0">请选择职业...</option>
      <option value="1">教师</option>
      <option value="2">软件工程师</option>
      <option value="3">律师</option>
  </select>
  <!-- v-model 双向绑定 --> 
  <!--multiple 不写值 默认为true，可以多选-->
  <!-- 使用 value 区分  -->
  <!-- occupation:[3,2,1]  值是 数组的形式 -->
  ```

- radio        单选框

  ```html
   <input type="radio" id="male" value="1" v-model='gender'>
  <label for="male">男</label>
  <input type="radio" id="female" value="2" v-model='gender'>
  <label for="female">女</label>
  <!-- v-model 双向绑定 --> 
  <!-- 使用 value 区分  -->
  ```

- checkbox  多选框

  ```html
  <input type="checkbox" id="ball" value="1" v-model='hobby'>
  	<label for="ball">篮球</label>
  <input type="checkbox" id="sing" value="2" v-model='hobby'>
  	<label for="sing">唱歌</label>
  <input type="checkbox" id="code" value="3" v-model='hobby'>
  	<label for="code">写代码</label>
  <!-- v-model 双向绑定 --> 
  <!-- 使用 value 区分  -->
  <!--    hobby:[3,2,1]  值是 数组的形式-->
  ```

  表单域修饰符

  - number ：转化为数值

  - trim ：去掉开始和结尾的空格（字符中间的空格不能去掉）

  - lazy ：将input 事件切换为 change事件

    ​	input 事件：只要有内容变化就会触发
    ​	change 事件：只有 失去焦点 或 按下回车键 时才触发

    ```html
    <input type="text" v-model.number="age">
    <input type="text" v-model.trim="info">
    <input type="text" v-model.lazy="msg">
    ```

### 自定义指令

1. 自定义指令的语法规则

   ```js
   Vue.diretive('focus',{//获取元素焦点
       inserted:function(el){
           el.focus();
       }
   })
   //自定义指令的 名称：'focus'
   ```

   自定义指令的用法

   ```html
   <input type='text' v-focus>
   ```

2. 带参数的自定义指令

   ```js
   Vue.directive('color',{
       bind:function(el,binding){
           el.style.backgroundColor = binding.value.color;
       }
   });
   //binding 是指 {color:'red'}，value属性是的到 值：red
   ```

   带参数自定义指令的用法

   ```html
    <input type="text" v-color="{color:'red'}" >
    <!-- 或者 -->
    <input type="text" v-color="msg" >
   
           var vm = new Vue({
               el: '#app',
               data: {
                   msg:{
                   color:'blue'
                   }
               },
               methods: {}
           })
   ```

   局部指令

   ​	可以定义多个局部指令，用 , 隔开

   ```js
   directives: {
       color: {
           bind: function (el, binding) {
               el.style.backgroundColor = binding.value.color;
           }
       },
       focus:{
           inserted:function(el){
               el.focus();
           }
       }
   }
   ```

   

### 计算属性        computed: { }

1. 在Vue实例参数中添加一个新的属性：computed: { }，通过函数的形式定义计算属性 ，直接通过 函数名 使用(不用加括号)，计算属性是基于 data中的数据进行处理的

   ```html
   <h2>{{reveredMessage}}</h2>
   computed: {
   	reveredMessage: function () {
           return  this.msg.split('').reverse().jopin('')
       }
   }
   ```

2. 每个计算属性都包含一个get和一个set，一般没有set方法（只读属性）

   ```js
   conputed:{
       fullName: {
           set: function(newValue) {},// 一般不写set方法，只有只读属性
           get: function() {}
       },	// 计算属性完整写法
       fullName:function(){}  // 计算属性简写
   }
   ```

   

3. 计算属性 与 方法的区别   即：computed 与 methods 的区别

   计算属性会进行缓存，如果多次使用时，计算属性只会调用一次。

   - 计算属性是基于它们的依赖进行缓存的
     	依赖没有改变就不会再次执行计算属性

   - 方法不存在缓存

     每次调用都会执行
     
     

### 侦听器      watch: { }

应用场景：数据变化时执行异步或开销较大的操作

![](D:\md\imgs\侦听器.png)

侦听器的用法：

```js
watch: {
	firstName: function(val){  
        //属性的名称 与 方法的名称 必须一致，这样才能监听是哪个属性
        //val表示变化之后的值
        this.fullName = val + this.lastName;
    },
      lastName:function(val){
          this.fullName = this.firstName + val;
      }
}
```



### 过滤器

主要用于格式化数据

1. 自定义过滤器（全局过滤器）

   ```js
   Vue.filter('过滤器名称' , function(val){
       //过滤器的逻辑业务
   })
   ```

2. 局部过滤器

   ```js
   //在本组件中使用
   var vm = new Vue({
           el: '#app',
           data: {
               msg: '',
           },
           methods: {},
           filters:{
               upper: function(val){
   			//过滤器的逻辑业务
               }
           }
       })
   ```

3. 过滤器的使用

   ```html
   <div>{{msg | upper}}</div>	<!-- 在插值表达式中使用 -->
   <div>{{msg | upper | lower}}</div>	<!-- 支持级联操作 -->
   <div :abc='msg | upper'>测试数据</div>	<!-- 在属性绑定中使用 -->
   <!-- upper lower 为过滤器的名称 -->
   ```

4. 带参数的过滤器

   使用参数时：通过 （）的方式传递参数

   从第二个参数进行接受参数

   ```html
   <div>{{date | format( 'yyyy-MM-dd hh:mm:ss' )}}</div>
   ```

   ```js
   //arg 为传递的参数
   // function(value,arg=‘设置默认值’){// 逻辑}
   Vue.filter('format',function(value,arg){
      if (arg == 'yyyy-MM-dd') {
         var ret = '';
         ret += value.getFullYear() + '-' + (value.getMonth() + 1) + '-' + value.getDate()
          return ret;
       }
     return value;
   })
   ```
   
   

### 数组相关的API

1. 变异方法（修改原有数据）
   - push()
   - pop()
   - shift()
   - unshift()
   - splice()
   - sort()
   - reverse()
2. 替换数组（生成新的数组）
   - filter()
   - concat()
   - slice()
3. 修改响应式数据
   - Vue.set(vm.items,indexOfltem,newValue)
   - vm.$set(vm.items,indexOfltem,newValue)
     1. 参数一表示要处理的数组名称
     2. 参数二表示要处理的数组的索引
     3. 参数三表示要处理的数组的值

## 组件

- 组件 (Component) 是 Vue.js 最强大的功能之一

- 组件可以扩展 HTML 元素，封装可重用的代码

  组件使用的三个步骤：

  1. 创建组件构造器；
  2. 注册组件；
  3. 使用组件。

### 组件注册

1. 全局组件注册语法

   **全局组件**注册后，任何**vue实例**都可以用

   ```js
   Vue.extend(参数);//创建组件构造器
   Vue.component('组件的标签名',组件的构造器);//注册组件
   //语法糖注册方式
   Vue.component('组件名称'，{
       data: 组件数据,		//data 必须是一个函数
       template: 组合模板内容 	//组件模板内容必须是单个根元素
   })
   ```

   组件用法

   ```html
   <div id="app" >
       <组件名称></组件名称>
   </div>
   ```

   例：

   ```js
   // 创建组件
   const cpnC = Vue.extend({
       template: `<div>  
               <h2>标题</h2>
               <h3>内容</h3>
               <h4>结尾</h4> 
               </div>`,
   });
   // 注册组件 Vue.component('组件的标签名');
   Vue.component('my-cpn', cpnC);
   //使用组件
   <my-cpn></my-cpn>
   
   Vue.component('button-counter', {
           data: function () {
               return {
                   count: 0,
               }
           },
           template: '<button @click="handle">点击了{{count}}次</button>>',
           methods: {
               handle: function () {
                   this.count += 2;
               }
   }
   ```

   ```html
   <div id="app">
       <button-counter></button-counter>
   </div>
   ```

   组件注册的注意事项

   1. data必须是一个函数（保证每个组件的数据是相互独立的）

   2. 组件模板内容必须是单个根元素（语法要求）

   3. 组件模板内容可以是模板字符串（模板字符串需要浏览器提供支持）

   4. 组件命名方式

      - 短横线方式

        ```js
        Vue.component('my-component',){/* ... */}
        ```

      - 驼峰方式

        ```js
        Vue.component('MyComponent',{/* ... */})
        ```

        使用 驼峰式命名组件 只能在字符串模板中使用，

        但是在普通标签模板中，必须使用短横线的方式使用组件

      ```js
      Vue.component('button-counter', {
              data: function () {return { count: 0,}},
              template: //模板字符串
          `<div>
            <button @click="handle">点击了{{count}}次</button>
             <button>测试</button>
           </div>`,
              methods: {}
          })
      ```

2. 局部组件注册
   局部组件只能在注册他的父组件中使用

   components: {        }

   ```js
   const cpn = Vue.extend({
               template: `<div>
                       <h1>哈哈哈</h1>
                       <h2>123</h2>
                       <h3>456</h3>
                   </div>`
           });
   const app = new Vue({
       el: '#app',
       components: { //Vue实例中注册全局组件
           cpn: cpn
       }
   });
   
   var HelloWorld = {        /* ... */    };
   var HelloTom = {        /* ... */    };
   var HelloJay = {        /* ... */    };
   
   var vm = new Vue({
           el: '#app',
           data: {},
           components: {
              'cpn2':{template:`<div>
   					<h2>局部组件的注册</h2>
   				</div>`}
           }
       })
   ```

### 模板的分离写法

1. 使用<script>标签
2. 使用<template>标签

```JS
 <!-- 1. script标签 -->
  <script id="cpn" type="text/x-template">
    <div>
        <h2>我是标题</h2>
		<p>我是内容</p>
	</div>
</script>
    <!-- 2. template标签 -->
<template id="cpn">
    <div>
        <h2>我是标题cpn</h2>
        <p>我是内容</p>
    </div>
</template>
```



### 父组件和子组件

```js
const son = Vue.extend({
    template: `
        <div>
            <h2>我是son标题</h2>    
            <p> 我是son内容 </p>
        </div>
        `,
});
const fater = Vue.extend({
    template: `
        <div>
            <son></son>
            <h2>我是fater标题</h2>    
            <p> 我是fater内容 </p>
        </div>
        `,
    components: {	
        son: son	// 在 fater组件里面 注册 son组件
    }
});
```

### 组件中数据的存放

1. 组件对象也有一个data属性(也可以有methods等属性，下面我们有用到)
2. 只是这个data属性必须是一个函数
3. 而且这个函数返回一个对象，对象内部保存着数据

```js
Vue.component('cpn', {
    template: '#cpn',
    data() {
        return {
            title: 'abc'
        }
    }
});
/*为什么data在组件中必须是一个函数呢?
首先，如果不是一个函数，Vue直接就会报错。
其次，原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响。*/

```



### Vue调试工具

### 组件间数据交互

#### 父组件向子组件传值

1. 子组件内部通过 **props** 接受父组件传递过来的值

   ```js
   Vue.component('menu-item',{
       props:['title'],
       template:'<div>{{title}}</div>'
   })
   ```

2. 父组件通过属性将值传递给子组件 通过 v-bind

   ```html
   <menu-item title="父组件传递过来的值"></menu-item> <!-- 静态绑定-->
   <menu-item :title="Ftitle"></menu-item>  <!-- 动态绑定 -->
   ```

3. **props** 属性名规则

   - props传递数据原则：单向数据流（父组件给子组件传递数据）

   - 在 props 中使用驼峰形式，模板中需要使用短横线的形式

   - 字符串形式的模板中没有这个限制

     ```html
     <menu-item :menu-title='ptitle'></menu-item>
     <!-- 在html中使用是短横线形式 -->
     ```

     ```js
      Vue.component('menu-item', {
     	props: ['menuTitle'],
     	template: '<div>{{menuTitle}}												<third-com testTitle="hello"></third-com> 	
         		 </div>' 
          //在js中使用是驼峰形式
     });
     Vue.component('third-com', {
         props: ['testTitle'],
         template: '<div>{{testTitle}}</div>'
     });
     ```

4. **props** 基本用法

   - props的值有两种方式：

      ​	方式一：字符串数组，数组中的字符串就是传递时的名称。

      ​	方式二：对象，对象可以设置传递时的类型，也可以设置默认值等。

      ​				当需要对 **props** 进行类型等验证时，就要使用对象类型

      - 验证都支持哪些数据类型呢？

         **String** **Number** **Boolean** **Array** **Object** **Date** **Function** **Symbol** 

   - ```js
     const cpn = {
         template: '#cpn',
         // props: ['cmovies', 'cmessage']	//字符串数组
         props: { // 对象
             cmovies: Array,	//定义传来值得类型 Array
             cmessage: {	、
                 // type定义传来值得类型(type为null是，匹配任何类型)
                 type: String,	
                 required: true	//required 定义为必须填写得字段
                 default: 'aaaaaa',	// default 定义默认值
                	//当默认值是 对象或数组 必须从一个工程函数获取
                 //       default() {return 对象或数组}
             
         }
             },
         },
     }
     ```

     

   

#### 子组件向父组件传值

- 子组件用`$emit()`触发事件

- `$emit('事件名称',参数)`  第一个参数为 自定义的事件名称     第二个参数为需要传递的数据

- 父组件用v-on 监听子组件的事件

1. 子组件通过自定义事件向父组件传递信息

   ```html
   <button @click="$emit('enlarge-text',参数)">扩大父组件中的字体大小</button>
   ```

2. 父组件监听子组件的事件

   ```html
   <!-- 父组件通过 $event 接收参数 -->
   <menu-item :parr="parr" v-on:enlarge-text="handle($event)"></menu-item>
   <!-- 简写如下： -->
   <menu-item :parr="parr" @enlarge-text="handle($event)"></menu-item>
   <!-- 自定义的事件名称 和 父组件监听的事件名称 相同 ，enlarge-text  -->
   <!-- $event 获取传递的参数 -->
   ```


#### 父子组件的访问方式

1. 父组件访问子组件：使用 **$children** 或 **$refs**  reference(引用)

   -  **this.$children** 是一个数组类型，它包含所有子组件对象。
        我们这里通过一个遍历，取出所有子组件的message状态。

   -  **$refs** 的使用：（如果没有组件 ref 属性则 **this.$refs** 为空对象 ）

     $refs和ref指令通常是一起使用的。

     首先，我们通过ref给某一个子组件绑定一个特定的ID。

     其次，通过this.$refs.ID就可以访问到该组件了。

   

2. 子组件访问父组件：使用 **$parent** 

   - 允许通过 $parent 来访问父组件，但是在真实开发中尽量不要这样做。

3. 直接访问 Vue实例：**$root**

   - 直接访问根组件 **this.$root** 



#### 非父子组件间的传值

​		(  兄弟组件间的传值  )

1. ​	单独的事件中心管理组件间的通信
   ​	

   ```js
   //事件中心
   var eventHub = new Vue();
   ```

2. ​    监听事件与销毁事件

   ```js
   eventHub.$on('add-todo',函数);  //监听事件
   eventHub.$off('add-todo');   //销毁事件
   ```

3. 触发事件

   ```js
   event.$emit('add-todo',参数)
   ```

<img src="D:\md\imgs\事件中心管理组件间的通信.png" style="zoom: 80%;" />



### 组件插槽  slot

##### 插槽的基本使用

- 在 template 中使用  <slot></slot>  标签

```js
Vue.component('alert-box',{
        template:`
            <div>
                <strong>ERROR:</strong>
                <slot>默认内容</slot>  
            </div>
        `, // 默认内容 可以不写
});
```

插槽的内容

```css
/* 组件标签中的内容会传递给 标签<slot></slot> */
<alert-box>有BUG</alert-box>  
  /* 组件标签中没有内容，则显示 标签<slot></slot> 中默认的内容 */
<alert-box></alert-box> 
```

##### 具名插槽

- 具名插槽用法：
  在 <slot></slot> 中的添加 "**name**" 属性绑定元素 
```html
  <template>
      <slot name="left">左边</slot>
    <slot name="center">中间</slot>
      <slot name="right">右边</slot>
  </template>
```

   在普通HTML标签中添加 "**slot** " 属性来指定, 这个slot的值必须和下面组件 slot 的 name 值对应上
   如果没有匹配到 则放到匿名的插槽中

  ```js
<cpn>
    <span slot="left">&lt;</span>
    <input slot="center" type="text" value="请输入商品">
    <button slot="right">搜索</button>
</cpn>
  ```

  插槽内容

  使用 <slot> 中的 "name" 属性绑定元素 指定	插槽的名字

  ```html
  <base-layout>
          <p slot="header">header信息</p>
          <p>主要内容1</p>
          <p>主要内容2</p>
          <p slot="footer">footer信息</p>
      </base-layout>
  /*-------------------------------------------------*/
  <base-layout>
      <!-- 注意点：template标签最终不会渲染到页面上     --> 
          <template slot="header">
              <p>header信息1</p>
              <p>header信息2</p>
          </template>
              <p>主要内容1</p>
              <p>主要内容2</p>
          <template slot="footer">
              <p>footer信息1</p>
            <p>footer信息2</p>
          </template>
  </base-layout>
  ```

  注意：具名插槽的渲染顺序，完全取决于模板，而不是取决于父组件中元素的顺序

##### 编译作用域

 **父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译。** 

案例：

```html
<div id="app">
	<cpn v-show="isShow"></cpn>  <!-- 在Vue实例 app中找 isShow -->
</div>
<template id="cpn">
    <div>
        <h2>我是子组件</h2> 
        <p v-show="isShow">我是内容，哈哈哈</p>  <!-- 在子组件 cpn中找 isShow -->
    </div>
</template>
<script>
        const app = new Vue({
            el: '#app',
            data: {
                isShow: true
            },
            methods: {},
            components: {
                cpn: {
                    template: '#cpn',
                    data() {
                        return {
                            isShow: false
                        }
                    },
                }
            }
        });
</script>
```



##### 作用域插槽

- 作用域插槽 —— 父组件替换插槽的标签，但是内容由子组件来提供。
  应用场景：父组件对子组件的内容进行加工处理
  
- 父组件中在 template标签中添加 slot-scope属性(固定写法)
  
- 子组件插槽中定义 :data="" 传入子组件中的数据 pLanguages data为自定义名称
  
  - 既可以复用子组件的slot，又可以使 <slot> 标签的内容不一致
  
  ```html
  <div id="app">
      <cpn></cpn>
      <cpn>
          <!-- 父组件中在 template标签中添加 slot-scope属性(固定写法) -->
          <template slot-scope="slot">
              <span v-for="item in slot.data"> {{item}} -</span>
          </template>
      </cpn>
  </div>
  <template id="cpn">
      <div>
          <slot :data="pLanguages"> 
         <!-- 子组件插槽中定义 :data="" 传入子组件中的数据 pLanguages 
  		data为自定义名称-->
              <ul><li v-for="item in pLanguages">{{item}}</li></ul>
        </slot>
      </div>
  </template>
  <script>
      const app = new Vue({
          el: '#app',
          data: {},
          methods: {},
          components: {
              cpn: {
                  template: '#cpn',
                  data() {
                      return {
                          pLanguages: ['js', 'java', 'c++', 'c#', 'python', 'go', 'swift']
                    }
                  }
              }
          }
      });
  </script>
  ```
  
  ```html
  <!--
  当我们希望li 的样式由外部使用组件的地方定义，因为可能有多种地方要使用该组件,但样式希望不一样 这个时候我们需要使用作用域插槽 
  -->
  <!-- 父组件中使用了<template>元素,而且包含 slot-scope 属性(固定的)，slot-scope="slotProps"，slotProps为自定义，用于接受info传过来的数据-->
  <fruit-list :list="list">
      <template slot-scope="slotProps">
          <strong v-if="slotProps.info.id==3" class="current">				{{slotProps.info.name}}
          </strong>
          <span v-else>{{slotProps.info.name}}</span>
      </template>
  </fruit-list>
  ```
  
  



## Vue  Router  路由

- 前端路由
  - 概念：根据不同的用户事件，显示不同的页面内容
  - 本质：用户事件与事件处理函数之间的对应关系
  - 核心：改变URL，但是页面不进行整体的刷新
  - 前端路由负责事件监听，触发事件后，通过事件函数渲染不同的内容
  - 由前端写的 js 代码在浏览器中执行，最终渲染出来的网页

前端渲染/后端渲染

SPA页面（单页面富应用）：SPA最主要的特点就是在前后端分离的基础上加了一层前端路由，也就是前端来维护一套路由规则.

### 准备

- URL的hash：URL的hash也就是锚点(#), 本质上是改变window.location的href属性，我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新
- HTML5的history模式：pushState
- HTML5的history模式：replaceState
- HTML5的history模式：go
  1.  history.back() 等价于 history.go(-1)
  2. history.forward() 则等价于 history.go(1)

#### 安装和使用vue-router

1. 安装vue-router：*npm install vue-router --save* 
2. 安装路由功能：
   1. 导入路由对象，并调用Vue.use(VueRouter)
   2. 创建路由实例，并且传入路由映射配置
   3. 在Vue实例中挂载创建的路由实例

使用vue-router的步骤：

1. 创建路由组件
2. 配置路由映射：组件和映射的关系
3. 使用路由：通过<router-link>和<router-view>



#### 配置路由的默认路径

```js
const routes = [{//默认路径
    path: '/',
    redirect: '/home'  // redirect：重定向
}, {//home路径
    path: '/home',
    component: Home
}, {//about路径
    path: '/about',
    component: About
}]
```

#### 更改H5中history

```js
export default new Router({
    //配置路由和组件之间的应用关系
    routes,
    mode: 'history'	//mode:'history'   -->使用 H5中的history模式
})
```

### router-link 补充

<router-link>默认渲染出来的是  <a>标签

- to: 指定跳转的路由

  ```js
  <router-link to="/home">首页</router-link>  //跳转到 '/home'
  ```

<router-link>其他属性：

- **tag**: tag可以指定<router-link>渲染成的组件

  ```js
  <router-link to="/home" tag="button">首页</router-link> //渲染成 button
  <router-link to="/home" tag="li">首页</router-link>  //渲染成 li
  ```

- **replace**: preplace不会留下history记录, 所以指定replace的情况下, 后退键返回不能返回到上一个页面中

  ```js
  <router-link to="/home" tag="button" replace>首页</router-link>
  ```

- **active-class**: 当<router-link>对应的路由匹配成功时, 会自动给当前元素设置一个router-link-active的class, 设置active-class可以修改默认的名称.

  ```js
  <router-link to="/home"active-class="active">首页</router-link>
  ```

  当需要修改多个<router-link>router-link-active的class时，通过router实例的属性进行修改 **linkActiveClass** 

  ```js
  export default new Router({
      routes,
      mode: 'history',
      linkActiveClass: 'active'  
  })
  ```

#### 通过代码跳转路由

this.$router.push('/路由')：可以返回上一个页面

this.$router.replace('路由')：不能返回上一页面

```html
<template>
  <button @click="homeClick">首页</button>
  <button @click="aboutClick">关于</button>
</template>
<script>
export default {
  name: 'App',
  methods:{
    homeClick(){
      this.$router.push('/home') //代码
    },
    aboutClick(){
      this.$router.push('/about') //代码
    }
  }
}
</script>
```

### 动态路由

在某些情况下，一个页面的path路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：/user/aaaa或/user/bbbb，除了有前面的/user之外，后面还跟上了用户的ID。

这种path和Component的匹配关系，我们称之为动态路由(也是路由传递数据的一种方式)。

![](imgs\Vue\动态路由.png)



### 路由的懒加载

结合 Vue 的异步组件和 Webpack 的 代码分割功能，轻松实现路由组件的懒加载。

- 路由懒加载的主要作用就是将**路由对应的组件打包成一个个的js代码块**.
- 只有在这个路由被访问到的时候, 才加载对应的组件

#### 懒加载的方式

1. 结合Vue的异步组件和Webpack的代码分析

   ```js
   const Home = resolve => { require.ensure(['../components/Home.vue'], () => { resolve(require('../components/Home.vue')) })};
   ```

2. AMD写法

   ```js
   const About = resolve => require(['../components/About.vue'], resolve);
   ```

3. **ES6中, 我们可以有更加简单的写法来组织Vue异步组件和Webpack的代码分割** 

   ```js
   const Home = () => import('../components/Home.vue')
   ```

### 嵌套路由

- 创建对应的子组件, 并且在路由映射中配置对应的子路由.
- 在组件内部使用<router-view>标签.

```html
<template>
    <div>
        <h2>我是Home</h2>
        <p>123</p>
    <router-link to="/home/news">新闻</router-link>
    <router-link to="/home/message">信息</router-link>

        <router-view></router-view>
    </div>
</template>
```

```js
const routes = [{ // 默认路由
    path: '/',
    redirect: '/home' //redirect 路由重定向
}, {
    path: '/home',
    component: Home,
    // 在 children 里面配置子路由
    children: [{
            path: '/',
            redirect: 'news'
        },
        {
            path: 'news',
            component: HomeNews
        }, {
            path: 'message',
            component: Homemessage
        }
    ]
} ]
```



### 传递参数

传递参数的类型：params和query

1. **params**的类型:		**$route.params** 获取参数
   - 配置路由格式: /router/:id
   - 传递的方式: 在path后面跟上对应的值
   - 传递后形成的路径: /router/123, /router/abc
2. **query**的类型:            **$route.query** 获取参数
   - 配置路由格式: /router, 也就是普通配置
   - 传递的方式: 对象中使用query的key作为传递方式
   - 传递后形成的路径: /router?id=123, /router?id=abc

1. params         $route.params

   ```html
   <router-link :to="'/user/'+userId">用户</router-link> //
   <button @click="userClick">用户</button><!--手动配置-->
   
   <script>
   export default {
     name: 'App',
     data(){
       return{ userId:'zhangsan' }
     },
     methods:{
       //手动配置路由
       userClick(){
         this.$router.push('/user/'+this.userId)
       }
     }
   }
   </script>
   ```

2. query           $route.query

   ```html
   <router-link :to="{path:'/profile',query:{name:'lihao',age:18,height:1.88}}">档案</router-link>
   <button @click="profileClick">档案</button><!--手动配置-->
   
   <script>
   export default {
     name: 'App',
     data(){
       return{ userId:'zhangsan' }
     },
     methods:{
       //手动配置路由
       profileClick(){
         this.$router.push({
           path:'/profile/'+123,
           query:{name:'lihao',age:18,height:1.88}
         })
       }
     }
   }
   </script>
   ```

   

### $router 和 $route 的区别

- $router是VueRouter的一个对象，通过Vue.use(VueRouter)和Vue构造函数得到一个router的实例对象，这个对象中是一个全局的对象，他包含了所有的路由，包含了许多关键的对象和属性。
- $route是一个跳转的路由对象（活跃的路由），每一个路由都会有一个$route对象，是一个局部的对象，可以获取对应的name，path，params，query等。



### 导航守卫

1. vue-router提供的导航守卫主要用来监听监听路由的进入和离开的.

2. vue-router提供了 **beforeEach**（前置守卫） 和 **afterEach**（后置守卫） 的钩子函数, 它们会在路由即将改变前和改变后触发.

3. 导航钩子的三个参数解析:

   - to: 即将要进入的目标的路由对象.
   - from: 当前导航即将要离开的路由对象.
   - next: 调用该方法后, 才能进入下一个钩子.

4. beforeEach 需要主动调用 next()，afterEach 不需要主动调用next()函数.

   ```js
   router.beforeEach((to, from, next) => {
     next()  //beforeEach 需要主动调用 next()
   })
   router.afterEach(route => {
   	//afterEach 不需要主动调用next()函数.
   })
   ```

5. 我们使用的导航守卫, 被称之为 **全局守卫** 。

   1. 路由独享的守卫 

      ```js
      //你可以在路由配置上直接定义 beforeEnter 守卫：
      const router = new VueRouter({
        routes: [
          {
            path: '/foo',
            component: Foo,
            beforeEnter: (to, from, next) => {
              // ...
            }
          }
        ]
      })
      ```

   2. 组件内的守卫 

      - beforeRouteEnter
      - beforeRouteUpdate (2.2 新增)
      - beforeRouteLeave

      ```js
      const Foo = {
          template: `...`,
          beforeRouteEnter (to, from, next) {
          // 在渲染该组件的对应路由被 confirm 前调用
          // 不！能！获取组件实例 `this`，因为当守卫执行前，组件实例还没被创建
          },
          beforeRouteUpdate (to, from, next) {
          // 在当前路由改变，但是该组件被复用时调用
          // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
          // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
          // 可以访问组件实例 `this`
          },
          beforeRouteLeave (to, from, next) {
          // 导航离开该组件的对应路由时调用
          // 可以访问组件实例 `this`
          }
      }
      ```

### 路由元信息

*定义路由的时候可以配置 `meta` 字段：* 

​	利用   *$route.matched*   数组 遍历得到   meta

```js
{
    path: '/user/:id',
    component: User,
    meta: {   //meta 路由元信息
        title: '用户'
    }
}
```

利用 **beforeEach** 和 **路由元信息** 完成标题的修改

```js

const routes = [{ // 默认路由
    path: '/',
    redirect: '/home' //redirect 路由重定向
}, {
    path: '/home',
    component: Home,
    meta: {	// meta 被称为路由元信息
        title: '首页'
    }
}, {
    path: '/about',
    component: About,
    meta: {
        title: '关于'
    }
}
}]
const router = new Router({
    //配置路由和组件之间的应用关系
    routes,
    mode: 'history',
    linkActiveClass: 'active'
})

router.beforeEach((to, from, next) => {
    document.title = to.matched[0].meta.title
    next()
})
```



### keep-alive

- keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。

- 两个重要的属性

  1. ***include***  字符串或正则表达，只有匹配的组件会被缓存
  2. ***exclude*** 字符串或正则表达式，任何匹配的组件都不会被缓存

- ```html
  <keep-alive exclude="Profile,User">	 <!-- Profile，User 不会被缓存 -->
      <router-view></router-view>	
  </keep-alive>
  <keep-alive include="Home,About">	 <!-- Home,About 会被缓存 -->
      <router-view></router-view>	
  </keep-alive>
  ```

***activated 和 deactivated：只有该组件被保持了状态使用 keep-alive 时，才是有效的*** 

```js
 //activated和deactivated：只有该组件被保持了状态使用 keep-alive 时，才是有效的
activated () {
    // activated 函数是：进入活跃时回调的函数
    this.$router.push(this.path);
},
    deactivated () {
        // 不活跃时回调
    },
```

首页中使用 path 属性记录离开时的路径

```js
<script>
export default {
    name:'Home',
    data(){
        return {path:'/home/news'}
    },
    activated () {
        // activated 函数是：进入活跃时回调的函数
        this.$router.push(this.path);
    },
    deactivated () {
        // 不活跃时回调
    },
    beforeRouteLeave(to, from, next)  {
        //组件内的守卫，导航离开该组件的对应路由时调用
        this.path = this.$route.path
        next()
    }
}
</script>
```



## VueX

——Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。

- 它采用 ***集中式存储管理*** 应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
- Vuex 也集成到 Vue 的官方调试工具 [devtools](https://github.com/vuejs/vue-devtools)[ extension](https://github.com/vuejs/vue-devtools)，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。
- 状态自管理应用包含以下几个部分：
  - **state**，驱动应用的数据源；
  - **view**，以声明方式将 **state** 映射到视图；
  - **actions**，响应在 **view** 上的用户输入导致的状态变化。

安装

```
npm install vuex --save
```

在一个模块化的打包系统中，您必须显式地通过 `Vue.use()` 来安装 Vuex：

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```





### 核心概念

- State
- Getters
- Mutation
- Action
- Module

### State

——**单一状态树** Single Source of Truth

它便作为一个“唯一数据源 (SSOT)”而存在，这也意味着，每个应用将**仅仅包含一个** **store** 实例。

##### 在组件中获取Vuex状态

在Vue实例中注册 ***store*** 

——通过在根实例中注册 `store` 选项，该 store 实例会 **注入到根组件下的所有子组件中** ，且子组件能通过 `this.$store` 访问到。

```js
const app = new Vue({
  el: '#app',
  // 把 store 对象提供给 “store” 选项，这可以把 store 的实例注入所有的子组件
  store,
  components: { Counter },
  template: `
    <div class="app">
      <counter></counter>
    </div>
  `
})
```

##### mapState辅助函数

当需要获取多个状态时，可以使用mapState辅助函数帮助我们生成计算属性。

```js
import { mapState } from 'vuex'
export default {
  computed: mapState({
      //...
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```

当映射的计算属性的名称与 state 的子节点名称相同时，我们也可以给 `mapState` 传一个字符串数组。

```js
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
```

##### 对象展开运算符

`mapState` 函数返回的是一个对象。利用 **对象展开运算符** 将它与局部计算属性混合使用

```js
computed:{
    countLocal(){return '局部计算属性'},
        ...mapState(
            ['count','count1','count2','count3']
        )
}
```



### Getters

——有时候，我们需要从store中获取一些state变异后的状态（可以认为是 store 的计算属性）,就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。

通过属性访问 getters ，   ***$store.getters.属性***   例如：`$store.getters.doneTodos` 

##### Getter 接受 state 作为其第一个参数

```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false } ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```

##### Getter 也可以接受其他 getter 作为第二个参数

```js
getters: {
 doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  doneTodosCount: (state, getters) => { 
      // 接受getters作为地各个参数，获取到  doneTodos 的返回值
    return getters.doneTodos.length
  }
}
```

##### 通过方法访问

`让 getter 返回一个函数，来实现给 getter 传参` 

```js
getters: {
  // ...
  getTodoById: (state) => (id) => {   //使用 箭头函数
    return state.todos.find(todo => todo.id === id)
  }
  getTodoByAge(state){
      return function(age){
          return state.todos.filter(s=> s.age > age)
      }
  }
}
```

```html
<template>
	<h2> 通过方法访问：{{$store.getters.getTodoById(2)}}   </h2>
</template>
```



##### `mapGetters` 辅助函数

`mapGetters` 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性：

```js
computed:{
    //使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
        'doneTodosCount',
      'anotherGetter',
        //...
    ])
}
```

将 `mapGetters`属性另取一个名字，则使用对象形式：

```js
computed:{
    ...mapGetters({
        // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  		doneCount: 'doneTodosCount'
    })
}
```



### Mutation

——更改 Vuex 的 store 中的状态的**唯一方法**是提交 **mutation**。

nMutation主要包括两部分：

1. 字符串的 **事件类型（type）** 
2. 一个**回调函数（handler）** ,该回调函数的第一个参数就是state

通过  `store.commit` 方法唤醒mutation handler

```js
//mutation的定义方式
mutations: {
    increment(state){
        state.count++
    }
}
//通过 store.commit 唤醒mutztions中的incremen
methdos:{
    increment(){
        this.$store.commit('increment'),
    }
}
```



##### 提交载荷（payload）

可以向 `store.commit`传入额外的参数，即 mutation 的 **载荷（payload）**：

```js
store.commit('increment',10)
```

```js
mutations:{
    increment(state,n){
		state.count +=n
    }
}
```

大多数情况下，载荷(payload)应该是一个对象,可以包含多个字段

```js
store.commit('increment',{
    num: 10,
    amount: 100 
})
```

```js
mutations:{
    increment(state,payload){
		state.count +=payload.amount
    }
}
```

##### 对象风格的提交方式

提交 mutation 的另一种方式是直接使用包含 `type` 属性的对象：

```js
store.commit({
  type: 'increment',
  amount: 10
})
```

当使用对象风格的提交方式，整个对象都作为载荷传给 mutation 函数，因此 handler 保持不变：

```js
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```



##### Mutation响应式规则

Vuex的store中的state是响应式的, 当state中的数据发生改变时, Vue组件会自动更新.

- 这就要求我们必须遵守一些Vuex对应的规则:

  1. 提前在store中初始化好所需的属性.	

  2. 当给state中的对象添加新属性时, 使用下面的方式:

     1.  使用Vue.set(obj, 'newProp', 123)

     2.  用新对象给旧对象重新赋值

        `注: Vue.set()添加属性，Vue.delete()删除属性` 

        ```js
        // Vue.set(要修改的对象, 索引值, 修改后的值)
        // Vue.delete(要删除的对象,索引值)
        ```

##### 使用常量替代 Mutation 事件类型

建立一个 `mutation-type.js` 文件

```js
// mutation-types.js
export const SOME_MUTATION = 'SOME_MUTATION'
```

```js
// store.js
import Vuex from 'vuex'
import { SOME_MUTATION } from './mutation-types'

const store = new Vuex.Store({
  state: { ... },
  mutations: {
    // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名
    [SOME_MUTATION] (state) {
      // mutate state
    }
  }
})
```

```js
// 组件里面
import { SOME_MUTATION } from './store/mutation-types'
export default {
  name: 'App',
  //...
  methods:{
    addClick(){
      this.$store.commit(SOME_MUTATION)  //直接使用常量
    }
  }
}
```



##### Mutation 必须是同步函数

在 Vuex 中，**mutation 都是同步事务**：

```js
store.commit('increment')
// 任何由 "increment" 导致的状态变更都应该在此刻完成。
```



### Action

Action 类似于 mutation，不同在于：

- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。

在组件中通过 `this.$store.dispatch('xxx')` 分发 action，

`Action 函数接受一个 context 对象，因此你可以调用 context.commit 提交一个 mutation，或者通过 context.state 和 context.getters 来获取 state 和 getters。`

```js
actions: {
    increment (context) {
      context.commit('increment')
    }
  }
```

实践中，我们会经常用到 ES2015 的 参数解构 来简化代码（特别是我们需要调用 `commit` 很多次的时候）：

```js
actions: {
    increment ({commit}) {
      commit('increment')
    }
  }
```

Action 通过 `store.dispatch` 方法触发：

```js
store.dispatch('increment')
```

在 action 内部执行**异步**操作：

```js
actions: {
    increment ({commit}) {
      setTimeout(()=>{
          commit('increment')
      },1000)
    }
  }
```

##### Actions 支持同样的载荷方式和对象方式进行分发：

```js
// 以载荷(payload)形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```

##### mapActions辅助函数

```js
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
        // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`
      'increment', 
        
      // `mapActions` 也支持载荷：
	// 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
      'incrementBy' 
    ]),
    ...mapActions({
        // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
      add: 'increment' 
    })
  }
}
```



##### Action返回Promise

Action 通常是异步的，`store.dispatch` 可以处理被触发的 action 的处理函数返回的 Promise，并且 `store.dispatch` 仍旧返回 Promise：

```js
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  }
}
```

```js
//使用返回的 Promise
this.$store.dispatch('actionA').then(()=>{ //... })
```

一个 `store.dispatch` 在不同模块中可以触发多个 action 函数。在这种情况下，只有当所有触发函数完成后，返回的 Promise 才会执行。



### Modules

Vuex 允许我们将 store 分割成**模块（module）**。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：

```js
const moduleA = { //模块A
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}
const moduleB = { //模块B
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})
```

通过 store.state.a 获取 模块A 和 模块B

```js
store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```

#### 模块的局部状态

- 对于模块内部的 **`mutation`** 和 **`getter`**，接收的第一个参数是 **模块的局部状态对象**。
- 对于模块内部的 **`action`**，局部状态通过 `context.state` 暴露出来，根节点状态则为 `context.rootState`。
- 对于模块内部的 **`getter`**，根节点状态会作为第三个参数暴露出来：

```js
//模块内的 mutation			
	this.$store.commit('属性名'[,'可选参数'])
//模块内的 getter
 	this.$store.getters.属性名
//模块内的 action
    this.$store.dispatch('属性名'[,'可选参数'])
```

```js
actions: {
//模块内部的 action，局部状态通过 context.state 暴露出来，根节点状态则为context.rootState
    incrementIfOddOnRootSum ({ state, commit, rootState }) {
      if ((state.count + rootState.count) % 2 === 1) {
        commit('increment')
      }
    }
}
```



```js
getters: { //rootState 根节点状态 作为第三个参数
    sumWithRootCount (state, getters, rootState) {
      return state.count + rootState.count
    }
  }
```









## Vue CLI

使用前提：Node（8.9以上版本）、Webpack（  *npm install webpack -g*  ）

### Vue CLI的使用

- 安装      *npm install -g @vue/cli* （CLI3）

  1. 拉取2.x模板（旧版本）  *npm install -g @vue/cli-init* 

     - Vue CLI2初始化项目

       ​    		*vue init webpack my-project* (my-project 是项目名称) 

  2. Vue CLI3初始化项目

     ​					*vue create my-project* 
     
     ​					 *vue ui*  (可视化)
     
  3. 指定版本安装：

     - 查看所有版本号

     ```
     //3.x 和 4.x 的所有版本号
     npm view @vue/cli versions --json
     //1.x 和 2.x 的所有版本号
     npm view vue-cli versions --json
     ```

     - 安装	

       1. 安装 3.x 和 4.x 版本

          ```
          npm install -g @vue/cli@版本号
          ```

       2. 安装 ***1.x*** 和 ***2.x*** 版本

          ```
          npm install -g vue-cli@版本号
          ```

- 卸载     

  - npm uninstall -g @vue/cli（CLI3/4）
  - npm uninstall vue-cli -g  (CLI1/2)

### 自定义配置Vue脚手架

1. 在根目录创建 vue.config.js  文件

2. 在文件中进行相关配置，从而覆盖默认配置

   ```js
   module.exports = {
       devServer: {
           //自动打开浏览器
           open: true,
           port: "8800"
       }
   }
   ```

   

### Runtime-Compiler和Runtime-only的区别

- 如果在之后的开发中，你依然使用template，就需要选择Runtime-Compiler

- 如果你之后的开发中，使用的是.vue文件夹开发，那么可以选择Runtime-only

  - Runtime-only	——性能更高，代码量少

    ```js
    new Vue({
      el: '#app',
      render: h => h(App)
    })
    // render -> vdom(虚拟Dom) -> UI
    ```

  - Runtime-Compiler

    ```js
    new Vue({
      el: '#app',
      components: { App },
      template: '<App/>'
    })
    // template -> ast(抽象语法树) -> render -> vdom(虚拟Dom) -> UI
    ```

  - render函数的使用

    ```js
    //render 函数的使用
    // 方式一：renter createElement('标签','相关数据对象(可以不传)','内容数组')
    renter createElement('div',{ class:'box' },['你好']); //基本使用
    renter createElement('div',{class:'box'},['你好',centerElement('h2',['标题'])]);//嵌套render函数
    ```

    ```js
    //方式二：传入一个组件对象
    render (createElement)=>{ return createrElement(cpn) } // cpn是组件
    ```

    


## Webpack

​	——模块打包工具

### 基础介绍

#### 前端模块化

- webpack其中一个核心就是让我们可能进行模块化开发，并且会帮助我们处理模块间的依赖关系；
- 不仅仅是JavaScript文件，我们的CSS、图片、json文件等等在webpack中都可以被当做模块来使用。

#### 打包

- 将webpack中的各种资源模块进行打包合并成一个或多个包(Bundle)；
- 并且在打包的过程中，还可以对资源进行处理，比如压缩图片，将scss转成css，将ES6语法转成ES5语法，将TypeScript转成JavaScript等等操作。

#### 模板工程

```
* build   --webpack设置文件夹
* config  --工程设置文件
* src     --源文件夹
* static  --静态文件夹
* index.html  --网页入口文件
```



#### 与Gulp的对比

1. gulp的核心是Task；
2. 我们可以配置一系列的task，并且定义task要处理的事务（例如ES6、ts转化，图片压缩，scss转成css），之后让grunt/gulp来依次执行这些task，而且让整个流程自动化，所以grunt/gulp也被称为前端自动化任务管理工具。

Gulp和webpack的不同

- grunt/gulp更加强调的是前端流程的自动化，模块化不是它的核心；
- webpack更加强调模块化开发管理，而文件压缩合并、预处理等功能，是他附带的功能。

### webpack安装

1. 需要安装 node.js		查看node版本：node -v
2. 全局安装webpack       安装命令：npm install webpack@3.6.0 -g
3. 局部安装                     安装命令：npm install webpack@3.6.0 --save-dev

### webpack配置

- package.json： npm包管理的文件      生成命令：npm init

- 入口和出口

  1. 创建一个  webpack.config.js  文件

     ```js
     const path = require('path')
     module.exports = {
         //入口
         entry: './src/main.js',
         //出口，通常是一个对象，至少包含两个属性，path和filename
         output: {
             path: path.resolve(__dirname, 'dist'),//path是一个绝对路径
             filename: 'bundle.js'
         }
     }
     ```

- 在 package.json 中定义启动

  1. 在 **scripts** 中定义自己的执行脚本
  2. 运行命令  npm run build   （build是自己定义的）
  3. srcipts 脚本执行时有顺序：
     1. 首先，会寻找本地的node_modules/.bin路径中对应的命令。
     2. 如果没有找到，会去全局的环境变量中寻找。

  ```json
  {
      "name": "meetwebpack",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
          "test": "echo \"Error: no test specified\" && exit 1",
          "build": "webpack"
      },
      "author": "",
      "license": "ISC",
      "devDependencies": {
          "webpack": "^3.6.0"
      }
  }
  ```

  

### loader

—— loader 是webpack中一个非常核心的概念。

#### loader使用过程

1. 通过npm安装需要使用的 loader
2. 在webpack.config.js中的 module 关键字下进行配置

#### css文件处理

- 安装  style-loader、css-loader

- 配置

  ```js
  module: {
      rules: [{
          test: /\.css$/,
          // css-loader只负责将css文件进行加载
          // style-loader负责将样式添加到DOM中
          // 使用多个loader时, webpazk是从右向左加载的
          use: ['style-loader', 'css-loader']
      }]
  }
  ```

#### less文件处理

- 安装  less-loader

- 配置

  ```js
  module: {
      rules: [
          {
              test: /\.less$/i,
              use: [{
                  loader: "style-loader", 
              }, {
                  loader: "css-loader" 
              }, {
                  loader: "less-loader", 
              }]
          }
      ]
  }
  ```

#### 图片资源

- 安装 url-loader、file-loader

- 配置

  ```js
  module: {
      rules: [
          {
              test: /\.(png|jpg|gif)$/i,
              use: [{
                  loader: 'url-loader',
                  options: {
  // 当加载的图片, 小于limit时, 会将图片编译成base64字符串形式.
  // 当加载的图片, 大于limit时, 需要使用file-loader模块进行加载.
  // 大于limit时，还需要再 路径下添加 dist/
                      limit: 8196,
                      name: 'img/[name].[hash:8].[ext]'
                  }
              } ],
          },
      ]
  }
  ```

  ```js
  // 出口
  output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'bundle.js',
  // 添加 dist/路径
      publicPath: 'dist/'
  },
  ```

#### ES6语法处理

- 安装	babel

  ​	npm install --save-dev babel-loader@7 babel-core babel-preset-es2015

  ​	现在直接安装es2015（以后根据需求安装不同的 env）

- 配置

  ```js
  module: {
      rules: [
          {
              test: /\.m?js$/,
              exclude: /(node_modules|bower_components)/,
              use: {
                  loader: 'babel-loader',
                  options: {
                      presets: ['es2015'] 
                      //presets: ['@babel/preset-env']
                  }
              }
          }
      ]
  }
  ```

### 引入Vue.js

安装Vue——  npm install vue --save
主：因为我们后续是在实际项目中也会使用vue的，所以并不是开发时依赖（不加-dev）

出现 runtime-only 版本错误时，需要修改 webpack配置

- runtime-only
- runtime-compiler

```js
module.exports = {
// 在module.export 添加 resolve
    resolve: {
        //alias: 别名
        alias: {
            'vue$': 'vue/dist/vue.esm.js'
        }
    }
}
```

el 和 template 的区别：

1. el 用于指定Vue要管理的DOM，可以帮助解析其中的指令、事件监听等等；
2. template模板的内容会替换掉挂载的对应el的模板

#### Vue组件化开发

安装：vue-loader以及vue-template-compiler

​	 *npm install vue-loader vue-template-compiler --save-dev* 

​	修改webpack配置

```js
module: {
    rules: [
        {
            test: /\.vue$/,
            use: {
                loader: "vue-loader"
            }
        }
    ]
}
```

### plugin

—— **plugin** 是插件的意思，通常是用于对某个现有的架构进行扩展

webpack中的插件，就是对webpack现有功能的各种扩展，比如打包优化，文件压缩等等。

- loader和plugin区别
  1. loader主要用于转换某些类型的模块，它是一个转换器；
  2. plugin是插件，它是对webpack本身的扩展，是一个扩展器。
- plugin的使用过程
  1. 通过npm安装需要使用的plugins(某些webpack已经内置的插件不需要安装)；
  2. 在webpack.config.js中的plugins中配置插件。

#### 需要添加的插件

##### 添加版权的Plugin

```js
//导入webpack
const webpack = require('webpack')
moduleexports = {
 	...
    plugins:[
        new webpack.BannerPlugin('最终版权归 Li Hao 所有')
    ]
}
```

##### 打包html的plugin

安装 HtmlWebpackPlugin 插件

​	 *npm install html-webpack-plugin --save-dev* 

```js
//导入 HtmlWebpackPlugin 
const HtmlWebpackPlugin = require('html-webpack-plugin');
moduleexports = {
 	...
    plugins:[
        // 传入一个参数 作为模板
        new HtmlWebpackPlugin({ template: 'index.html' })
    ]
}
```

##### js压缩的plugin

安装  uglifyjs-webpack-plugin  插件

​	 *npm install uglifyjs-webpack-plugin --save-dev* 

```js
//导入 uglifyjs-webpack-plugin
const uglifyjswebpackPlugin = require('uglifyjs-webpack-plugin');
moduleexports = {
 	...
    plugins:[
        new uglifyjswebpackPlugin()
    ]
}
```



### 搭建本地服务器

 *webpack提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用express框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果* 

安装： *npm install --save-dev webpack-dev-server@2.9.1* 

- devserver也是作为webpack中的一个选项，选项本身可以设置如下属性：
- contentBase：为哪一个文件夹提供本地服务，默认是根文件夹，我们这里要填写./dist
- port：端口号（不写会默认8080端口）
- inline：页面实时刷新
- historyApiFallback：在SPA页面中，依赖HTML5的history模式

```js
module.exports = {
	...
    devServer: {
        contentBase: '/dist', //指定文件夹（为哪个文件夹提供服务）
        inline: true, // 页面实时刷新
    }
}
```

在package.json中配置：

```json
{
    "name": "meetwebpack",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
         //配置 脚本 （只需要执行 npm run dev）
        "dev": "webpack-dev-server --open"  
    },
}
```





## 前端模块化

常见的模块化规范：

1. CommonJS
2. AMD
3. CMD
4. ES6的Modules

### CommomJS(了解)

1. 导出     model.exports

   ```js
   model.exports = { flag:true,sun；function(){return 'sun'} }
   ```

2. 导入     require

   ```js
   var {flag , sun} = require('路径');
   ```

### ES6的Modules

1. 导出

   - export	(同一个模块中可以有多个，)

     ```js
     // 第一种导出方式
     export let name = '李四';
     export let age = 18;
     // 第二种导出方式
     let name = '李四';
     let age = 18;
     export {name,age}
     // 还可以出函数或类
     export function fun(){ console.log('函数') }
     export class Person{ constructor(name,age){ 
         this.name = name;
       this.age = age; } }
     // 或者
     function fun(){ console.log('函数') }
     class Person{ constructor(name,age){ 
         this.name = name;
         this.age = age; } }
     export { fun,Person }
     ```
     
   - export default    (在同一个模块中只能有一个，导入者可以自己命名 )

     ```js
     // 方式一
     export default function () {console.log('default function') }
     //方式二
     function fun() {console.log('default function') }
     export default fun;
     ```

     

2. 导入

   - import		

     ```html
     <!-- 首先，在HTML代码中引入的文件，类型必须设置为 module -->
     <script src="info.js" type="module"></script>
     <script src="main.js" type="module"></script>
     ```

     ``` js
     import {name,age,height} from "./info,js"
     ```

     ```js
     // 通过 * 可以导入模块中的所有变量，通常需要起一个别名
     // 使用时 别名.变量明
     import * as info form "./info.js"
     console.log(info.name, info.age, info.height)
     ```




## 使用Ajax库—axios

### axios

安装：  `npm install --save --save-exact axios vue-axios  ` 

支持多种请求方式：

- axios(config)
- axios.request(config)
- axios.get(url[, config])
- axios.delete(url[, config])
- axios.head(url[, config])
- axios.post(url[, data[, config]])
- axios.put(url[, data[, config]])
- axios.patch(url[, data[, config]])

```js
axios({
    url: 'http://123.207.32.32:8000/home/data',
    //params 专门针对get请求参数拼接
    params: {
        type: 'pop',
        page: 1
    }
}).then(res => {
    console.log(res);
})
```

发送并发请求：

- 使用axios.all, 可以放入多个请求的数组
- axios.all([]) 返回的结果是一个数组，使用 axios.spread 可将数组 [res1,res2] 展开为 res1, res2

```js
axios.all([axios({
        url: 'http://123.207.32.32:8000/home/multidata'
    }), axios({
        url: 'http://123.207.32.32:8000/home/data',
        params: {
            type: 'sell',
            page: 5
        }
    })])
    .then(axios.spread((res1, res2) => {
        console.log(res1);
        console.log(res2);
    }))
```

### 全局配置

例如：

```js
axios.defaults.baseURL = ‘123.207.32.32:8000’
axios.defaults.headers.post[‘Content-Type’] = ‘application/x-www-form-urlencoded’;
```

### 拦截器

- axios提供了拦截器，用于我们在发送每次请求或者得到相应后，进行对应的处理。
  - 请求：成功/失败
  - 响应：成功/失败

请求拦截

```js
//请求拦截
instance.interceptors.request.use(config => {
    // console.log(config.url);
    //将拦截到的 数据config 返回出去
    return config
}, err => {
    console.log(err);
})
```

响应拦截

```js
// 响应拦截
instance.interceptors.response.use(res => {
    //将拦截的数据 返回出去
	return res.data
}, err => {
console.log(err);
})
```



## 引入一些框架

1. 引入bootstrap4
   1. vue-webpack中导入bootstrap4框架   npm install bootstarp --save --save-exact
   2. 在main.js中引入    import 'bootstrap/dist/css/bootstrap.min.css'
   3. 测试BootStrap功能，引入成功

2. 引入Element-UI

   1. 安装依赖包： npm install element-ui -s

   2. 导入相关资源：

      ```js
      //手动配置 element-ui
      import ElementUI from 'element-ui' //导入组件库
      import 'element-ui/lib/theme-chalk/index.css' //导入组件相关样式
      Vue.use(ElementUI);
      ```

      



## 组件库

1. vue-chartjs

   Chart.js库的vue实现，可以完成网页中的图表显示。https://vue-chartjs.org/
   演示：http://demo.vue-chartjs.org/
   
2. vue-fa

   FontAwesome5库的vue实现，可以调用FontAwesome5的各种组件。

   https://cweili.github.io/vue-fa/

3. vee-validate

   基于模板的vue校验框架。

   https://baianat.github.io/vee-validate/

4. eslint-plugin-vue

   vue的文法校验工具，可以快速找出代码、指令、样式单中的问题，同时还可以集成到VSCode, Sublime, Atom等IDE中。

   https://eslint.vuejs.org/

5. vue-lazyload

   图片懒装载处理组件。

   https://github.com/hilongjw/vue-lazyload

6. axios

   HTTP通信组件，可以远程存取各种REST-API服务。

   https://github.com/axios/axios

7. vuedraggable

   网页对象拖动组件，只需写少量的代码，就可以完成页面对象的拖动排序。

   https://github.com/SortableJS/Vue.Draggable
   演示: https://sortablejs.github.io/Vue.Draggable/#/simple

8. Vue-Socket.io

   对于socket.io库的封装，可以和Vuex状态管理配合使用。

   https://github.com/MetinSeylan/Vue-Socket.io

9. Vue-multiselect

   多选框的解决方案，还包括状态管理、下拉框、Ajax、检索框等功能。

   https://vue-multiselect.js.org/

10. vuejs-datepicker

    vue的日期选择组件。

    https://github.com/charliekassel/vuejs-datepicker

11. vue-md-editor

    vue的markdown编辑器。

    https://github.com/anguer/vue-editor

12. vue-typer

    内容显示的打字机组件。https://github.com/cngu/vue-typer
    演示：https://cngu.github.io/vue-typer/

13. vue-rate-it

    五星评价组件，省的自己编写了。https://craigh411.github.io/vue-rate-it/
    演示：https://jsfiddle.net/craig_h_411/992o7cq5/

14. Vue-good-table
    vue的表格操作组件，支持列排序、内容过滤、分页等操作。
    https://xaksis.github.io/vue-good-table/

15. Vuex

16. Vue-Router

17. Vuetify

    vue的UI/UX框架，除Bootstrap外的选择。

    https://vuetifyjs.com/

18. element-ui

    基于vue 2.0的组件库，同时支持React和Angular。

    http://element.eleme.io/

19. vue-material

    Google设计风格的UI组件库。

    https://vuematerial.io/

20. bootstrap-vue

    Bootstrap的vue组件库，好用没有之一。

    https://bootstrap-vue.js.org/

21. Nuxt.js

    Vue的服务器端渲染框架，解决客户端渲染的诸多问题。（首页载入慢，SEO等）

    https://nuxtjs.org/



