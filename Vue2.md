## vue2.x

MVVM模型：

- M：模型(Model)			data中的数据
- V：视图(View)             模板代码
- VM：视图模型(ViewModel)   Vue实例

### 基础语法

#### 插值

​	`{{}}` 

#### 指令(内置指令)

1. v-bind：单向数据绑定

2. v-model：双向数据绑定
  - v-model:value简写为：v-model

3. v-for：遍历数组/对象/字符串（通常添加 `key` 属性）

4. v-if/v-else-if/v-else：控制节点是否渲染

5. v-show：控制节点是否显示

6. v-text：向其所在的节点中渲染文本内容

   - 与插值语法的区别是`v-text`会替换掉节点中的内容，{{xx}}则不会

7. v-html：向指定节点中渲染包含html结构的内容

   - 可以识别html结构，有安全问题，容易导致XXS攻击

8. v-clock：是一个特殊的属性（没有值），Vue实例创建完毕并接管容器，会删掉`v-clock`属性

   - 使用 css 配合 `v-clock`可以解决网速满时页面展示问题

   - ```html
     <style>
         [v-cloak] {
         display: none;
         }
     </style>
     ```

9. v-once：只编译一次，显示内容之后不再具有响应式功能

10. v-pre：直接显示原始信息，跳过编译过程

11. v-on：@

   - 事件修饰符：(可以连写)
     1. `prevent`：阻止默认事件
     2. `native`：原生事件
     3. `stop`：阻止事件冒泡
     4. `once`：事件只触发一次
     5. `capture`：使用事件的捕获模式
     6. `self`：只有event.target是当前操作的元素时才触发事件
     7. `passive`：事件的默认行为立即执行，无需等待事件回调执行完毕
     
   - 键盘事件 `@keyup`  `@keydown`

     - vue中常用按键别名：

       > 1. 回车 => enter
       > 2. 删除 => delete （捕获“删除”和“退格”）
       > 3. 退出 => esc
       > 4. 空格 => space
       > 5. 换行 => tab （特殊与 `keydown` 配合使用）
       > 6. 上、下、左、右 => up、down、left、right
       > 7. 系统修饰键：ctrl、alt、shift、meta(win键)
       >    - 配合 `keyup`使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。
       >    - 配合`keydown`使用：正常触发事件。
       > 8. 自定义键名：Vue.config.keyCodes.自定义键名 = 键码

   - 滚动事件

     - `@scroll`：滚动条滚动

     - `@wheel`：鼠标滚轮滚动

`el`两种写法：

```js
new Vue({
    el:'#root'
})
```

```js
const vm = new Vue({})
vm.$mount('#root')
```



#### 计算属性

> - 底层借助了`Object.defineproperty()` 方法提供的getter() 和 setter()
> - 比 methods 相比内部有缓存机制，效率高；计算属性不能开启异步任务
> - 如果计算属性要被修改，则必须写set()去相应修改，且set()中要引起计算时依赖的数据发生变化
> - `set()`：初次读取计算属性时，所依赖的数据发生变化时
> - `get()`：set()被调用的时机 当fullName被修改时
>
> ```js
> // 完整写法
> computed: {
> 	fullName: {
>         get() {},
>         set(value) {}
> }
> ```
>
> ```js
> // 简写
> // function(){} 相当于 set() 函数
> getName: function() {}
> ```
>
> 

#### 监听属性

> 1. 被监听的属性发生变化时，回调函数自动调用；
>
> 2. 监听的属性必须存在；
>
> 3. 两种写法：
>
>    1. 在`watch`中配置
>    2. 通过`Vue`实例配置
>
> 4. 监听属性的配置项
>
>    - `immediate:true`  // 初始化时直接调用
>    - `handler(newval,oldval){}` // 
>    - `deep:true` // 开启深度监听（Vue的`watch`默认不监听对象内部值的改变，需手动配置`deep`）
>
> 5. 当`watch`中只有`handler(){}`时可以简写，如下：
>
>    ```js
>    const vm = new Vue({
>        el: '#root',
>        data: {
>            isHot: true
>        },
>        watch: {
>            isHot(newVal, oldVal){
>                console.log("被修改了！")
>            },
>        }
>    })
>    vm.$watch('isHot',function(newVal, oldVal){            console.log("被修改了！")
>    })
>    ```
>
>    
>
> ```js
> /* 完整写法 */
> const vm = new Vue({
>     el: '#root',
>     data: {
>         isHot: true
>     },
>     watch: {
>         isHot: {
>             immediate: true, // 初始化时直接调用
>             handler(newVal, oldVal) {
>                 console.log("被修改了！")
>             }
>         },
>     }
> })
> vm.$watch('isHot',{
>     immediate: true, // 初始化时直接调用
>     handler(newVal, oldVal) {
>         console.log("被修改了！")
>     	}
>     }
> })
> ```
>
> 

