# Node.js

Node.js运行环境的安装

- https://nodejs.org/en/				node.js官网
- http://nodejs.cn.download/        node.js中文网

Node.js的组成部分

- JavaScript 由三部分组成：ECMAScript，DOM，BOM。
- Node.js是由 ECMAScript 及Node环境提供的一些附加API组成的，包括哇唔见、网络、路径等等一些更强大的API。



## Noda.js中模块化开发

- Node.js规定一个JS文件就是一个模块，模块内部定义的变量和函数默认情况下在外部无法得到
- 模块内部可以使用 **exports** 对象将成员导出，使用 **require** 方法导入其他模块
- 模块成员 **导出** ：

```js
//a.js
const add = (a1, a2) => a1 + a2;

exports.add = add;	//导出
```

```js
//b.js
// const a = require('./02-a.js'); //导入模块
const a = require('./02-a')  //导入模块时可省略后缀 .js

// console.log(a);
console.log(a.add(20, 20));
```

- 另一种模块成员 **导出** 方式：	module.exports

```js
const greeting = name => `hello ${name}`;
const x = 100;

module.exports.greeting = greeting;  // module.exports
```



exports 和 module.exports 两种导出方式的区别：

1. **exports** 是 **module.exports** 的别名（地址引用关系）
2. 冲突的时候，导出对象以 **module.exports** 为准
3. **module.exports** 可以批量导出



## 系统模块

​		Node运行环境提供的API。因为这些API都是以模块化的方式进行开发的, 所以我们又称Node运行 环境提供的API为系统模块。

### 系统模块fs 文件操作

```js
//引入 fs 模块
const fs = require('fs');
```

读取文件内容 readFile 方法

```js
fs.reaFile('文件路径/文件名称'[,'文件编码'],callback);	//耗时操作
// callback 是一个回调函数，参数有：err，doc
	// 文件读取错误，err是一个对象
    // 文件读取成功 err是 null
    // doc 是文件读取的结果

// 包装fs.readFile 成 readFile 支持异步函数的方法
const promisify = require('util').promisify;
const readFile = promisify(fs.readFile);
```

写入文件内容 writeFile 方法
	写入的文件可以不存在，会自动创建

```js
fs.writeFile('文件路径/文件名称','数据',callback);	//耗时操作
// 回调函数 参数是：err
	//用来判断 是否写入成功
	// 文件读取错误，err是一个对象
    // 文件读取成功 err是 null
```



### 系统模块path 路径操作

为什么进行路径拼接？

- ​	不同操作系统的路径分隔符不同
  1. windows 是 \  /
  2. Linux 是  /

路径拼接的语法

```js
path.join('路径','路径',...);	//不属于耗时操作，有返回值
    // 返回 拼接好的路径
    // 会自动根据 系统 确定分隔符
```

相对路径和绝对路径

- 大多数情况下服务器端舒勇绝对路径，因为相对路径有时候相对的是命令行工具的当前工作目录
- 在读取文件或者设置文件路径时都会选择绝对路径
- 使用 __dirname 获取当前文件所在的绝对路径  (两个下划线)

```js
const path = require('path');
console.log(path.join(__dirname, '01-helloNode.js'));
// 获取到了 01-helloNode.js 这个文件的绝对路径
```









## 第三方模块

什么是第三方模块

- 别人写好的、具有特定功能的、我们能直接使用的模块即第三方模块，由于第三方模块通常都是由 多个文件组成并且被放置在一个文件夹中，所以又名包。

第三方模块有两种存在形式：

1. 以js文件的形式存在，提供实现项目具体功能的API接口。
2. 以命令行工具形式存在，辅助项目开发

获取第三方模块命令：

- npm (node package manager) ： node的第三方模块管理工具
- 使用方式： 
  1. 下载：npm install 模块名称 模块名称2 模块名称3 
  2. 卸载：npm unintall package 模块名称
- 全局安装与本地安装
  1. 命令行工具：全局安装
  2. 库文件：本地安装



#### nodemon

- nodemon是一个命令行工具，用以辅助项目开发。
- 在Node.js中，每次修改文件都要在命令行工具中重新执行该文件，非常繁琐。

使用步骤：

1. ​	npm install nodemon –g

2. ​	在命令行工具中用nodemon命令替代node命令执行文件

   ctrl + c  ——终止操作（在命令行中是终止操作）



#### nrm

- nrm ( npm registry manager )：npm下载地址切换工具
- npm默认的下载地址在国外，国内下载速度慢

- 使用步骤：
  1. npm install nrm –g 
  2. 查询可用下载地址列表： nrm ls 
  3. 切换npm下载地址： nrm use 服务器别名



#### Gulp

- 基于node平台开发的前端构建工具
- 将机械化操作编写成任务, 想要执行机械化操作时执行一个命令行命令任务就能自动执行了
- 用机器代替手工，提高开发效率。

Gulp的使用：

