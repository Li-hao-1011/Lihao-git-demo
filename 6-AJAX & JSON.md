# AJAX & JSON

```
概念： ASynchronous JavaScript And XML	异步的JavaScript 和 XML

异步和同步：客户端和服务器端相互通信的基础上
    同步：客户端必须等待服务器端的响应。在等待的期间客户端不能做其他操作。
    异步：客户端不需要等待服务器端的响应。在服务器处理请求的过程中，客户端可以进行其他的操作。
    
    Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。 [1] 
	通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
	传统的网页（不使用 Ajax）如果需要更新内容，必须重载整个网页页面。

	提升用户的体验
```

## 应用场景

1.  页面上拉加载更多数据中
2.  列表数据无刷新分页
3.  表单项离开焦点数据验证
4.  搜索框提示文字下拉列表

运行环境

Ajax 技术需要运行在网站环境中才能生效，当前课程会使用Node创建的服务器作为网站服务器。

## 运行原理及实现方式

### Ajax运行原理

Ajax 相当于浏览器发送请求与接收响应的代理人，以实现在不影响用户浏览页面的情况下，局部更新页面数据，从而提高用户体验。

![](D:\md\imgs\Ajax运行原理.png)





### 实现方式

 1. 创建Ajax对象

    ```json
    var xhr = new XMLHttpRequest();
    ```

	2. 告诉Ajax请求方式及请求地址

    ```js
    xhr.open('get','http://example.com');
    ```

	3. 发送请求、

    ```js
    xhr.send();
    ```

	4. 获取服务端给与客户端的响应数据

    ```js
    xhr.onload = function () {
        console.log(xhr.responseText);
    };  // onload()  事件监听
    ```

    

### 服务端响应的数据格式

- 在真实的项目中，服务器端 **大多数情况下会以 JSON 对象作为响应数据的格式** 。当客户端拿到响应数据时，要将 JSON 数据和 HTML 字符串进行拼接，然后将拼接的结果展示在页面中。
- 在 http 请求与响应的过程中，无论是请求参数还是响应内容，如果是对象类型，最终都会被转换为对象字符串进行传输。

```js
JSON.parse();  // 将 json 字符串转换为json对象
```



### 请求参数传递

- GET请求方式

  ```js
  xhr.open('get', 'http://localhost:3000/get?' + parms);
  //需要 拼接 请求参数
  ```

- POST请求方式

  ```js
  xhr.open('get', 'http://localhost:3000/get?');
  // setRequestHeader(); 参数一：报文属性名称，参数二：报文属性值
  xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded') xhr.send('name=zhangsan&age=20');
  
   const bodyParser = require('body-parser');
   app.use(bodyParser.urlencoded({ extended: false })); // bodyParser调用 urlencoded方法
  ```



2.  Content-Type 属性的值是 application/json

   ```js
   {name: 'zhangsan', age: '20', sex: '男'};
   
   // 服务器中 bodyParser调用json方法
   const bodyParser = require('body-parser');
   app.use(bodyParser.json()); // 调用json方法
   ```

   - 在请求头中指定 Content-Type 属性的值是 application/json，告诉服务器端当前请求参数的格式是 json。

```js
JSON.stringify() // 将json对象转换为json字符串
```

注意：get 请求是不能提交 json 对象数据格式的，传统网站的表单提交也是不支持 json 对象数据格式的。



### 获取服务器端的响应

​		在创建ajax对象，配置ajax对象，发送请求，以及接收完服务器端响应数据，这个过程中的每一个步骤都会对应一个数值，这个数值就是ajax状态码。

- 0：请求未初始化(还没有调用open())
- 1：请求已经建立，但是还没有发送(还没有调用send())
- 2：请求已经发送
- 3：请求正在处理中，通常响应中已经有部分数据可以用了
- 4：响应已经完成，可以获取并使用服务器的响应了

```js
xhr.readyState  // 获取Ajax状态码
```

 **onreadystatechange** **事件** 

- 当 Ajax 状态码发生变化时将自动触发该事件。
- 在事件处理函数中可以获取 Ajax 状态码并对其进行判断，当状态码为 4 时就可以通过 xhr.responseText 获取服务器端的响应数据了。

```js
 <script type="text/javascript">
        var xhr = new XMLHttpRequest();
        console.log(xhr.readyState); //0
        xhr.open('get', 'http://localhost:3000/readyState');
        console.log(xhr.readyState); //1
 		xhr.send();
        xhr.onreadystatechange = function() {
            console.log(xhr.readyState); // 2  、// 3   、// 4
            if (xhr.readyState == 4) {
                console.log(xhr.responseText);
            }
        };
    </script>
```

#### 两种获取服务端的响应

![](D:\md\imgs\Ajax获取服务器端响应的两种方式.png)

### Ajax错误处理