#### 过滤器

> 主要用于格式化数据
>
> 1. 局部过滤器
>
>    - ```js
>      var vm = new Vue({
>          el:'#root',
>          data:{ msg:'123456' },
>          filters:{
>              upper(val, args='默认值'){
>                  // 过滤器的逻辑
>                  // args是过滤器的参数，从第二个参数进行接受
>                  // args='默认值'：通过 ES6语法设置默认值
>              }
>          }
>      })
>      ```
>
>      
>
> 2. 全局过滤器
>
>    - ```js
>      Vue.filter('lower',function(val,args){
>          // 过滤器的逻辑
>      })
>      ```
>
>      
>
> 3. 过滤器的使用
>
>    - ```html
>      <div> {{ msg | upper}} </div> <!-- 通过 | 管道符 在插值表达式中使用 -->
>      <div> {{ msg | upper | lower}} </div> <!-- 支持级联操作 -->
>      <div :abc="msg | upper"> 测试数据 </div> <!-- 在属性绑定中使用 -->
>      ```
>

#### 自定义指令

> 1. 全局指令
>    - `Vue.directive(‘指令名’,配置对象)`或`Vue.directive(‘指令名’,回调函数)`
> 2. 局部指令
>    - `new Vue({directives:{ '指令名':配置对象 } })`或
>      `new Vue({ directives:{ '指令名':回调函数 } })`
> 3. 配置对象中常用3个的回调
>    1. `bind()`：指令与元素成功绑定时调用
>    2. `inserted()`：指令所在的元素被插入页面时调用
>    3. `update()`：指令所在模板结构被重新解析式调用
> 4. 注意
>    - 指令定义时不加 `v-`，使用时加 `v-`
>    - 指令必须用短横线`-`分隔，不能用驼峰命名法，`className`改为`class-name`



#### 生命周期

> **`beforeCreate`**：无法通过vm访问到data中的数据、methods中的方法；
>
> **`created`**：可以访问 `this`（访问vm中到data中的数据、methods中的方法）；
>
> **`beforeMount`**：页面呈现的是未经Vue编译的DOM结构，所有对DOM的操作没有作用；
>
> **`mounted`**：页面呈现的是Vue编译过的DOM，一般在此过程中进行：开启定时器、网络请求、订阅消息、绑定自定义事件等**初始化操作**；
>
> **`beforeUpdata`**：数据更新了，但页面没有更新。页面尚未和数据保持同步。
>
> 1. 根据更新的数据，生成新的虚拟DOM进行，最终完成页面更新，
>
>    即：完成了Model ----> View 的更新
>
> **`updataed`**：数据是新的，页面也是新的，页面和数据保持同步。
>
> 1. 调用 `vm.$destroy`后触发 `beforeDestory`和`destroyed`
>
> **`beforeDestroy`**：此时vm中所有数据都可用，但是马上要执行销毁过程了，一般在此阶段：关闭定时器、取消订阅消息、解绑自定义事件等收尾工作。
>
> **`destroyed`**：销毁实例了。
>
> 1. 销毁Vue实例：
>    - 销毁后借助Vue开发者工具看不到任何消息；
>    - 销毁后自定义事件会失效，但原生DOM事件依然有效；
>    - 一般不会再`beforeDestroy`操作数据，因为即便操作数据，也不会再触发更新页面流程了。
> 2. `this.$destroy()`销毁当前组件的实例，销毁后所有实例的自定义事件全部失效
>
> **`activeed`**：路由组件被激活时触发
>
> **`deactived`**：路由组件失活时触发





**`Object.defineProperty()`**

> 给对象添加属性
>
> 参数：
>
> 1. 对象
>
> 2. 属性名
>
> 3. {
>
>    value // 属性值
>    enumerable // 控制属性是否可以修改，默认为false
>    writable // 控制属性是否可以修改，默认为false
>    configurable // 控制属性是否可以被删除，默认为false
>
>    // 当读取 person的age属性时，get函数(getter)会被调用，且返回的值就是age的
>    get(){} 
>
>    //当修改person的age属性时，set函数(setter)会被调用，且收到修改的具体值
>    set(value){}
>
>    }