1. **npm install gulp**  (库文件都是本地安装，所以不需要加-g)
2. 在项目根目录下建立 **gulpfile.js** 文件
3. 重构项目的文件夹结构 ，新建 **src** 目录放置源代码文件，**dist** 目录放置构建后文件
4. 在gulpfile.js文件中编写任务
5. 在命令行工具中执行gulp任务

Gulp中提供的方法：

- **gulp.src()** ：获取任务要处理的文件
- **gulp.dest()** ：输出文件
- **gulp.task()** ：建立gulp任务
- **gulp.watch()** ：监控文件的变化

Gulp插件：

- gulp-htmlmin ：html文件压缩 
- gulp-csso ：压缩css 
- gulp-babel ：JavaScript语法转化 
- gulp-less: less语法转化 
- gulp-uglify ：压缩混淆JavaScript 
- gulp-file-include 公共文件包含（抽取代码的公共部分）
- browsersync 浏览器实时同步

使用步骤： 

1. 安装插件：**npm install gulp-插件名 --save-dev**  
2. 在 **gulpfile.js** 中引入插件 
3. 在 gulpfile.js 中使用插件

构建任务：

gulp 4 版本之后，构建 default 发生了变化

gulp 4 的方法:	

- ​	gulp.series：按照顺序执行
- ​    gulp.paralle：可以并行计算

```js
//gulp 3
gulp.task('default', ['htmlmin', 'cssmin', 'jsmin', 'copy']);
```

```js
//gulp 4
gulp.task('default', gulp.parallel("copy", "cssmin", "jsmin", "htmlmin", function() { console.log("success") }))
```

运行任务：

​	通用命令： gulp default

​	简写命令：gulp



#### router	

功能：实现路由			npm install router

使用步骤：

1. 获取路由对象

2. 调用路由对象提供的方法创建路由

3. 启用路由，使路由生效

   ```js
   const getRouter = require('router');	//获取路由对象
   const router = getRouter();		//调用路由对象提供的方法创建路由
   router.get('/add',(req,res)=>{
       res.end('hello world')
   })
   router(req, res, () => {});  //启用路由功能
   ```

   

#### serve-static

功能：实现静态资源访问服务			npm install serve-static

步骤：

1. 引入 server-static 模块创建静态资源服务功能的方法

2. 调用方法创建静态资源服务并指定静态资源服务目录

3. 启用静态资源服务功能

   ```js
   //引入 server-static 模块创建静态资源服务功能的方法
   const serveStatic = require('server-static');
   //调用方法创建静态资源服务并指定静态资源服务目录
   const serve = serverStatic('public');
   // 启用静态资源访问服务功能
   serve(req, res, () => {});		
   ```

   



## package.json文件

node_modules文件夹的问题

- 文件夹以及文件过多过碎，当我们将项目整体拷贝给别人的时候,，传输速度会很慢很慢
- 复杂的模块依赖关系需要被记录，确保模块的版本和当前保持一致，否则会导致当前项目运行报错

#### package.json文件夹的作用

- 项目描述文件，记录了当前项目信息，例如项目名称、版本、作者、github地址、当前项目依赖了 哪些第三方模块等
- 使用 **npm init -y** 命令生成。（y即yes，即不修改任何内容，全部使用默认值ye）

#### 项目依赖

- 在项目的开发阶段和线上运营阶段，都需要依赖的第三方包，称为项目依赖
- 使用” **npm install 包名** ”下载的文件会默认被添加到 package.json 文件的 dependencies 字段
- **npm install --production** （只下载项目依赖，生产环境）



#### 开发依赖

- 在项目的开发阶段需要依赖，线上运营阶段不需要依赖的第三方包，称为开发依赖。（比如：gulp）
- 使用” **npm install 包名 --save-dev** ”将包添加到package.json文件的devDependencies字段

- **npm install** //所有依赖全部安装



#### package-lock.json文件的作用

记录模块与模块之间的依赖关系： 

- 锁定包的版本，确保再次下载时不会因为包版本不同而产生问题 
- 加快下载速度，因为该文件中已经记录了项目所依赖第三方包的树状结构和包的下载地址，重 新安装时只需下载即可，不需要做额外的工作



## Node.js中模块加载机制

#### 模块查找规则-当模块拥有路径但没有后缀时

- require方法根据模块路径查找模块，如果是完整路径，直接引入模块。

```js
require('./find.js');
```

1. 如果模块后缀省略，先找同名JS文件再找同名JS文件夹 
2. 如果找到了同名文件夹，找文件夹中的index.js 
3. 如果文件夹中没有index.js就会去当前文件夹中的package.json文件中查找main选项中的入口文件。（将当前目录当作整体模块）
4. 如果找指定的入口文件不存在或者没有指定入口文件就会报错，模块没有被找到

```js
require('./find')
```



#### 模块查找规则-当模块没有路径且没有后缀时

1. Node.js会假设它是系统模块
2. Node.js会去node_modules文件夹中 
3. 首先看是否有该名字的JS文件 
4. 再看是否有该名字的文件夹 
5. 如果是文件夹看里面是否有index.js 
6. 如果没有index.js查看该文件夹中的package.json中的main选项确定模块入口文件
7. 否则找不到报错

