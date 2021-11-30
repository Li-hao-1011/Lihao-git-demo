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



### CommonJS

- 每一个js文件都是一个单独的模块

- 核心变量：<font style="color:red">Node中真正导出的是**`module.export`**，不是`exports `</font> 

  - **exports** 导出
    - `exports`默认为空对象`{}`，
  - **module.exports** 导出
    - 每一个js文件都是一个Module对象
    - exports与module.exports的关系
      - 关系：NodeJS默认是`module.exports = exports`
        - `module.exports = exports`在模块顶层执行
      - `module.exports`是`exports`的一个引用

  

  - **require** 导入