### 组件化

#### 非单文件组件

`<school></school>`组件本质是 VueComponent的构造函数，由`Vue.extend()`生成的。

只需要注册组件，并使用`<school></school>`，Vue解析时会帮我们创建school组件的实例对象，即`new VueComponent(options)`

每调用`Vue.ectend()`，则返回全新的`VueComponent()`。

关于this指向：

1. 组件中 `this`均是 `VueComponent`的实例对象
2. `new Vue()`中是`Vue`实例对象

内置关系：
 VueComponent.prototype.__proto__  ===  Vue.prototype
好处：让组件实例对象可以访问到原型上的属性和方法。

#### 单文件组件

1. `Vue.js`与`vue.runtime.xxx.js`的区别
   - `vue.js`是完整版本，包含：核心功能+模板解析器
   - `vue.runtime.xxx.js`是运行版本的Vue，只包含：核心功能，没有模板解析器；vueCLI默认引入此版本，所以不能使用`template`配置项，需要使用`render`函数接收`createElement`函数去指定具体内容。
2. `render`函数



### Vue CLI 

**`Vue脚手架`**·

#### ref

> 1. 被用来给元素或子组件注册引用信息（id的替代者）
> 2. 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象
> 3. 使用方式：
>    - 写 `ref` 属性：`<h1 ref="xxx"></h1>`
>    - 获取：**`this.$refs.xxx`**

#### props

> 1. 组件接受父组件传来的数据
>
> 2. `props`是只读的，Vue不建议修改props中的数据，修改后会发出警告
>
> 3. 接收方式：
>
>    - 只接收：`props:['name']`
>
>    - 限制类型：`props:{name:String}`
>
>    - 限制类型+限制必要性+指定默认值：
>
>      `props:{name:{type:String,required:true,default:'老王'}}`

#### mixin

> 1. 可以把多个组件公用的配置提取成一个混入对象
> 2. 使用`mixin`
>    - 定义：{ data(){...}, methods:{...} }
>    - 使用：
>      1. 全局混入：Vue.mixin(...)
>      2. 局部混入：mixins:[ ...]

#### 插件

> 1. 用于增强`Vue`
>
> 2. 包含`install()`的一个对象，`install`的第一个参数是Vue，第二个及之后的参数是插件使用者传递的数据
>
> 3. 定义插件：
>
>    - ```js
>      {
>      	install( Vue ) {
>      		Vue.filter()
>      		Vue.directive()
>      		Vue.mixin()
>      		Vue.prototype.$myMethods = function(){}
>      	}
>                                                                                                                    
>      }
>      ```

#### scoped

> 1. 让`style`样式在局部生效，防止冲突。
>
> 2. 写法
>
>    ```vue
>    <style scoped lang="less">
>        .demo{ font-size:14px; }
>    </style>
>    ```
>
>    



#### 组件的自定义事件

> 1. 子组件给父组件传值；
> 2. 子组件用 `this.$emit()`触发事件
> 3. 父组件绑定事件
>    1. 通过 `v-on` 或 `@`监听子组件的事件
>    2. 通过 `ref`，绑定事件，`this.$refs.ref数据.$on('事件名称',回调)` 
> 4. 子组件触发事件
>    1. `this.$emit('事件名',参数)`
> 5. 解除自定义事件
>    - `this.$off()`  解绑所有的自定义事件；
>    - `this.$off('事件名')`  解绑指定自定义事件；
>    - `this.$off(['事件名','事件名'])` 解绑多个自定义事件，参数是数组；
> 6. 组件绑定原生DOM事件，需要使用`native`修饰符；
> 7. 通过`this.$refs.xxx.$on('事件名'，回调)`绑定自定义事件，**回调**要么配置在`methods`中，要么使用`箭头函数`，否则 `this`指向出现问题（指向`ref`所指的组件）

#### 全局事件总线

​	——**任意组件之间通信**

> 1. 安装全局事件总线
>
>    ```js
>    new Vue({
>    	// ...
>    	beforeCreate(){
>    	// 安装全局事件总线
>    		Vue.prototype.$bus = this	
>    	}
>    })
>    ```
>
> 2. 使用事件总线
>
>    1. 接收数据：子组件中给`$bus`绑定自定义事件，事件的回调函数在组件`methods`中；
>
>       ```vue
>       methods(){
>       	demo(data){}
>       }
>       mounted(){
>       	this.$bus.$on('xxx',this.demo) // 绑定自定义事件事件
>       }
>       ```
>
>    2. 提供数据：this.$bus.$emit( ' xxx' , data)
>
> 3. 在`beforeDestroy()`钩子中用`this.$off('xxx')`解绑当前组件所用到的事件。