```js
require('find');
```





# 服务器端基础概念



URL

统一资源定位符，又叫URL（Uniform Resource Locator），是专为标识Internet网上资源位置而 设的一种编址方式，我们平时所说的网页地址指的即是URL。

URL的组成：

- 传输协议://服务器IP或域名:端口/资源所在位置标识 
- http://www.xyz.com/news/20181018/09152238514.html 
- http：超文本传输协议，提供了一种发布和接收HTML页面的方法。

IP地址：

- 互联网中设备的唯一标识。

域名：

- 域名就是平时上网所使用的网址
  - http://www.itheima.com  =>  http://124.165.219.100/

端口：

- 



## 创建Web服务器

```js
const http = require('http');	//引用系统模块
const app = http.createServer();	//创建Web服务器

// 客户端发送来的请求
app.on('request', (req, res) => {
    //响应
    res.end('<h2>hello user</h2>');
});
//监听 3000 端口
app.listen(3000);
console.log("网站服务器启动成功");
```



## HTTP协议

超文本传输协议（英文：HyperText Transfer Protocol，缩写：HTTP）规定了如何从网站服务器 传输超文本到本地浏览器，它基于客户端服务器架构工作，是客户端（用户）和服务器端（网站） 请求和应答的标准。

![image-20210209154434090](D:\md\imgs\http协议.png)

### 请求报文

1. 请求方式

   - GET 	 
   - POST	

2. 请求地址

   ```js
   app.on('request', (req, res) => {
   
       req.headers //获取请求报文
       req.url //获取请求地址
       req.method //获取请求方法
   })
   ```

### 响应报文

1. HTTP 状态码
   - 200 请求成功
   - 404 请求的资源没有被找到
   - 500 服务器端错误
   - 400 客户端请求有语法错误

2. 内容类型
   - text/plain(纯文本，默认) 
   - text/html 
   - text/css 
   - application/javascript 
   - image/jpeg 
   - application/json

```js
//响应状态码
res.writeHead(200, {
    'content-type': 'text/html;charset=utf8'
}) 
// content-type为：内容类型
// charset=utf8为：utf-8编码
```



## HTTP请求与响应处理

### 请求参数

客户端向服务器端发送请求时，有时需要携带一些客户信息，客户信息需要通过请求参数的形式传 递到服务器端，比如登录操作。

1. GET请求参数

   参数被放置在浏览器地址栏中，获取需要借助系统模块url

   ```js
   const http = require('http');
   const url = require('url');
   const app = http.createServer();
   app.on('request', (req, res) => {
   // 将url路径的各个部分解析出来并返回对象；true 代表将参数解析为对象格式
   let {query , pathname} = url.parse(req.url, true);//除了query还有一个pathname比较常用
   console.log(query);
   });
   app.listen(3000);
   ```

   

### POST请求参数

- 参数被放置在请求体（报文）中进行传输，获取POST参数需要使用 **data事件** 和 **end事件**

- 使用querystring系统模块将参数转换为对象格式

  ```js
  const querystring = require('querystring');//处理请求参数模块
  app.on('request', (req, res) => {
  let postData = '';
      //监听参数传输事件
  req.on('data', (params) => postData += params;);
      //chunk是传递进来的post数据chua
      //监听参数传输完毕事件
  req.on('end', () => {
  console.log(querystring.parse(postData));
  });
  });
  ```

  

### 静态资源

​		服务器端不需要处理，可以直接响应给客户端的资源就是静态资源，例如CSS、JavaScript、image、 html等文件。（浏览器能够直接解析的文件）

​		为什么不用双击打开文件呢？ 
​				双击能够打开，只能证明这个文件在你的本地，而不是网络文件。

第三方模块  mime

​	可以获取文件的类型，如css、js、html等

```js
let type = mime.getType(realPath)；// realPath：地址路径
// 返回 文件的类型
```



### 动态资源

​		相同的请求地址不同的响应资源，这种资源就是动态资源。



## Node.js异步编程



### 同步API、异步API

- 同步API：只有当前API执行完成后，才能继续执行下一个API
- 异步API：当前API的执行不会阻塞后续代码的执行

同步API可以从返回值中拿到API执行的结果, 但是异步API是不可以的

- 使用 **回调函数** 获取异步API执行结果

```js
function getMsg (callback) {
    setTimeout(function () {
    	callback ({ msg: 'Hello Node.js' })
    }, 2000);
}
getMsg (function (msg) {
	console.log(msg);
});
```



### 同步API, 异步API的区别（代码执行顺序）

- 同步API从上到下依次执行，前面代码会阻塞后面代码的执行

  ```js
  for (var i = 0; i < 100000; i++) {
  	console.log(i); }
  console.log('for循环后面的代码');
  //按顺序执行
  ```

  