1. 网络畅通，服务器端能接收到请求，服务器端返回的结果不是预期结果。

   可以判断服务器端返回的状态码，分别进行处理。xhr.status 获取http状态码

2. 网络畅通，服务器端没有接收到请求，返回404状态码。

   检查请求地址是否错误。

3. 网络畅通，服务器端能接收到请求，服务器端返回500状态码。

   服务器端错误，找后端程序员进行沟通。

4. 网络中断，请求无法发送到服务器端。

   会触发xhr对象下面的onerror事件，在onerror事件处理函数中对错误进行处理。

   ```js
   // 当网络中断时,触发 onerror()事件
   xhr.onerror = function() {
   	alert('网络中断无法发送Ajax请求');
   }	
   ```

- Ajax状态码：表示Ajax请求的过程状态，是ajax对象返回的
- Http状态码：表示请求的处理结果，是服务器端返回的



### **低版本** **IE** **浏览器的缓存 **问题

问题：在低版本的 IE 浏览器中，Ajax 请求有严重的缓存问题，即在请求地址不发生变化的情况下，只有第一次请求会真正发送到服务器端，后续的请求都会从浏览器的缓存中获取结果。即使服务器端的数据更新了，客户端依然拿到的是缓存中的旧数据。

- 解决方案：在请求地址的后面加请求参数，保证每一次请求中的请求参数的值不相同。 

```js
 xhr.open('get', 'http://www.example.com?t=' + Math.random());
// 保证请求参数的值不同
```



## Ajax异步编程

异步和同步：客户端和服务器端相互通信的基础上
    同步：客户端必须等待服务器端的响应。在等待的期间客户端不能做其他操作。
    异步：客户端不需要等待服务器端的响应。在服务器处理请求的过程中，客户端可以进行其他的操作。



## Ajax封装

```js
function ajax(obj) {
            // 存储的是默认值
            var defaults = {
                type: 'get',
                url: '',
                dta: {},
                header: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                },
                success: function() {},
                error: function() {},
            }

            // 使用obj对象中的属性覆盖 defaults对象中的属性
            Object.assign(defaults, obj);

            var xhr = new XMLHttpRequest();
            var params = '';
            for (var attr in defaults.data) {
                params += attr + '=' + defaults.data[attr] + '&';

            }

            params = params.substr(0, params.length - 1);


            // 判断请求方式
            if (defaults.type == 'get') {
                xhr.open(defaults.type, defaults.url + '?' + params);
                xhr.send();
            } else if (defaults.type == 'post') {
                var contentTpye = defaults.header['Content-Type']
                xhr.open(defaults.type, defaults.url);

                xhr.setRequestHeader('Content-Type', contentTpye);
                if (contentTpye == 'application/json') {
                    xhr.send(JSON.stringify(defaults.data));

                } else {
                    xhr.send(params);
                }
            }

            xhr.onload = function() {

                // 获取响应头中的数据；xhr.getResponseHeader()
                // console.log(xhr.getResponseHeader('Content-Type'));
                var contentType = xhr.getResponseHeader('Content-Type');

                // 服务器端返回 的数据
                var responseType = xhr.responseText;

                // contentType.includes('application/json')，判断contentType中是否包含'application/json'
                if (contentType.includes('application/json')) {
                    responseType = JSON.parse(responseType);
                }

                // 当http状态码等于 200 的时候
                if (xhr.status == 200) {
                    // 请求成功
                    defaults.success(responseType, xhr);
                } else {
                    // 请求失败
                    defaults.error(responseType, xhr);
                }
            }
        };
```



## 模板引擎

在客户端的使用：

1. 下载 art-template 模板引擎库文件并在 HTML 页面中引入库文件

2.  准备 art-template 模板

3.  告诉模板引擎将哪一个模板和哪个数据进行拼接

4.  将拼接好的html字符串添加到页面中

5.  通过模板语法告诉模板引擎，数据和html字符串要如何拼接

   ```html
   <head>
       <meta charset="UTF-8">
       <title>Document</title>
       <!-- 1. 引入模板引擎的库文件 -->
       <script src="js/template-web.js"></script>
   </head>
   <body>
       <div id="container">
       </div>
       <!-- 2. 准备art-template模板 -->
       <script id="tpl" type="text/html">
    		<!-- 将数据引入到模板中 -->
           <h1>{{username}} {{age}}</h1>
       </script>
       <script type="text/javascript">
           // 3. 告诉模板引擎将那个数据和那个模板进行拼接
           var html = template('tpl', {
               username: 'zhangsan',
               age: 20,
           });
           document.getElementById('container').innerHTML = html;
       </script>
   </body>
   
   </html>
   ```

   

## ForData对象

FormData对象的作用：

1. 模拟HTML表单，相当于将HTML表单映射成表单对象，自动将表单对象中的数据拼接成请求参数的格式。
2. 异步上传二进制文件