#### 消息订阅与发布(pubsub)

> 1. 一种组件间通信的方式，适用于**任意组件间通信**；
>
> 2. 使用步骤：
>
>    1. 安装`pubsub-js`：`npm install pubsub-js`
>
>    2. 引入 `import pubsub from 'pubsub-js'`
>
>    3. 接收数据： 
>
>       ```js
>       methods(){
>           // 第一个数据name 为消息名称，第二个为数据
>           demo(name，data){...}
>       }
>       mounted(){
>           // 订阅消息
>           this.pid =  pubsub.subscribe('xxx',this.demo) 
>       }
>       ```
>
>    4. 提供数据：`pubsub.publish('xxx',数据)` 发送消息
>
>    5. 在`beforeDestroy()`钩子中，用`pubsub.unsubscribe(this.pid)`取消订阅



#### `$nextTick`

> 在下一次DOM更新结束后执行指定的回调，（将回调延迟到下次 DOM 更新循环之后执行）
>
> 当没有回调且在支持`Promise`的环境中使用则返回一个`promise`,
>
> ```js
> Vue.$nextTick(callback)
> 
> Vue.$nextTick()
> 	.then(function(){
>     	// DOM更新了	
> 	})
> ```



#### 过度与动画

> 作用：在插入、更新、或移除DOM元素时，在合适的时候给元素添加样式类名

> 将元素包含在`transitin`组件中`Vue`会自动在恰当时机添加`css过度/动画`类名（如果应用了）
>
> 在进入/离开的过度中，会有6个class切换：
>
> 1. `v-enter`：**进入**过渡的开始状态
> 2. `v-enter-active`：**进入**过渡的生效状态
> 3. `v-enter-to`：**进入**过渡的结束状态
> 4. `v-leave`：**离开**过度的开始状态
> 5. `v-leave-active`：**离开**过渡的生效状态
> 6. `v-leave-to`：**离开**过度的结束状态
>
> 当`<transition></transition>`没有名字时，则`v-`是默认前缀；
>
> 有名字时`<transition name="my-transition"></transition>`，则会使用 `my-transition`作为前缀
>
> 当给多个元素配置过度/动画，则需要使用`<transition-group></transition-group>`，并且每一个都要配置**`key`** 
>
> `appear`属性为`true`时设置节点在初始渲染的过渡(刚开始的效果)



#### axios

> 
>
> **跨域**：协议、域名、端口不同
>
> 解决：
>
> 1. `cors`：后端解决
>
> 2. `jsonp`：`script`中`src`属性，只能解决 `GET`请求
>
> 3. `代理服务器`：
>
>    1. `nginx`
>
>    2. `vue-cli`
>
>       **vue脚手架配置代理**
>
>       1. 方法一
>
>          在`vue.config,js`中添加如下配置：
>
>          ```js
>          devServer:{
>              proxy:"http://localhost:5000"
>          }
>          ```
>
>          说明：
>
>          - 配置简单，请求资源时直接发给前端(8080)即可
>          - 不能配置多个代理，不能灵活控制请求是否走代理
>          - 会优先匹配前端资源（当8080端口有资源时则不会请求服务器）
>
>       2. 方法二
>
>          `vue.config.js`
>
>          ```js
>          module.exports = {
>              devServer:{
>                  proxy:{
>                      '/api':{ // 匹配所有以‘/api’开头的请求路径
>                          // 请求目标的基础路径
>                          target:'http://localhost:5000',
>                          // 控制请求头的 host 字段(是否显示正确端口)
>                          // 默认为 true
>                          changeOrigin:true,
>                         	// 取消前缀 '/api'
>                          pathRewrite:{'^/api':''},
>                          ws:true
>                      },
>                      '/demo':{
>                          target:'http://localhost:5001',
>                          changeOrigin:true,
>                          pathRewrite:{'/demo':''}
>                      }
>                  }
>              }
>          }
>          ```
>
>          说明：
>
>          - 可以配置多个代理，而且可以灵活控制请求是否走代理
>          - 请求资源时必须加前缀，配置略微繁琐



#### 插槽

1. 作用：让父组件可以向子组件指定的位置插入`html`结构，也是一种组件间的通信，适用于**父组件===>子组件**