- 异步API不会等待API执行完成后再向下执行代码

  ```js
  console.log('代码开始执行');
  setTimeout(() => { console.log('2秒后执行的代码')}, 2000);
  setTimeout(() => { console.log('"0秒"后执行的代码')}, 0);
  console.log('代码结束执行');
  //执行顺序：代码开始执行--->代码结束执行--->"0秒"后执行的代码--->2秒后执行的代码
  ```

  

### 回调地狱问题

如果异步API后面代码的执行依赖当前异步API的执行结果，但实际上后续代码在执行的时候异步 API还没有返回结果，这个问题要怎么解决呢？

```js
const fs = require('fs');
fs.readFile('.1/txt','utf8',(err,result1)=>{
    console.log(result1);
    fs.readFile('./2.txt','utf8',(err,result2)=>{
        console.log(result2);
        fs.readFile('./3.txt','utf8',(err,result3)=>{
            console.log(result3);
        })
    })
});
```



### Promise

- Promise出现的目的是解决Node.js异步编程中回调地狱的问题。

```js
let promise = new Promise((resolve,reject)=>{  
    setTimeout(()=>{
        if(true){
            resolve({name:'张三'})
        }else {
            reject('失败了')
        }
    }，2000);
});
promise.then((result)=>{console.log(result)})  //{name:'张三'}
	.catch((error)=>{console.log(error)})  //失败了
```

需要 先 new 一个Promise实例对象，通过参数 (resolve,reject)，

- resolve 返回  **异步API执行成功的结果** 

- reject 返回 **异步API执行失败的结果** 

  实例对象.then((result)=>{})		（ .then() 接受成功的信息）

  ​				.catch((error)=>{})					  （.catch() 接受失败的信息）
  
- Promise三种状态

  - pending：等待事件
  - fulfill：满足状态，当我们主动回调resolve时，就会回调 .then()
  - reject：拒绝状态，当我们主动回调reject时，就会回调 .catch()
  
- Promise的all方法

  - Promise.all(参数)：参数为数组，当参数全部执行完成后，才执行  .then(results=>{})

  -  .then(results=>{})中 results 是一个数组

  - ```js
    Promise.all([
        new Promise((reslove, reject) => {
            setTimeout(() => {
                reslove('res1')
            }, 1000)
        }),
        new Promise((reslove, reject) => {
            setTimeout(() => {
                reslove('res2')
            }, 4000)
        }),
    ]).then(results => {
        console.log(results[0]);
        console.log(results[1]);
    })
    ```

    

#### 解决回调地狱问题

```js
const fs = require('fs');

function p3() {
    return new Promise((resolve, reject) => {
        fs.readFile('./3.txt', 'utf8', (err, result3) => {
            resolve(result3);
        })
    });
};
function p2() {
    return new Promise((resolve, reject) => {
        fs.readFile('./2.txt', 'utf8', (err, result3) => {
            resolve(result3);
        })
    });
};
function p1() {
    return new Promise((resolve, reject) => {

        fs.readFile('./1.txt', 'utf8', (err, result3) => {
            resolve(result3);
        })
    });
};
p1().then((r1) => {
        console.log(r1);
        return p2();
    })
    .then((r2) => {
        console.log(r2);
        return p3()
    })
    .then((r3) => {
        console.log(r3);
    })
```





### 异步函数

- 异步函数是异步编程语法的终极解决方案，它可以让我们将异步代码写成同步的形式，让代码不再 有回调函数嵌套，使代码变得清晰明了

```js
const fn = async () => { };
```

```js
async function fn () { };
```

#### async 关键字

- 普通函数定义前加async关键字 普通函数变成异步函数
-  异步函数默认 **返回 promise 对象** 
- 在异步函数内部使用return关键字进行结果返回 结果会被包裹的promise对象中 return关键字 代替了resolve方法
- 在异步函数内部使用 **throw关键字 抛出程序异常** 
- 调用异步函数再 **链式调用then方法** 获取异步函数执行结果
- 调用异步函数再 **链式调用catch方法** 获取异步函数执行的错误信息

**await 关键字** 

- await关键字只能出现在异步函数中
- await promise ：await后面只能写promise对象 写其他类型的API是不可以的
- await关键字可是暂停异步函数向下执行 **直到 promise 返回结果** 

#### 解决回调地狱问题

##### 方法一：

```js
const fs = require('fs');
async function p1() {
    return fs.readFile('./1.txt', 'utf8', (err, result1) => {
        resolve(result1);
    })
};
async function p2() {
    return fs.readFile('./2.txt', 'utf8', (err, result2) => {
        resolve(result2);
    })
};
async function p3() {
    return fs.readFile('./3.txt', 'utf8', (err, result3) => {
        resolve(result3);
    })
};

async function fn() {
    await p1();
    await p2();
    await p3();
}
```



##### 方法二：

const promisify = require('util').promisify;

const readFile = promisify(fs.readFile);

封装一个函数，得到一个函数，得到的函数 返回值是一个promise

