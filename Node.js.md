# Node.js

浏览器内核

- Gecko
- Trident
- Webkit
- Blink

JavaScript引擎

- V8
- JavaScriptCore
- Chakra
- SpoderMonkeey



V8引擎，及原理？



node的版本工具

- nvm：
  - 查看所有版本：`nvm list available`
  - 安装：`nvm install <版本号>`
  - 切换：`nvm use <版本号>`
  - 卸载：`nvm uninstall <版本号> `
- n：



Node的REPL

- REPL是**Read-Eval-Print Loop**的简称，翻译为**"读取-求值-输出" 循环**；





给Node传递参数

直接再命令行输入，如：`node index.js lihao age=22`

获取参数：通过`process.argv`数组获取

- argc：argument counter的缩写，传递参数的个数；
- argv：argument vector的缩写，传入的具体参数



Node输出

- console.log()

- console.clear()

  清空控制台

- console.tarce()

  打印函数的调用栈



常见的全局对象

- `process`：node进程相关信息，获取传递给node的参数
- `global`：global是一个全局对象，事实上前端我们提到的process、console、setTimeout等都有被放到global中
- `console`
- `setTimeout`
- `setInterval`
- `setImmediate`：立即执行
- `process.next(callback[,..args])`：添加到下一次tick队列中

特殊的全局对象

- `__dirname`
- `__filename`
- ...



## JavaScript模块化

### 模块化规范

- ### AMD

- ### CMD

- ### CommonJS

立即函数调用表达式（IIFE）`(function(){})()`



#### CommonJS

- 每一个js文件都是一个单独的模块

- 加载过程是运行时加载并且是**同步**的

- 核心变量：<font >Node中真正导出的是**`module.export`**，不是`exports `</font> 

  - **exports** 导出
    - `exports`默认为空对象`{}`，
  - **module.exports** 导出
    - 每一个js文件都是一个Module对象
    - exports与module.exports的关系
      - 关系：NodeJS默认是`module.exports = exports`
        - `module.exports = exports`在模块顶层执行
      - `module.exports`是`exports`的一个引用

  

  - **require** 导入

    - `require`是一个函数，可以帮助我们引入一个文件（模块）中导入的对象

      - 查找规则：`require(X)`

        1. X是一个核心模块，例如：path、http

           > 直接返回核心模块，并停止查找

        2. X是以 ./或 ../ 或 /(根目录)

           1. 将X当作一个文件在对应目录下查找

              - 有后缀名：按照后缀名查找文件

              - 没有后缀名：则按照以下顺序：

                > 1. 直接查找文件X
                > 2. 查找X.js
                > 3. 查找X.json
                > 4. 查找X.node

           2. 们没有找到对应文件，将X作为一个目录

              - 查找下面的index文件（没有找到则报错 not fount）

                > 1. 查找X/index.js文件
                > 2. 查找X/index.json文件
                > 3. 查找X/index.node文件

        3. 直接是一个X(没有路径)，并且不是核心模块

           > 1. 先在当前文件目录下查找`node_modules`文件
           > 2. 然后逐级查找`node_modules`文件，直到根目录下

- CommonJS模块的加载过程

  1. 模块在第一次引用时，模块总的代码会执行一次

  2. 模块被多次引入时，会缓存，最终只加载（运行）一次

     - 每个模块对象`module`都有一个属性：loaded

       为`false`表示还没有加载，为`true`表示已经加载

  3. 有用循环引用时，加载顺序是采用：深度优先算法 

     1. `【Node采用的是深度优先算法】`
     2. 引用关系是一种数据结构：图结构，遍历有：深度优先遍历和广度优先遍历
     
  4. 导出的是一个对象，其他地方修改这个对象属性时，所有地方都会改变

- 缺点：
  1. 加载模块是同步的，在浏览器中加载js文件则太慢



#### ES MOdule

与CommonJS的模块化的不同之处

1. 使用了`import`和`export`**关键字** 
   - `export`负责将模块内的内容导出
   - `import`负责从其他模块导入内容
2. 采用编译器的静态分析，并且加入了动态引用的方式
3. 采用ES Module将自动采用严格模式 `use strict`

```js
// 导出
// 方式一
// export const name = 'lihao'

const name = 'lihao'
// 方式二  export 后面的大括号 { }  不是一个对象 
// { /* 放置要导出的变量的引用列表 */ }
export {
	name
}
// 方式三 给要导出的变量起别名，导入时以别名为准
export {
	name as fName
}
```

```js
// 导入
// 方式一 '。/modules/foo.js'  必须带上后缀 .js
import { 标识符列表 } from '模块'
// 方式二 起别名
import { fName as wName } from './modules/foo.js'
// 方式三 通过 * 将模块功能放到一个模块功能对象上  如：foo
import * as foo from './modules/foo.js'
```

```js
// 导出导入结合使用，直接将导入模块导出
export { name } from './modules/foo.js'
```

1. 在浏览器中使用：导入js时`script`中**type属性为`module`** 此时会当作一个模块

   ```js
   <script src="./index.js" type="module"></script>
   ```

##### 默认导出

> `export default` 在一个模块中只能有一个默认导出（default export）

```js
// 默认导出
export default function(){
	console.log('默认导出')
}

// 导入，导入时不使用 {}，直接指定使用的名字
import defaultFun from './modules/cax.js'
```

##### import函数

`import`关键字加载模块时，不能放入到逻辑代码中

因为：ES Module在被JS引擎解析时，就必须知道他的依赖关系

使用`import()`函数，是一种异步动态加载，返回一个Promise

```js
import('./modules/foo.js')
    .then( res =>{} )
    .catch( err => {} )
```

##### ES MOdule加载过程

- `ES Module`加载js文件是解析时加载，并且是异步的；script标签上设置了`type=module`相当于加上async属性

- `export`在导出一个变量时，js引擎会解析这个语法，并创建`模块环境记录`（module environment record）

  - 模块环境记录会和变量进行绑定（binding），并且时实时绑定，在导入时是实时获取到最新的变量
  - 但如果导出的是一个对象，那么main.js中是可以修改对象的属性的，它们执行同意内存地址

  ![](F:\coding\Git\md\imgs\NodeJS\ES Module加载过程.png)









#### AMD（不常用）

- 主要应用在浏览器的一种模块化规范
- 采用**异步**加载模块

#### CMD（不常用）

- 也是应用在浏览器的一种模块化规范
- 采用**异步**加载模块，将吸取CommonJS的优点