2. 分类：默认插槽、具名插槽、作用域插槽

3. 使用

   - 默认插槽

     ```vue
     <!-- 父组件 -->
         <Categroy>
     		<div> html结构 </div>
         </Categroy>
     <!-- 子组件 -->
     	<template>
     		<div>
     			<slot> 默认插槽内容 </slot>
             </div>
     	</template>
     ```

   - 具名插槽

     ```vue
     <!-- 父组件 -->
         <Categroy>
     		<div slot="header"> 头部 </div>
     		<template slot='center'>
     			<div> 主体 </div>
     		</template>
     		<template v-slot:footer>
     			<div> 底部 </div>
     		</template>
         </Categroy>
     <!-- 子组件 -->
     	<template>
     		<div>
     			<slot name='header'> 默认插槽内容 </slot>
     			<slot name='center'> 默认插槽内容 </slot>
     			<slot name='footer'> 默认插槽内容 </slot>
             </div>
     	</template>
     ```

   - 作用域插槽

     - 数据在子组件自身，但根据数据成成的结构需要组件的使用者(父组件)决定

       - 父组件对子组件的数据进行加工处理

     - 父组件在`template`标签中使用`slot-scope`属性获取子组件传的数据(固定写法)

     - 子组件插槽中使用`v-bind`传数据

       ```vue
       <!-- 父组件 -->
           <Categroy>
       		<template slot-scope="data" slot="center">
       			<div> 
                       <!-- data为一个对象 -->
                   	{{ data.games }}  
                   </div>
       		</template>
           </Categroy>
       <!-- 子组件 -->
       	<template>
       		<div>
                   <!-- 配合具名插槽使用 -->
       			<slot name="center" :games="games" > 默认插槽内容 </slot>
               </div>
       	</template>
       <script>
       	export default {
               	name:'Child',
               	data(){
                       return {
                           games:["红色警戒", "传学火线", "劲舞团", "超级玛丽"],
                       }
                   }
       	}
       </script>
       ```



### vueX

`npm install vuex` 

搭建Vuex环境

`/src/store/index.js`

```js
// 创建 Vuex中的  store
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);

const action = {};  // sction：用于响应组件中的动作
const mutations = {};  // mutations：用于操作数据
const state = {};  // state：存储数据

// 创建并暴露store
export default new Vuex.Store({
  action,
  mutations,
  state,
});
```



#### **state** 

单一状态数，（存放数据）

> 组件中通过 `mapState`映射成计算属性，获取`$store.state`中的数据
>
> ```js
> import { mapState } from 'vuex'  // 引入 mapState
> 
> // 对象形式
> computed:{
>     ...mapState({
>       //...
>     // 箭头函数可使代码更简练
>     count: state => state.count,
> 
>     // 传字符串参数 'count' 等同于 `state => state.count`
>     countAlias: 'count',
> 
>     // 为了能够使用 `this` 获取局部状态，必须使用常规函数
>     countPlusLocalState (state) {
>       return state.count + this.localCount
>     }
>   })
> }
> 
> // 数组形式
> computed:{
>     ...mapState(['count','countAlias','countPlusLocalState'])
> }
> ```
>
> 

#### **action **

提交`mutation`而不是直接变更状态，并且可以包含**异步操作**

组件中通过  `this.$store.dispatch('xxx',value)`分发action

`action`函数接受`context对象`（上下文），通过`context`可以调用 `context.commit()`提交`mutation`，或者`context.getters`和`context.state`获取`getters`和`state`

**mapActions**

```js
methods:{
    ...mapActions({incrementOdd:'jiaOdd'}) // 对象写法
   	...mapActions(['jiaOdd']) // 数组写法
}
// 使用时  this.incrementOdd()  无参数
	// 有参数：this.jiaOdd(参数)
```



#### **mutation **

更改Vuex中的数据的唯一方法是通过`mutation`，`mutation`中必须是同步事务

组件中用`this.$store.commit('xxx',value)`提交载荷

`mutation`函数接受的第一个参数`state`获取`store`中的数据，第二个参数传过来的数据

```js
this.$store.commit('increment',value) // 直接传入参数
this.$store.commit({	// 传入对象
    type:'increment',
    count:10
})

// 使用
mutations:{
    increment(state,payload){
		state.num +=payload.count 	// 直接将整个对象传给mutation对象
    }
}
```

**mapMutations**