```js
const fs = require('fs');
const promisify = require('util').promisify;//改造现有的异步函数API，让其返回promise对象，从而支持异步函数语法
const readFile = promisify(fs.readFile);

async function fn() {
    let r1 = await readFile('./1.txt', 'utf8');
    let r2 = await readFile('./2.txt', 'utf8');
    let r3 = await readFile('./3.txt', 'utf8');
    console.log(r1);
    console.log(r2);
    console.log(r3);
};

fn();
```



## Node.js 全局对象 global

在 **浏览器** 中全局对象是 **window**，在 **Node** 中全局对象是 **global** 。

Node中全局对象中有以下方法，可以在任何地方使用，global 可以省略。

- console.log()	在控制台中输出
- setTimeout()	设置超时定时器
- clearTimeout()	清除超时定时器
- setInterval()		设置间歇定时器
- clearInterval()	清除间歇定时器





# MongoDB 

数据库：数据库即存储数据的仓库，可以将数据进行有序的分门别类的存储。它是独立于语言之外的软件， 可以通过API去操作它。



**数据库相关概念** 

在一个数据库软件中可以包含多个数据仓库，在每个数据仓库中可以包含多个数据集合，每个数据集合中可以包含多条文档（具体的数据）。

![](D:\md\imgs\MongoDB数据库术语.png)



Mongoose第三方包

-  使用Node.js操作MongoDB数据库需要依赖Node.js第三方包mongoose

  ​	npm install mongoose

## 启动、停止MongoDB

- 启动MongoDB：

  ​	net start mongodb

- 停止MongoDB：

  ​	net stop mongodb

  命令行工具要有系统管理员权限



## 数据库连接

- 使用mongoose提供的 connect 方法即可连接数据库

```js
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/mongodbProject_1', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log('数据库连接成功'))
    .catch(err => console.log(err, '数据库连接失败'))
```

## 创建数据库

- 在MongoDB中不需要显式创建数据库，如果正在使用的数据库不存在，MongoDB会自动创建

## 创建集合

创建集合分为两步，

1.  **对集合设定规则** ，

2.  **创建集合** 创建mongoose.Schema构造函数的 实例即可创建集合。（创建了数据库，创建了集合；但是没有数据的时候，并不会真正创建数据库）

   ```js
   //设置集合规则
   const courseSchema = new mongoose.Schema({
       name: String,
       author: String,
       isPublished: Boolean
   });
   // 创建集合并应用规则,(参数一：集合名称、参数二：集合规则)
   const Course = mongoose.model('Course', courseSchema); // courses
   //会返回一个构造函数，因为构造函数下有很多的方法可以对数据库进行操作
   ```



## 创建文档

- 创建文档实际上就是向集合中插入数据。

- 分为两步：

  1. 创建集合实例。

  2. 调用实例对象下的 **save 方法** 将数据保存到数据库中。

     ```js
     //创建集合实例(创建文档)
     const course = new Course({
         name: 'node,js基础',
         author: '黑马讲师',
         isPublished: true
     });
     // 将数据保存到数据库中
     course.save();
     ```


另一种方法：	构造函数下面的 create方法向集合插入文档

```js
Course.create({ name: 'js', author: '黑马程序员', isPublished: false }, (err, doc) => {
    console.log(err);
    console.log(doc);
})  // 通过 回调函数 接受异步API结果
```

```js
Course.create({ name: 'js', author: '黑马程序员456', isPublished: false })
    .then(doc => { console.log(doc); })
    .catch(err => { console.log(err); })
// 通过 Promise 对象接受异步API结果
```





## MongoDB数据库导入数据

​	mongoimport –d 数据库名称 –c 集合名称 --file 要导入的数据文件  (file前面两个 - )

​	前期准备： 找到mongodb数据库的安装目录，将安装目录下的bin目录放置在环境变量中。
​			将MongoDBTools解压，覆盖到bin目录。
​				 		C:\Program Files\MongoDB\Server\4.4\bin
​			并将mongoimport文件设置成系统变量



## 查询文档

- find() 方法查找数据，不管查几条数据返回的都是数组。如果找不到返回空数组。
- findOne() 方法 返回的是一个对象(文档)，默认返回当前集合中第一条文档

两个方法可以接受一个对象作为参数

```js
User.find({ _id: '5c09f236aeb04b22f8460967' })
    .then(result => { console.log(result); });
```

```js
User.findOne({ name: '李四' }).then(result => { console.log(result); });
```

```js
User.find({ age: { $gt: 20, $lt: 40 } }).then(res => { console.log(res); })
// 查询集合中 age 大于20且小于40 的文档
```



```js
User.find({age: {$gt: 20, $lt: 50}}).then(result => console.log(result));
// 匹配大于20小于50，$gt 表示大于、$lt 表示小于
```

```js
// 匹配hobies包含足球的文档  $in 表示包含
User.find({ hobbies: { $in: ['足球'] } }).then(res => { console.log(res); });
```

```js
// select(参数)方法选择要查询的字段，不想要查询的字段名前面加上横杠“-”
User.find().select('name email -_id').then(result => console.log(result)) 
// 查询name email字段，不包含_id字段
```

```js
// 将数据按照年龄进行降序排序
User.find().sort('-age').then(result => console.log(result)) 
// sort(参数)方法默认升序，参数前面加 - 表示降序排列
```

```js
// skip 跳过多少条数据 limit 限制查询数量。在分页中比较常用
User.find().skip(2).limit(2).then(result => console.log(result))
```



## 删除文档

```js
// 删除单个文档  findOneAndDelete()方法
// 查找到一条文档 并且删除，返回删除的文档（如果查询条件匹配了多个文档，将会删除第一个匹配的文档）
Course.findOneAndDelete({_id:'id字符串'}).then(result => console.log(result))
```

```js
// 删除多个
// 参数是 查询条件，返回值是一个对象，{n:4,ok:1} ok代表删除是否成功,n代表删除几条数据
User.deleteMany({}).then(result => console.log(result))//删除全部文档
```



## 更新文档

```js
// 更新单个文档,返回Promise对象，ok属性为 1 则更新成功
// 如果 匹配了多个数据，只更新第一个文档
User.updateOne({查询条件}, {要修改的值}).then(result => console.log(result));
User.updateOne({name:'张三'}, {name:'张狗剩'}).then(result => console.log(result))
```

```js
// 更新多个文档
User.updateMany({查询条件}, {要修改的值}).then(result => console.log(result));
```

## mongoose验证

在创建集合规则时，可以设置当前字段的验证规则。验证失败就禁止插入。

1. required：true，必传字段，
   还可以传入一个数组[ ]，[true , '请传入文章标题']，第二个参数是错误提示

2. minlength：3，字符串最小长度为3

3. maxlength：20，字符串最大长度为20

4. min：2，数值最小为2

5. max：100，数值最小为100

6. enum：['html','css','javaScript','node.js']，（列举出当前字段可以拥有的值）当前字段的值必须为enum中的一种，参数可以是数组也可以是一个对象

   ```js
   enum:{
       values: ['html','css','javascript','node.js'],
       message:'分类名称要在一定的范围内才可以', // 错误信息
   }
   ```

   

7. trim：true，去除字符串两边的空格

8. default：默认值，如果没有填写则默认为此值

9. validate：自定义验证器

   ```js
   author:{
       type:String,
       validate:{
           validator: v =>{	
               // 返回布尔值，true验证成功、false验证失败，v是要验证的值(传入的值·)
               return v && v.length > 4	},
           message:'传入的值不符合验证规则',   //自定义错误信息
       }
   }
   ```

获取错误信息：

```js
Post.create({ title: '61' },age:60,category:'java',author:'bd')
    .then(res => console.log(res))
	.catch{error => {		// 通过 .catch()方法获取错误信息
        const err = error.errors;
        for( var attr in err ){
            console.log(err[attr]['message'])
        }
    }}
```



## 集合关联

​		通常不同集合的数据之间是有关系的，例如文章信息和用户信息存储在不同集合中，但文章是某个 用户发表的，要查询文章的所有信息包括发表用户，就需要用到集合关联。

1. 使用id对集合进行关联
2. 使用populate方法进行关联集合查询

```js
const mongoose = require('mongoose');
//连接数据库
mongoose.connect('mongodb://localhost/mongodbProject_1', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log('数据库连接成功'))
    .catch(err => console.log(err, '数据库连接失败'));

// 用户集合规则
const userSchema = new mongoose.Schema({
    name: {
        type: String,
        required: [true, '请传入姓名'],
    }
});
// 文章规则
const postSchema = new mongoose.Schema({
    title: { type: String, },
    author: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User'
    }

});
const User = mongoose.model('User', userSchema);
const Post = mongoose.model('Post', postSchema);

// 创建用户
// User.create({ name: '张三' }).then(res => console.log(res))

// 创建文章
// Post.create({ title: '123', author: '6027beba5675d7533848902d' }).then(res => { console.log(res); });
// 查询
Post.find().populate('author').then(res => { console.log(res); });
```





# 模板引擎   art-template

art-template模板引擎是 Node.js 第三方模块

1. ​	npm install art-template   命令下载
2. ​	const template = require('art-template')  引入模板
3. ​	const html = template(‘模板路径’, 数据)；告诉模板引擎要拼接的数据和模板在哪 
   - 模板路径使用绝对路径，数据参数为 对象类型

## 模板语法

- lart-template同时支持两种模板语法：标准语法和原始语法。

- 标准语法可以让模板更容易读写，原始语法具有强大的逻辑处理能力。

  标准语法： {{ 数据 }}

  原始语法：<%=数据 %>

### 输出

- 标准语法： {{ 数据 }}
- 原始语法：<%=数据 %>

### 原始输出

如果数据中携带 HTML标签，默认模板引擎不会解析标签，会将其转义后输出。

- 标准语法：{{@ 数据 }}

- 原始语法：<%- 数据 %>

  会将HTML标签解析

### 条件判断

标准语法：

```js
{{if 条件}} ... {{/if}}
{{ if v1}} ... {{else if v2}} ... {{else}} ... {/if}
```