```js
methods:{
    ...mapMutations({increment:'JIA'}), //  对象写法
    ...mapMutations(['JIAN'])  // 数组写法
}
// 使用时  this.increment()  无参数
	// 有参数：this.JIAN(参数)
```



#### getters

`getter`的返回值会根据他的以来被缓存起来，且只有当它的依赖发生变化才被重新计算，相当于计算属性

组件通过 `this.$store.getters.属性`访问

`getters`接受`state`作为第一个参数，第二个参数为`getters`

```js
getters:{
	num(state){
		return state.sum * 100
	},
	num10:(state,getters)=>{
		return getters.num + 10
	}
}
```

通过方法访问给`getters`传参

```js
getters:{
    getNum(state){
        return function(age){
            return state.num == age ? '同龄':'不同龄'
        }
    },
    getNum:(state) => (age)=>{	return state.num == age ? '同龄':'不同龄'	}
}
// 组件中访问
this.$store.getters.getNum(21)
```

> `mapGetters` 映射`getters`的数据到计算属性
>
> ```js
> import { mapGetters } from 'vuex'  // 引入 mapState
> 
> // 对象形式
> computed:{
>     ...mapGetters({
>         getSchool:'getSchool'
>   })
> }
> 
> // 数组形式
> computed:{
>     ...mapState(['getSchool','getSum','getSubject'])
> }
> ```
>
> 



#### modules

> 模块化vuex
>
> 需要给每个module开启命名空间**`namespaced:true`** 
>
> ```js
> const count = {
> namespaced:true, //  使 辅助函数 mapState\mapMutations等可hi识别到
> state:{sum:0,school:'仓颉',subject:'物理'},
> mutations:{},
> actions:{},
> getters:{}
> }
> const person = {
> namespaced:true, //  使 辅助函数 mapGetters\mapActions 等可hi识别到
> state:{personList:[{id:'001',name:'张三'}]},
> mutations:{   
> ADD_PERSON(state, value) {
> 		state.personList.unshift(value);
> 	}
> },
> actions:{
> addPersonWang(context, value) {
>  if (value.name.indexOf("王") === 0) {
>    context.commit("ADD_PERSON", value);
>  }
> 	},
> },
> getters:{
> firstPerserName(state) {
>  return state.personList[0].name;
> 	},
> }
> }
> // 创建并暴露store
> export default new Vuex.Store({
> 	modules: {
>         count: countOptions,
>         person: personOptions,
>     },
> });
> ```
>
> 组件中使用
>
> ```js
> methods:{
> // 正常使用 mutations
> addPerson(){
> this.$store.commit('person/ADD_PERSON:',value)
> }
> // 使用 辅助函数 mapMutations()
> ...mapMutations('person',['ADD_PERSON'])
> 
> // 正常使用 actions
> addNameWang(){
> this.$dispatch('person/addPersonWang',personObj)
> }
> // 使用 辅助函数 mapActions()
> ...mapActions('person',['addPersonWang'])
> },
> computed:{
> // 使用 mapState() 辅助函数 
> ...mapState('count:',['school','sum','subject'])
> personList(){
> // 正常读取 state
> 	return this.$store.state.person.personList
> 	}
> // 正常使用 getters
>     fristName(){
>         return this.$store.getters['person/firstPersonName'];
>     }
> // 使用 辅助函数 mapGetters
>     ...mapGetters('person',['firstPersonName'])
> }
> ```
>



### vue-router

> SPA应用(single page web application)

将**组件**映射到**路由**，再告诉`Vue Router`在哪里渲染它们

#### 配置路由

> 1. 导入路由对象，并使用`Vue.use(VueRouter)`
>
> 2. 创建路由实例，并传入路由映射配置
>
>    ```js
>    export default new VueRouter({
>        routes:[
>            {
>                name:'HomePage', // 设置路由名称
>                path:'/home',
>                component:Home
>                children:[		// 配置子路由（嵌套路由）
>                	{
>                		path:'/message',
>                		component:Message
>            		}
>                ]
>            }
>        ]
>    })
>    ```
>
> 3. 在`Vue`实例中挂载创建的路由实例
>
>    ```js
>    import router from '@/router/index.js'
>    new Vue({
>      render: (h) => h(App),
>      router,
>    }).$mount("#app");
>    ```
>
>    

使用路由：

> - 路由入口`<router-link></router-link>`，默认被渲染为`<a></a>`标签
>   - `to`：指定跳转的路径
>   - `replacce`：替换当前（栈顶）记录，浏览器后退键不能返回到上一个页面中
>   - `active-class`：设置一个匹配成功时的类名
>     - 设置多个时使用：**`linkActiveClass`** 
> - 路由出口`<router-view></router-view>`
>   - 路由匹配到的组件将渲染在这里 