原始语法：

```
<% if (v1) {%> ... <%} %>
<% if (v1) {%> ... <%} else if (v2){%> ... <%} else {%> ... <%} %>
```

```html
<!- 例子： -->
<%  
    if (age > 18)  { %> 年龄大于18<% }
    else if (age <15) {  %> 年龄小于15<% }
    else {%> 年龄不符合要求<%}
%>

{{if age>18}} 年龄大于18 
    {{else if age < 15}} 年龄小于15 
    {{else}} 年龄不符合要求            
{{/if}}
```



### 循环

标准语法：

​		{{each 数据}} ... {{/each}}

```js
{{each users}}
    {{$index}}  
    {{$value.name}}      
{{/each}}
```

原始语法：	

​		<%  for( ) { %>  ...	<%   }      %>

```
<% for(var i = 0;i< users.length;i++){ %>
            <%= i%>
            <%= users[i].name%>
<% }   %>
```



### 子模版

​	使用子模板可以将网站公共区块(头部、底部)抽离到单独的文件中。

- 标准语法：{{include '模板'}}
- 原始语法：<%include('模板') %>

```js
{{include './common/header.art'}}

<% include('./common/footer.art') %>
```



### 模板继承

使用模板继承可以将网站HTML骨架抽离到单独的文件中，其他页面模板可以继承骨架文件。

1. 在骨架模板中使用  {{block ' 自定义名字 '}} {{/block}}；	// 自定义名称 --->定向填充特殊的内容
2. 在页面模板中使用  {{extend '骨架模板的路径'}}	继承骨架模板
3. 在页面模板中使用  {{block '自定义名称'}} ...内容 {{/block}}

模板示例：

```html
<!- 骨架模板 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    {{block 'link'}} {{/block}}			<!-  -->
</head>
<body>
    {{block 'content'}} {{/block}}
</body>
</html>
```

```art
 {{extend './common/layout.art'}} ; 		
 {{block 'content'}}	<p>{{ msg }}</p>	{{/block}} 
 
 {{block 'link'}}	<link rel="stylesheet" type="text/css" href="./main.css">	{{/block}}
```



### 模板配置

1. 向模板中导入变量  template.defaults.imports.变量名 = 变量值;

2. 设置模板根目录 template.defaults.root = 模板目录

3. 设置模板默认后缀 template.defaults.extname = '.art'

   ```js
   const dateFormat = require('dateformat')
   // 导入模板变量
   template.defaults.imports.dateFormat = dateFormat;
   
   // 设置模板的根目录
   template.defaults.root = path.join(__dirname, 'views');
   
   // 设置模板的默认后缀
   template.defaults.extname = '.art'
   
   const html = template('06', {
       time: new Date()
   });
   
   console.log(template('07', {
       time: new Date()
   }));
   ```

   



# Express 框架

​		Express是一个基于Node平台的web应用开发框架，它提供了一系列的强大特性，帮助你创建各种Web应用。我们可以使用 npm install express 命令进行下载。

## Express框架特性

- 提供了方便简洁的路由定义方式
- 对获取HTTP请求参数进行了简化处理
- 对模板引擎支持程度高，方便渲染动态HTML页面
- 提供了中间件机制有效控制HTTP请求
- 拥有大量第三方中间件对功能进行扩展



## 创建服务器

​		使用Express框架创建web服务器及其简单，调用express模块返回的函数即可。

```js
const express = require('express');		// 导入 express 框架
// 创建网站服务器
const app = express();
// get 请求
app.get('/', (req, res) => {
    // send()  响应内容
    res.send('Hello Express');
});
app.get('/list', (req, res) => {
    // send()  响应内容
    res.send({
        name: '张三',
        age: 20
    });
});
// 监听端口
app.listen(3000);
console.log('服务器已启动');
```



## 中间件

​		中间件就是一堆方法，可以接收客户端发来的请求、可以对请求做出响应，也可以将请求继续交给下一个中间件继续处理。

![](D:\md\imgs\Nodejs-Express中间件.png)

- 中间件主要由两部分构成，中间件方法以及请求处理函数。
- 中间件方法由Express提供，负责拦截请求，请求处理函数由开发人员提供，负责处理请求。

```js
app.get('请求路径','处理函数');		// 接受并处理get请求
app.post('请求路径','处理函数');	// 接受并处理post请求
```

### 什么是中间件

- 可以针对同一个请求设置多个中间件，对同一个请求进行多次处理。
- 默认情况下，请求从上到下依次匹配中间件，一旦匹配成功，终止匹配。
- 可以调用 **next() 方法** 将请求的控制权交给下一个中间件，直到遇到结束请求的中间件。

```js
app.get('/request', (req, res, next) => {
    req.name = '张三';
    next();
};
app.get('/request', (req, res) => {
    res.send(req.name);
});
```

### app.use()中间件用法

app.use 匹配所有的请求方式，可以直接传入请求处理函数，代表接收所有的请求。