#### 路由传参

1. **query**参数

   - ```html
     <!-- 字符串形式传递 -->
     <router-link :to="/home?id=10&title='Home'">主页</router-link>
     ```

   - ```html
     <!-- 对象形式传递 -->
     <router-link 
         :to="{
              path:'/home',
              query:{
                  id:10,
              	 title:'Home'
     		}
         }"
     >主页
     </router-link>
     ```

   - 组件接受参数：通过 `$route.query`

2. **params**参数

   1. 必须在路由配置中占位`params`参数

      ```js
      {
         name: "xiangqing",
         // 声明展位 params参数
         path: "detail/:id/:title",
         component: Detail,
       },
      ```

      

   2. ```html
      <!-- 字符串形式传递 -->
      <router-link :to="`/detail/${10}/${Home}`">详情</router-link>
      ```

      ```html
      <!-- 对象形式传递  -->
      <router-link 
          :to="{
               name:'xiangqing',
               query:{
                   id:10,
               	 title:'Home'
      		}
          }"
      >详情
      </router-link>
      ```

      **注意：用`params`对象形式传值时不能使用`path`指定匹配路径**

3. 通过`props`将组件和路由解耦

   1. `props`对象模式  

      当 `props` 是静态的时候有用。

      ```js
      export default new VueRouter({
        routes: [
          {
            path: '/promotion/from-newsletter',
            component: Promotion,
            props: { id:'10',title:'Home' }
          }
        ]
      })
      /* 组件中通过 this.$route 获取 */
      this.$route.query
      this.$route.params
      ```

      

   2. `props`布尔模式

      如果 `props` 被设置为 `true`，`route.params` 将会被设置为**组件属性**。

      ```js
      export default new VueRouter({
        routes: [
          {
            path: '/promotion/from-newsletter',
            component: Promotion,
            props: true,
          }
        ]
      })
      /* 组件中通过 props 获取 */
      props:['id','title']
      ```

      

   3. `props`函数模式

      ```js
      export default new VueRouter({
        routes: [
          {
            path: '/promotion/from-newsletter',
            component: Promotion,
            // props：函数（接受 $route参数）
            props($route) {
               return {
                  id: $route.params.id,
                  title: $route.params.title,
                 };
            },
          }
        ]
      })
      /* 组件中通过 props 获取 */
      props:['id','title']
      ```

      ```js
      /* 连续解耦 */
      props(query:{id, title}) {
          return {
              id: id,
              title: title
          };
      },
      ```


#### 编程式路由导航

1. 作用：不借助`<router-link></router-link>`实现路由跳转，让路由跳转更加灵活

2. 方法：

   - `this.$router.forward()`：前进

   - `this.$router.back()`：后退

   - `this.$router.go(n)`：整数是是前n步，负数时为后退n步

   - `this.$router.push(参数)`：

     - 参数为：字符串、对象

       1. `this.$router.push('/home')`
       2. `this.$router.push({path:'/home'})`
       3. `this.$router.push({name:'Home',params:{id:'news'}})`
       4. `this.$router.push({path:'/home',query:{id:'13'}})`

     - 如果提供了**`path`**，`params`则会被忽略

       - 通过提供路由的`name`属性，或者完整的带有参数的`path`

         ```js
         this.$router.push({name:'user'},params:{userId})
         this.$router.push({path:`/user/${userId}`})
         ```

   - `this.$router.replace(参数)`

     - 跟 `router.push` 很像，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录	

#### 缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁

2. `include`为组件名称，省略是默认缓存所有路由

   `include`为数组可缓存多个  

   ```html
   <keep-alive include="News">
   	<router-view></router-view>
   </keep-alive>
   <keep-alive :include="['News', 'Message']">
   	<router-view></router-view>
   </keep-alive>
   ```

#### 两个新的生命周期钩子

路由组件独有的两个钩子，用于捕获路由组件的激活状态

**`activeed`**：路由组件被激活时触发

**`deactived`**：路由组件失活时触发



#### 路由守卫

*作用：对路由进行权限控制* 

*分为：**全局守卫**、**独享守卫**、**组件内守卫*** 

1. #### 全局路由守卫

   > 全局前置守卫
   >
   > - 初始化时、每次路由切换前执行
   >
   > - `router.beforeEach((to,from,next)=>{ next() // 放行 })`
   >
   > 全局后置守卫
   >
   > - 初始化时、每次路由切换后执行
   >
   > - `router.afterEach((to,from)=>{})`

2. #### 独享路由守卫

   > `beforeEnter((to,from,next)=>{next()})`

3. #### 组件内守卫

   > 1. 通过路由规则，进入该组件时被调用
   >
   >    `beforeRouterEnter((to, from , next)=>{ next() })`
   >
   > 2. 通过路由规则，离开该组件时被调用
   >
   >    `afterRouterEnter((to,from,next)=>{ next() })`



#### 路由元信息

> `meta`自定义一些内容
>
> ```js
> const router = new VueRouter({
>   routes: [
>     // 一级路由
>     {
>       name: "NameAbout",
>       path: "/about",
>       component: About,
>       meta: { title: "关于", isAuth: true },
>     }
>   ]
> })
> ```



#### HTML5 History模式与hash模式

> 默认为 **'hash模式'**  // 兼容性较好
>
> **'history'** // 兼容性一般，应用部署时需要后端人员支持
>
> ```js
>  new VueRouter({
>   mode: "history",
>   routes:[
>       /* 路由规则 */
>   ]
>  })
> ```
>
> 





## 总结

------

> 1. data中的所有属性，最后都出现在vm(Vue实例)上；
> 2. vm身上所有属性及Vue原型上所有属性，在Vue模板中都可以直接使用；

------

> 1. **Vue中的数据代理**
>
>    - 通过vm对象来代理data对象中属性的操作(读/写)
>
> 2. Vue中数据代理的好处
>
>    - 更加方便地操作data中地数据
>
> 3. 基本原理：
>
>    - 通过Object.defineProperty()把data对象中所有属性添加到vm上
>
>      为每一个添加地vm上的属性，都指定一个getter/setter
>
>      在getter/setter内部去操作data中对应的属性

------

> **vue如何检测 对象、数组？**
>
> Vue监视数据的原理：
>
> 1. ​	vue会监视data中所有数据
> 2. ​    监视对象数据：
>    - 通过`setter`实现监视，且在new Vue时就传入要检测的数据
>    - 对象中后追加的属性，Vue默认不做响应式处理
>    - 与要借助  `Vue.set()` 或 `this.$set()` 给vue添加响应式属性 
> 3. ​    监视数组数据：
>    - 通过包裹数组更新元素的放大实现：
>      1. 调用原生对应的方法对数组进行更新
>      2. 重新解析模板，更新页面
>    - 修改数组数据相关方式：
>      - 数组方法：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
>      - 替换数组：filter()、concat()、slice()
>      - Vue.set()、this.$set()
>        - VUe.set(vm.items,indexOfltem,newValue)、this.$set(vm.items,indexOfltem,newValue)
>          1. 参数：vm.items：表示要处理的数据（数组或对象）
>          2. 参数：indexOfltem：表示要处理的数组的索引或对象的属性名称
>          3. 参数：newValue：表示要处理的数据的值
>
> **数据劫持**：对data中的数据（所有）进行`getter`和`setter`的操作叫数据劫持；监视和劫持离不开**`Object.defineProperty()`**
>
> **模拟数据监视** 
>
> - ```js
>       // 只监视了一层  
>   	function Obs(data) {
>           const keys = Object.keys(data);
>                                                           
>           keys.forEach((k) => {
>             Object.defineProperty(this, k, {
>               get() {
>                 return data.k;
>               },
>               set(val) {
>                 console.log("数据被改了");
>                 data.k = val;
>               },
>             });
>           });
>         }
>                                                           
>   ```
>
>   
>
> 

------

## 复习

### webStorage

**localStorage** | **sessionStorage ** 

1. 存储大小一般为`5MB`左右（不同浏览器不同）

2. 浏览器通过`localStorage`和`sessionStorage`属性来实现本地存储

3. API

   1. `setItem('key','value')`

      接受一个键值对为参数，添加到本地存储中

   2. `getItem('key')`

      接受一个键名为参数，返回键名对应的值

   3. `removeItem('key')`

      接受一个键名为参数，在存储中删除对应的值

   4. `clear()`

      清空存储中的所有数据

4. 区别

   - `sessionStorage`存储的内容会随着浏览器窗口关闭而消失
   - `localStorage`需要手动清除才能删除
   - `getItem('key')`方法如果获取不到`key`对应的`value`，那么会返回 `null`
   - `JSON.parse(null)`结果为：nulle