```js
// 接受所有请求的中间件
app.use((req, res, next) => {
    console.log('请求走了 app.use 中间件');
    next();
});
```

app.use 第一个参数也可以传入请求地址，代表不论什么请求方式，只要是这个请求地址就接收这个请求。

```js
// 接受'/request' 
app.use('/request', (req, res, next) => {
    console.log('请求走了 app.use /request 中间件');
    next();
});
```

```js
// status() 可以传入状态码
res.status(404).send('当前访问的页面不存在');
```



### 错误处理中间件		

​	只能捕获到 同步代码中的错误，

​	异步代码需要手动触发错误(将错误传入到next()方法中)------>next(err)

- 在程序执行的过程中，不可避免的会出现一些无法预料的错误，比如文件读取失败，数据库连接失败。
- 错误处理中间件是一个集中处理错误的地方。

```js
 app.use((err, req, res, next) => {
     res.status(500).send('服务器发生未知错误');
 })
// 错误处理中间件有四个参数，err\req\res\next
```

​		当程序出现错误时，调用next()方法，并且将错误信息通过参数的形式传递给next()方法，即可触发错误处理中间件。

```js
app.get('/index', (req, res, next) => {
     throw new Error('程序发出了未知错误');	// throw 抛出错误
    fs.readFile('./01.js', 'utf8', (err, doc) => {
        if (err != null) {
            next(err);	// 手动触发错误
        } else {
            res.send(doc);
        }
    })
});
// 错误处理中间件
app.use((err, req, res, next) => {
    res.status(500).send(err.message)
})
```



### 捕获错误

- 在node.js中，异步API的错误信息都是通过回调函数获取的，支持Promise对象的异步API发生错误可以通过catch方法捕获。
- 异步函数执行如果发生错误要如何捕获错误呢？

 **try catch** 可以 **捕获异步函数以及其他同步代码在执行过程中发生的错误** ，但是不能其他类型的API发生的错误。

```js
app.get('/index', async(req, res, next) => {
    try {
        await readFile('.aa.js')
    } catch (e) {
        next(e);
    }
});
```



## 构建模块化路由

express.Router()  创建路由对象

```js
const express = require('express');
// 创建网站服务器
const app = express();
// 创建路由对象
const home = express.Router();
// 为路由对象匹配请求路径
app.use('/home', home);
// 创建二级路由
home.get('/index', (req, res) => {
    res.send('欢迎来到博客首页')
})
// 监听端口
app.listen(3000);
```



## Express请求处理

### GET参数的获取

Express框架中使用**req.query**即可获取GET参数，框架内部会将GET参数 **转换为对象并返回** 。

```js
app.get('/index', (req, res) => {
    res.send(req.query);
});
// http://localhost:3000/index?name=zhangsan&age=20&sex=男
// {"name":"zhangsan","age":"20","sex":"男"}
```

### POST参数的获取

Express中接收post请求参数需要借助第三方包 body-parser。

- npm install body-parser
- req.body  返回POST请求参数

```js
app.use(bodyParser.urlencoded({ extended: false }));
app.post('/add', (req, res) => {
    res.send(req.body)
})
// extended: false 方法内部使用 duerystring模块处理请求参数的格式
// extended: true 方法内部使用第三方模块 qs处理请求参数的格式
```



## Express路由参数

```js
app.get('/index/:id/:name/:age', (req, res) => {
    res.send(req.params)	// { id:123,name:lisi,age:20 } 
});
// localhost:3000/index/123/lisi/20
```



## 静态资源访问功能

通过Express内置的 **express.static** 可以方便地托管静态文件，例如img、CSS、JavaScript 文件等。

```js
app.use('/static', express.static(path.join(__dirname, 'public')));	//有指定路径
// http://localhost:3000/static/images/kitten.jpg
// http://localhost:3000/static/css/style.css
app.use(express.static(path.join(__dirname, 'public')));	//没有指定路径
// http://localhost:3000/images/kitten.jpg	
// http://localhost:3000/css/style.css
```

## 模板引擎

为了使art-template模板引擎能够更好的和Express框架配合，模板引擎官方在原art-template模板引擎的基础上封装了 **express-art-template** 。

- 使用    **npm install art-template express-art-template**    命令进行安装。

```js
// 使用 express-art-template 模板引擎，渲染模板后缀为 art 的模板
app.engine('art',require('express-art-template'));	
// 模板文件存放的位置，参数一：(默认的)配置项名字，参数二：模板的路径(绝对路径)
app.set('views',path.join(__dirname,'views'));
// 设置模板的默认后缀，参数一：(默认的)配置项名字，参数二：模板的后缀
app.set('view engine','art');
app.get('/',(req,res)=>{
    // 渲染模板
    res.render('index' ,{
        msg:'message'
    });
});
```

###  app.locals 对象

将变量设置到 **app.locals** 对象下面，这个数据在所有的模板中都可以获取到。

```js
app.locals.users= [{
	name:'李四',age:18
},{
    name:'张三',age:38
}]
```

