# JavaScript基础

```
javaScript：一门客户端脚本语言

		运行在客户端浏览器中，每一个浏览器都有javaScript的解析引擎。
		脚本语言：不需要编译，直接就可以被浏览器解析执行了。
		功能：增强用户和html页面的交互过程，可以控制html元素，让页面有动态效果。
		
* JavaScript = ECMAScript + JavaScript自己特有的东西(BOM+DOM)
* ECMAScript：客户端脚本语言的标准

特点：
	脚本编写
	基于对象
	简单
	安全
	动态
	跨平台
	单线程
```

### JS执行机制

```
JS是单线程
H5 提出Web Worker标准，允许JavaScript脚本创建多个线程	
	同步和异步	
	同步任务：同步任务都在主线程上执行，形成一个执行栈。
	异步任务：JS的异步是通过回调函数实现的。
		异步任务一般有3种类型：1.普通事件，如：click、resize
						    2.资源加载：如：load、error
						    3.定时器：包括：setInterval、setTimeout等
	异步任务相关回调函数添加到任务队列中（任务队列也称为消息队列）。
```

![](D:\ps\ps文件\JS事件循环.png)



## 基本语法：

### 		1.与html的结合方式

```
1. 内部JS：
			* 定义<script>，标签体内容就是js代码
2. 外部JS：
			* 定义<script>，通过src属性引入外部的js文件
			例		<script src="my.js"></script>
		* 注意：
				1. <script>可以定义在html页面的任何地方。但是定义的位置会影响执行顺序。
				2. <script>可以定义多个。
3. 行内
	例：<input type="button" value="按钮"	onclick="alert('hello JS')"/>
```

### 		2.注释

```
			1. 单行注释：//注释内容
			2. 多行注释：/*注释内容*/
```

### 3.常用的三种输出方式


```
三种输出方式:
    1.    alert()			弹出警告框
    2.    console.log		 控制台输出
    3.    document.write	  文本打印输出
    
用户输入：prompt("");弹出一个-->输入框，接受用户输入的数据
		prompt 接受的值 是String类型的
```



### 		4.数据类型

```
1. 简单数据类型(基本数据类型)：
   1. number：数字。 
          默认为：0;	包括：整数/小数/NaN(not a number 一个不是数字的数字类型)
              八进制--->0开头
              十六进制--->0x开头
              数字型的最大值：Number.MAX_VALUE
              数字型的最小值：Number.MIN_VALUE
              无穷大： Infinity
              无穷小：-Infinity
              非数值：NaN
          方法：isNaN()--->这个方法用来判断变量是否是数字，返回 true或者false
   2. string：字符串。 字符串  "abc" "a" 'abc'
      属性：length	--->字符串名.length
      		字符串的拼接：用 + 
      		转义字符：（写到 '' 里面）
      				\n		换行符，
      				\\		斜杠 \
      				\'		''单引号
      				\"		""双引号
      				\t		tab 缩进
      				\b		空格
   3. boolean: true和false
      true和false参与数字运算是：true为1	false为0
   4. null：一个对象为空的占位符，返回一个空的对象，	空对象的返回值是 0
   5. undefined：未定义类型。如果一个变量没有给初始化值，则会被默认赋值为undefined
 
 2. 引用数据类型(复杂数据类型)：对象Object
```

#### 栈内存 和 堆内存

```
1. 简单数据类型存储在 栈内存，存放的是 值
	简单数据类型 传参：传递的是 值；
2. 引用数据类型变量 存储在栈内存中，存放的是 地址(十六进制表示的)；真正的对象实例存储在 堆内存
	引用数据类型 传参：传递的是 地址；
```



#### 数据类型的转换

```
转换为字符串：1.toString()
			2.String()	强制转换
	  （重点）3.加号 拼接字符串
转换为数字型（重点）：	1.parseInt(string) 函数，将string型转换为数值型整数
				    2.parseFloat(string) 函数，将string型转换为数值型浮点数
				    3.Number() 强制转换
				    4.js 隐式转换(- * /)  利用算术运算隐式转换为数值型
转化为布尔型：Boolean()
		null、NaN、undefined、0、''  会转化为 false
		其余值都会转换为 true
				    
注意：1.parseInt(string) 和 parseFloat(string)：必须是数字开头的字符串才能将字符串转换为数值，数字后面的字母等全部舍去
	 2.Number() 和 js隐式转换：字符串string必须是纯数子，后面不能跟字母
	  
```



#### typeof检测数据类型

```
typeof 变量名

	null 的数据类型为：Object
```



#### 字面量

```
字面量是在源代码中一个固定值的表示法，就是字面量表示如何表达这个值。
```



### 		5.变量

```
         变量：一小块存储数据的内存空间
			 Java语言是强类型语言，而JavaScript是弱类型语言。
			 强类型：在开辟变量存储空间时，定义了空间将来存储的数据的数据类型。只能存储固定类型的数据
			 弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，可以存放任意类型的数据。
```

### 		6.运算符

​	优先级：

| 优先级 |   运算符   |        顺序         |
| :----: | :--------: | :-----------------: |
|   1    |   小括号   |         ()          |
|   2    | 一元运算符 |      ++  --  !      |
|   3    | 算术运算符 | 先 *  /  %  后 +  - |
|   4    | 关系运算符 |    >  >=  <  <=     |
|   5    | 相等运算符 |  ==  !=  ===  !==   |
|   6    | 逻辑运算符 |  先  &&  后  \|\|   |
|   7    | 赋值运算符 |          =          |
|   8    | 逗号运算符 |          ,          |

##### 	 		1.一元运算符：

​		只有一个运算数的运算符

```text
++，-- ， +(正号)  
	++ --: 自增(自减)
        ++(--) 在前，先自增(自减)，再运算
        ++(--) 在后，先运算，再自增(自减)
	+(-)：正负号
 注意：在JS中，如果运算数不是运算符所要求的类型，那么js引擎会自动的将运算数进行类型转换
             其他类型转number：
             	string转number：按照字面值转换。如果字面值不是数字，则转为NaN（不是数字的数字）
             	boolean转number：true转为1，false转为0	
```

##### 		2. 算数运算符

```
			+ - * / % ...
浮点数有精度问题，不能直接参加运算
```

##### 		3.赋值运算符

```
			= += -+ *= /= %= ...
```

##### 		4.比较运算符

​		值：true 或 false

```
			> < >= <= == ===(全等于) !=
			 比较方式
                  1. 类型相同：直接比较
                       字符串：按照字典顺序比较。按位逐一比较，直到得出大小为止。
                  2. 类型不同：先进行类型转换，再比较
                       ===：全等于。在比较之前，先判断类型，如果类型不一样，则直接返回false
```

##### 		5.逻辑运算符

​		值：true 或 false

```
    && || !
        &&(||) 与(或) (短路)
        ! 非
                 其他类型转boolean：
                       1. number：0或NaN为假， 其他为真
                       2. string：除了空字符串("")，其他都是true
                       3. null & undefined:都是false
                       4. 对象：所有对象都为true
```

##### 		6.三元运算符

```
			语法：
				表达式? 值1:值2;
				判断表达式的值，如果是true则取值1，如果是false则取值2；
```

##### 7.位运算

```
双目运算符：
    位与		&
    位或		|
    位异或		^
注意：把两个操作数所对应的二进制 进行运算

单目运算符
位运算符：~   实现对操作数安慰取反运算，
			操作数是JavaScript类型的常量或变量
```



### 	7.流程控制语句

```
             1. if...else...
             2. switch:
                    * 在java中，switch语句可以接受的数据类型： byte int shor char,枚举(1.5) ,String(1.7)
                        * switch(变量):
                            case 值:
                    * 在JS中,switch语句可以接受任意的原始数据类型
             3. while
             4. do...while
             5. for
```



### 	8.JS特殊语法

```
	1. 语句以;结尾，如果一行只有一条语句则 ;可以省略 (不建议)
    2. 变量的定义使用var关键字，也可以不使用
        * 用： 定义的变量是局部变量
        * 不用：定义的变量是全局变量(不建议)
```

### 9.预解析

```
js引擎运行js 分为两步：(1)预解析	(2)代码执行
        (1).预解析： js 引擎会把js 里面所有的 var 还有 function 提升到作用域的最前面
        (2).代码执行：按照代码书写的顺序从上往下执行
预解析：分为 变量预解析(变量提升)		和 函数预解析(函数提升)
	1.变量预解析(变量提升)：把所有的变量声明提升到当前作用域的最前面，不提升赋值操作
	2.函数预解析(函数提升)：把所有的 函数声明提升到当前作用域的最前面，不调用函数
```

```
面试题：
	f1();
    console.log(c);
    console.log(b);
    console.log(a);
    function f1(){
        var a=b=c=9;	// var a=9;b=9;c=9;		
        console.log(a);
        console.log(b);
        console.log(c);
    }
相当于：function f1(){
        var a;
        a=b=c=9;
        console.log(a);	//9
        console.log(b); //9
        console.log(c); //9
    }
    f1();
    console.log(c); //9
    console.log(b); //9
    console.log(a); //ReferenceError: not defined
```



## JavaScript对象

```
JavaScript中的对象分为3种：自定义对象、内置对象、浏览器对象

JS中 对象是 一组无序的相关属性和方法 的集合
JavaScript语言是基于对象的，不是面向对象的而是把其他语言所创建的对象统一起来

JavaScript中的所有事物都可以称为对象

JavaScript对象由 属性和方法组成
	属性：事物的特征，在对象中用 属性 来表示（常用名词）
	方法：事物的行为，在对象中用 方法 来表示（常用动词）

```

### 创建对象的三种方法

```
1. 利用 字面量 创建对象
        var box = {	//字面量方式
                          name : ‘张三',			//创建属性字段
                          age : 28
                    };
		(1)对象里面的属性或者方法 采取 键值对 的形式：  键:值（属性名 : 属性值）
		(2)多个 属性或者方法中间用逗号隔开  ,
		(3)方法冒号后面跟的是一个匿名函数 
2. 利用 new Object 创建对象
		 var box = new Object();		//new方式
		 box.name = '张三';		//创建属性字段
          box.age = 28;			//创建属性字段
      new关键字可以省略
           var box = Object();		//省略了new关键字
3. 利用 构造函数 创建对象
		构造函数:是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总是与 new 运算符一起使用
		构造函数的语法格式
				function 构造函数名(参数列表){
					this.属性 = 值；
					this.方法 = function(){}
				}
		 使用： new 构造函数名(参数列表);
	new 关键字：	 
		 new 构造函数名(参数列表) 可以在内存中创建一个新的空对象
		 this 就会只想刚才创建的空对象
		 执行构造函数里面的代码，给这个函数赋值
		 返回这个对象
	
	注意：
		 构造函数名 首字母 要大写
		 构造函数不需要 return 
		 属性和方法前面必须 写 this 
		 调用构造函数必须使用 new
		 只要 new 构造函数名() 调用函数就创建一个对象 
		
```

### 使用对象

```
1. 调用对象的属性		
            (1)对象名.属性名
            (2)对象名['属性名']	
2. 调用对象的方法		
			对象名.方法名()

3. 遍历对象
			for..in 语句 ------> 只用于遍历对象，不用于遍历数组
                    for(var k in Object){}	//Object 是对象名
                        k 是属性名			//k 是一个变量
                        Object[k] 是属性值
```

### 内置对象

```
内置对象：就是JS语言自带的一些对象，这些对象供开发者使用，并提供一些常用的 属性和方法	
	Math、Date、Array、String 等
```

##### Math	数学对象

```
1.* 特点：Math对象不用创建，直接使用。 
        Math.方法名();
2.  属性：
        Math.PI
3.方法：
       Math.max(参数列表)：返回参数列表中的最大值
               无参数返回 -Infinity
               有任一参数不能被转换为数值，返回 NaN
       Math.abs(x):取绝对值，参数为字符串则隐式转换为 数字
       Math.random():返回 0 ~ 1 之间的随机 浮点数，含0不含1
       Math.ceil(x)：向上取整。
       Math.floor(x)：向下取整。
       Math.round(x)：把数四舍五入。
               参数的小数部分 > 0.5，舍入到相邻的绝对值大的整数
               参数的小数部分 < 0.5，舍入到相邻的绝对值小的整数
               参数的小数部分 = 0.5，舍入到正无穷大方向上的整数
```

##### Date	日期对象

```
	起始时间为：1970年1月1月
1. 创建：
       var date = new Date(参数列表);
       没有参数：返回当前系统的当前时间 
       参数：
       		2020,11,18		数字型，用 , 分隔
       		'2020-11-18 8:8:8'	字符串型，用 - 分隔年-月-日，用 : 分隔时：分：秒
 2. 方法：
 		.getFullYear():返回年份
 		.getMonth():返回月份，学份从 0 开始到 11 
 		.getDate():返回第几日 
 		.getDay():返回星期几，星期日是0，其他不变
 		.getHours():返回当前的小时
 		.getMinutes():返回当前的分钟
 		.getSeconds():返回当前的秒数
 		
 		.getTime()	.valueOf()	+new Date (直接返回毫秒数)	 Date.now() (H5新增)
 			获取毫秒值(时间戳)，返回当前日期对象描述的时间到1970年1月1日零点的毫秒值差
       toLocaleString()：返回当前date对象对应的时间本地字符串格式
        
```



### 基本对象：

#### 1.Function：

```
	函数(方法)对象
        1. 创建：
              1. var fun = new Function(形式参数列表,方法体);  //忘掉吧
              2. function 方法名称(形式参数列表){
                     方法体
                 }
           	   3. var 方法名 = function(形式参数列表){
                   方法体
              }
        2. 方法：
        3. 属性：
           length:代表形参的个数
        4. 特点：
           1. 方法定义是，形参的类型不用写,返回值类型也不写。
           2. 方法是一个对象，如果定义名称相同的方法，会覆盖
           3. 在JS中，方法的调用只与方法的名称有关，和参数列表无关
           4. 在方法声明中有一个隐藏的内置对象（数组），arguments,封装所有的实际参数
        5. 调用：
           方法名称(实际参数列表);
        6. 返回值
        		return (值);
        	使用return语句的时候函数会停止执行，并返回指定的值
        	
        	this关键字：指 的是它本身，只能在函数体内部使用
        		this主要是实际的调用者
           
           
arguments对象：arguments对象代表正在执行的函数和调用它的参数 
	1. 函数对象的length属性说明函数定义时指定的参数个数 
	   arguments对象的length属性说明调用函数时实际传递的参数个数 
	
	2. arguments对象不能显式创建，函数在运行时并被调用时由JavaScript运行时环境创建并设定各个属性值，其中包括各个参数的值 。
	通常使用arguments对象来验证所传递的参数是否符合函数要求 

	
```

##### 立即执行函数

**写法**： (  function(){}  )()  或者 (  function(){}()  )

**主要作用**： 创建一个独立的作用域。 避免了命名冲突问题

下面三种情况都会刷新页面都会触发 load 事件。

1.a标签的超链接

2.F5或者刷新按钮（强制刷新）

3.前进后退按钮

但是 火狐中，有个特点，有个“往返缓存”，这个缓存中不仅保存着页面数据，还保存了DOM和JavaScript的状态；实际上是将整个页面都保存在了内存里。

所以此时后退按钮不能刷新页面。

此时可以使用 pageshow事件来触发。，这个事件在页面显示时触发，无论页面是否来自缓存。在重新加载页面中，pageshow会在load事件触发后触发；根据事件对象中的persisted来判断是否是缓存中的页面触发的pageshow事件

`注意这个事件给window添加。`



#### 2.Array:数组对象

```
1. 创建：
	1. var arr = new Array(元素列表);
    2. var arr = new Array(默认长度);
    3. var arr = [元素列表];
2. 方法
                
3. 属性
	length:数组的长度
4. 特点：
    1. JS中，数组元素的类型可变的。
    2. JS中，数组长度可变的。
```

##### 遍历数组

1. for(let i=0;i<Array.length;i++)

2. for(let i in Array) 【 i 是索引】

3. for(let item of Array)【 item 是值 】

4. filter/map/reduce 高阶函数

   ```js
   filter(callback)  
   /*	callback必须返回一个boolean值，
   	true（会返回参数n到新的数组中），false（会过滤掉参数n */
   const nums = [10,20,110,200,40,50];
   const numNew1 = nums.filter(function(n){ return n<100 })
   	/* 返回nums中小于100的数，并存放在numNew1数组中 */
   map(callback)
   const numNew2 = numNew1.map(function(n){ return n * 2 })
   	/* 将numNew1中的数 * 2，并存放在numNew1数组中并返回 */
   reduce(callback,number)
   const total = numNew2.reduce(function(preValue n){ return preValue+n },0)
   	/* reduce中参数一是回调函数,参数二是 初始值 */
   /* 第一次：preValue = 0 ，n = 20 
      第二次：preValue = 20，n = 40
      第三次：preValue = 60，n = 80
      第四次：preValue = 140，n = 100
      最终返回 240
   */	
   ```

   

##### 检测是否为数组的两种方式

```
1.   instanceof 运算符
	格式：参数 instanceof Array
2.	 Array.isArray(参数)  返回 true或false		(ES6新增)
```

##### 常用方法

```
	1.添加、删除数组元素方法：
		push(参数)：在数组的末尾添加一个或更多元素，并返回新数组的长度。
		unshift(参数)：向数组的开头添加一个或更多元素，并返回新的长度
                第一个参数：必需。向数组添加的第一个元素
                第二个参数：可选。向数组添加的第二个元素
                参数n:可选。可添加若干个元素
         pop()：删除数组中的最后一个元素并返回删除的元素，没有参数
         shift()：删除数组中的第一个元素并返回删除元素，没有参数
         
	2. 数组排序
		reverse()：颠倒数组中元素的顺序，返回颠倒后的Array对象的引用，会改变原来的数组
    	sort(参数)：用于对数组的元素进行排序，识别不了两位数
    		参数：可选，规定排序的顺序，必须是函数
    				升序函数：function sortNumber(a,b){return a - b}
    				降序函数：function sortNumber(a,b){return b - a}
    		数组在原数组上进行排序，并返回对数组的引用
	3. 数组索引方法
		indexOf(参数)；数组中查找给定元素的 第一个 索引号（从前往后查找）
					如果存在，返回索引号
					如果不存在，返回 -1
		参数：('要查找的字符',起始的位置)：从指定的位置开始查找，并返回元素所在的索引
			起始的位置：可选；不写的话就是从 0索引开始查
		lastIndexOf(参数):数组中查找给定元素的 最后一个 索引号（从后往前查找）
					如果存在，返回索引号
					如果不存在，返回 -1
	4. 数组转换为字符串
		toString([radix])：将数组表示为字符串（按顺序），用逗号分隔
                radix为可选项，表示进制。当对象是数字对象时，该参数起作用
                方法执行后各元素以 , 隔开
		join(参数):将数组中的元素按照指定的分隔符拼接为字符串
			参数可选，不选默认逗号 ,
		
		
	4. 	
		delete 数组名[数组下标]：删除指定元素，保留原来的位置
    	unshift()：向数组的开头添加一个或更多元素，并返回新的长度
    		第一个参数：必需。向数组添加的第一个元素
    		第二个参数：可选。向数组添加的第二个元素
    		参数n:可选。可添加若干个元素
    	concat()：合并（连接）现有数组来创建一个新数组
                不会更改现有数组，它总是返回一个新数组
                可以使用任意数量的数组参数
    	splice()：可用于向数组添加新项	
                返回一个包含已删除项的数组
                直接会对数组进行修改
                第一个参数：定义了应添加新元素的位置（拼接）
                第二个参数：定义应删除多少元素
                其余参数：定义要添加的新元素(可选项)
		slice()：用数组的某个片段切出新数组
                窃取数组的一段元素，窃取部分作为新数组返回，不会对原始数组改变
                第一个参数：为起始位置索引
                第二个参数：为结束位置索引，但并不包含结束位置的参数
                如果省略第二个参数，则窃取到结尾
                和splice有区分：不会对原始数组改变
```



####  3.Boolean

​				  

#### 4.Number



#### 5.String

```
字符串不可变:指得是里面的值不可变，改变的是地址的引用，内存中新开辟了一块空间

方法：
	1. indexOf('要查找的字符',起始的位置)	从指定的位置开始查找，并返回字符所在的索引
		起始的位置：可选；不写的话就是从 0索引开始查
                如果存在，返回索引号
                如果不存在，返回 -1
                
     2. charAt(index)	根据 索引位置 返回字符
     3. charCodeAt(index)	根据 索引位置 返回字符的ASCII码值
     		目的：可以判断用户判断那个 键
     4. str[index]  (H5 新增)  获取指定位置的字符
     5. concat(str1,str2,str3...)	用于连接两个或多个字符串，拼接字符串，等效于 + 
     6. substr(start,length)	从start 位置开始(索引号)，length取的个数
     7. replace('被替换的字符'，'替换为的字符')	替换字符，只会替换第一个字符(被替换的字符)，返回一个新的字符串
     8. split('分隔符')	字符转换为数组
     9. toUpperCase() 	将调用该方法的字符串转为大写形式并返回（如果调用该方法的值不是字符串类型会被强制转换）	在 null 或 undefined类型上调用：出现类型错误 TypeError，不会影响原字符串本身的值
     10. toLowerCase() 会将调用该方法的字符串值转为小写形式，并返回,toLowerCase() 不会影响字符串本身的值
```



#### 6.RegExp:	正则表达式对象

正则表达式（ Regular Expression ）是用于匹配字符串中字符组合的模式。在JavaScript中，正则表达式也是对象。

正则表通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词(替换)，或从字符串中获取我们想要的特定部分(提取)等 。

其他语言也会使用正则表达式，本阶段我们主要是利用JavaScript 正则表达式完成表单验证。

##### 正则表达式的特点

1. 灵活性、逻辑性和功能性非常的强。
2. 可以迅速地用极简单的方式达到字符串的复杂控制。
3. 对于刚接触的人来说，比较晦涩难懂。比如：^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$
4. 实际开发,一般都是直接复制写好的正则表达式. 但是要求会使用正则表达式并且根据实际情况修改正则表达式.   比如用户名:   /^[a-z0-9_-]{3,16}$/

```
1. 正则对象：
    1. 创建
        1. var reg = new RegExp(/正则表达式/);  //构造函数创建
        2. var reg = /正则表达式/;		//字面量创建
	2. 方法	
        1. test(参数):验证指定的字符串(参数)是否符合正则定义的规范	
        test() 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串。
        regexObj.text(str); //regexObj是正则表达式、str 是检测的文本
```

##### 正则表达式的参数

```js
/表达式/[switch]
```

switch（也称为修饰符）按照什么样的模式来匹配.有三种值;

- g：全局匹配
- i：忽略大小写
- gi：全局匹配 + 忽略大小写



##### 正则表达式的组成

一个正则表达式可以由简单的字符构成，比如 /abc/，也可以是简单和特殊字符的组合，比如 /ab*c/ 。其中特殊字符也被称为元字符，在正则表达式中是具有特殊意义的专用符号，如 ^ 、$ 、+ 等。

特殊字符非常多，可以参考： 

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

jQuery 手册：正则表达式部分

在线测试工具：https://c.runoob.com/

##### 边界符

正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符

| 边界符 | 说明                           |
| ------ | ------------------------------ |
| ^      | 表示匹配行首的文本（以谁开始） |
| $      | 表示匹配行尾的文本（以谁结束） |

如果 ^和 $ 在一起，表示必须是**精确匹配**。

##### 字符类

字符类表示有一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内。

#####  [] 方括号

表示有一系列字符可供选择，只要匹配其中一个就可以了

[^] ：表示取反  

```js
//取反 方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false 。
var reg2 = /^[^a-zA-Z0-9]$/;
```



##### 量词符

量词符用来设定某个模式出现的次数。

| 量词  | 说明            |
| ----- | --------------- |
| *     | 重复0次或更多次 |
| +     | 重复1次或更多次 |
| ?     | 重复0次或1次    |
| {n}   | 重复n次         |
| {n,}  | 重复n次或更多次 |
| {n,m} | 重复n到m次      |



##### 预定义类

预定义类指的是**某些常见模式的简写方式**

------

| 预定类 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| \d     | 匹配 0~9之间的任一数字，相当于 [0-9]                         |
| \D     | 匹配 除0~9以外的字符，相当于 [ ^0-9]                         |
| \w     | 匹配任意的字母、数字和下划线，相当于 [A-Za-z0-9_]            |
| \W     | 匹配 除字母、数字和下划线以外的字符，相当于 [ ^A-Za-z0-9_]   |
| \s     | 匹配空格（包含换行符、制表符、空格符等），相当于[\t\r\n\v\f] |
| \S     | 匹配非空格的字符，相当于[ ^\t\r\n\v\f]                       |



##### 正则表达式中的替换 

replace() 方法可以实现替换字符串操作，用来替换的参数可以是一个字符串或者是一个正则表达式
只能替换第一个匹配的字符串

```js
stringObject.replace(regexp/replacement)
/*
	第一个参数：被替换的字符串 或者 正则表达式
	第二个参数：替换为的字符串
	返回值是一个替换完毕的新字符串
*/
var newstr = text.value.replace(/激情|gay/g, '**');
//将text.value 的值根据 正则表达式：/激情|gay/g  ，替换成 ** ，
//并且返回替换好的新字符串
```





```txt
1. 单个字符:[]	表示有一系列字符可供选择，只要匹配其中一个就可以了
    如： [a] [ab] [a-zA-Z0-9]
	注意：取反 方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false
2. 量词符号：
    ?：表示出现0次或1次
    *：表示出现0次或多次
    +：出现1次或多次
    {m,n}:表示 m<= 数量 <= n
    {,n}:最多 n 次
    {m,}:最少 m 次
    {n}:只能出现 n 次
3. 开始、结束符号
        ^:开始
        $:结束
   如果 ^和 $ 在一起，表示必须是精确匹配。
```



```javascript
var rg = /abc/; // 正则表达式里面不需要加引号 不管是数字型还是字符串型
				// /abc/ 只要包含有abc这个字符串返回的都是true
---------------------------------------
var reg1 = /^abc$/; // 精确匹配 要求必须是 abc字符串才符合规范
--------------------------------------
var reg2 = /^abc{3}$/;	// 精确匹配,只让c重复3次，为 abccc 时才为true
--------------------------------------
var reg3 = /^(abc){3}$/; // 精确匹配,小括号表示优先级，为 abcabcabc 时才为true
--------------------------------------
var rg = /[abc]/; // 只要包含有a 或者 包含有b 或者包含有c 都返回为true
-------------------------------------
var rg1 = /^[abc]$/; // 三选一 只有是a 或者是 b  或者是c 这三个字母才返回 true
--------------------------------------
var reg = /^[a-z]$/ //26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围  
------------------------------------
//字符组合
var reg1 = /^[a-zA-Z0-9]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true 
-------------------------------------
//取反 方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false 。
var reg2 = /^[^a-zA-Z0-9]$/;
-------------------------------------
```



#### 7.Global:全局对象

```
		1. 特点：全局对象，这个Global中封装的方法不需要对象就可以直接调用。  
			方法名();
		2. 方法：
			    encodeURI():url编码
			    decodeURI():url解码

			    encodeURIComponent():url编码,编码的字符更多
			    decodeURIComponent():url解码

			    parseInt():将字符串转为数字
			        * 逐一判断每一个字符是否是数字，直到不是数字为止，将前边数字部分转为number
			    isNaN():判断一个值是否是NaN
			        * NaN六亲不认，连自己都不认。NaN参与的==比较全部问false

			    eval():将 JavaScript 字符串，并把它作为脚本代码来执行。
			    	只接受一个参数
            3. URL编码
               传智播客=%E4%BC%A0%E6%99%BA%E6%92%AD%E5%AE%A2
```

### 基本包装类型

```
基本包装类型：把简单数据类型 包装成了 复杂数据类型
			这些基本数据类型就有了 属性和方法
```



## DOM简单学习

```
         功能：控制html文档的内容
         获取页面标签(元素)对象：Element
             document.getElementById("id值"):通过元素的id获取元素对象

         操作Element对象：
            1. 修改属性值：
                1. 明确获取的对象是哪一个？
                2. 查看API文档，找其中有哪些属性可以设置
            2. 修改标签体内容：
                * 属性：innerHTML
                1. 获取元素对象
                2. 使用innerHTML属性修改标签体内容
```

## 事件简单学习

```
JavaScript 使我们有能力创建动态页面，而事件是可以被 JavaScript 侦测到的行为。
简单理解： **触发--- 响应机制**。
功能： 某些组件被执行了某些操作后，触发某些代码的执行。

事件三要素：
    事件源（谁）：触发事件的元素
    事件类型（什么事件）： 例如 onclick 点击事件
    事件处理程序（做啥）：事件触发后要执行的代码(函数形式)，事件处理函数	
 		
 如何绑定事件
	1. 直接在html标签上，指定事件的属性(操作)，属性值就是js代码
		1. 事件：onclick--- 单击事件
	2. 通过js获取元素对象，指定事件属性，设置一个函数
```

## Web API

​	Web API 是浏览器提供的一套操作浏览器功能和页面元素的 API ( BOM 和 DOM )。



## BOM:

#### 概念

```
1. 概念：Browser Object Model 浏览器对象模型
	* 将浏览器的各个组成部分封装成对象。

2. 组成：
	* Navigator：浏览器对象(不太用)
	* Screen：显示器屏幕对象(不太用)
	* Window：窗口对象
	* Location：地址栏对象
	* History：历史记录对象
	
```

#### this指向问题

1. 全局作用域 或者 普通函数中 this 指向全局对象window（定时器里面的 this 也指向window）
2. 方法调用中谁调用 this ，this指向谁
3. 构造函数中 this指向构造函数的实例



#### Window 窗口对象

```
1. 创建	Window对象不需要创建可以直接使用
 	window 对象是浏览器的顶级对象，它具有双重角色
2. 方法
         1. 与弹出框有关的方法：
            alert()	显示带有一段消息和一个确认按钮的警告框。
            confirm()	显示带有一段消息以及确认按钮和取消按钮的对话框。
                * 如果用户点击 确定 按钮，则方法返回true
                * 如果用户点击 取消 按钮，则方法返回false
            prompt()	显示可提示用户输入的对话框。
                * 返回值：获取用户输入的值
         2. 与打开关闭有关的方法：
            close()	关闭浏览器窗口。
                * 谁调用我 ，我关谁
            open()	打开一个新的浏览器窗口
                * 返回新的Window对象
         3. 与定时器有关的方式
            setTimeout()	在指定的毫秒数后调用函数或计算表达式。
                * 参数：
                    1. js代码或者方法对象
                    2. 毫秒值
                * 返回值：唯一标识 id ，用于取消定时器
            clearTimeout()	取消由 setTimeout() 方法设置的 timeout。

            setInterval()	按照指定的周期（以毫秒计）来调用函数或计算表达式。
            clearInterval()	取消由 setInterval() 设置的 timeout。   

3. 属性：
        1. 获取其他BOM对象：
            history
            location
            Navigator
            Screen
        2. 获取DOM对象
            document
4. 特点
        * Window对象不需要创建可以直接使用 window使用。 window.方法名();
        * window引用可以省略。  方法名();
```

##### 窗口加载事件

```
1. onload	当页面内容全部加载完毕再去执行处理函数
	window.onload = function(){}
	或者	window.addEventListener('load',function(){})
	window.onload 传统注册方式只能写一次，会以最后一个 window.onload为准
	如果使用 addEventListener 则没有限制
	
2. DOMContentLoaded		仅当DOM加载完成（IE9以上支持）
	document.addEventListener('DOMContentLoaded',function(){})
注意：
    load 等页面内容全部加载完毕，包含页面 dom元素 图片flash css等等	 
    DOMContentLoaded 是等DOM加载完毕，不包含 图片flash css 等就可以执行，加载速度比 load更快一些
```

##### 调整窗口大小事件

```
window.onresize = function(){}
window.addEventListener('resize',function(){})

window.onresize 是调整窗口大小加载事件，当触发时就调用的处理函数。
注意：
	1.只要窗口大小发生像素变化，就会触发这个事件。
	2.经常用这个事件完成响应式布局
		window.innerWidth 返回当前屏幕的宽度
		window.innerHeigth	返回当前屏幕的高度
```

##### 定时器

```
1. setTimeout() 设置定时器
        该方法用于设置一个定时器，该定时器在定时器到期后执行调用函数
        window.setTimeout(调用函数，[延迟的毫秒数]);
    注意：
        1.window 可以省略
        2.这个调用函数可以直接写函数名、写函数名、采取字符串'函数名()'。第三种不推荐
        3.延迟的毫秒数省略默认是 0 ，如果写必须是毫秒；
        4.经常需要给定时器赋值一个标识符
    调用函数也称为 回调函数 callback ；普通函数则是按照代码顺序直接调用。
    
2. clearTimeout(timeoutID)	停止setTimeout()建立的定时器
		该方法取消先前通过调用 setTimeout() 建立的定时器
		1.window 可以省略
		2.参数 timeoutID 是定时器的标识符
```

```
1. setInterval()  定时器  	
	该方法重复调用一个函数，每隔特定的事件间隔就去调用一次回调函数
	window.setInterval(回调函数，[间隔的毫秒数]);
    注意：
        1.window 可以省略
        2.这个调用函数可以直接写函数名、写函数名、采取字符串'函数名()'。第三种不推荐
        3.延迟的毫秒数省略默认是 0 ，如果写必须是毫秒；
        4.经常需要给定时器赋值一个标识符


2. clearInterval() 	停止 setInterval() 建立的定时器
	该方法取消了先前通过调用 setInterval() 建立的定时器
	1.window 可以省略
    2.参数 timeoutID 是定时器的标识符
```



#### Location 地址栏对象

```
window对象给我们提供了一个 location属性用于获取或设置窗体的URL,并且可以用于解析URL。这个属性返回的是 location 地址栏对象
	URL:统一资源定位符
	URL的一般语法格式：
		protocol://host[:prot]/path/[?query]#fragment
		protocol:通信协议；host：主机(域名)；prot：端口号；
		path：路径；query：参数，通过&符号分隔开；fragment：片段，#后面内容常见于链接
1. 创建(获取)：
		1. window.location
		2. location

2. 方法：
		location.assign()	跟href一样，可以跳转页面（也称为重定向页面）
		location.replace()	替换当前页面，没有历史记录所以不能后退
		location.reload()	重新加载当前文档。相当于刷新按钮或者F5，如果
				若：参数为true强制书信Ctrl+f5
		
3. 属性
		* location.href		设置或返回完整的 URL。
		  location.host 	返回主机（域名）
		  location.port		返回端口号，如果未写返回 空字符串
		  location.pathname	 返回路径
		* location.search	返回参数
		  loaction.hash		返回片段  #后面常见于链接 锚点
```

#### navigator 对象

```
navigator对象包含有关浏览器的信息，有很多属性，最常用的是 userAgent，
1. 创建(获取)：
    1. window.navigator
    2. history
2. 属性：
	navigator.userAgent	该属性返回由客户机发送服务器的 user-agent头部的值
```



#### History 历史记录对象

```
    1. 创建(获取)：
        1. window.history
        2. history

    2. 方法：
         history.back()	加载 history 列表中的前一个 URL。
         history.forward()	加载 history 列表中的下一个 URL。
         history.go(参数)	加载 history 列表中的某个具体页面。
            * 参数：
                * 正数：前进几个历史记录
                * 负数：后退几个历史记录
    3. 属性：
         length	返回当前窗口历史列表中的 URL 数量。
```

## DOM

#### 概念

```
 概念： Document Object Model 文档对象模型
	 将标记语言文档的各个组成部分，封装为对象。可以使用这些对象，对标记语言文档进行CRUD的动态操作
	 
 W3C DOM 标准被分为 3 个不同的部分：
	* 核心 DOM - 针对任何结构化文档的标准模型
            * Document：文档对象
            * Element：元素对象
            * Attribute：属性对象
            * Text：文本对象
            * Comment:注释对象

		   * Node：节点对象，其他5个的父对象
	* XML DOM - 针对 XML 文档的标准模型
	* HTML DOM - 针对 HTML 文档的标准模型
```

#### DOM 事件流

```
事件流 描述的是从页面中接受事件的顺序。
事件 发生时会在元素节点之间按照特定的 顺序传播，这个 传播过程 即 DOM事件流。
DOM事件流分为3个阶段：	
		1. 捕获阶段
		2. 当前目标阶段
		3. 冒泡阶段
```

![](D:\ps\ps文件\DOM事件流.png)

##### 注意：

	1. JS 代码中只能执行 捕获 或者 冒泡 中的一个阶段。
 	2.  onclick 和 attachEvent 只能得到冒泡阶段
 	3. addEventListener( type , listener [ , userCapture ] ) 第三个参数如果是  true ，表示在事件 捕获阶段 调用事件处理程序；如果是  false 不写默认是 false），表示在事件的 冒泡阶段 调用事件处理程序。
 	4. 实际开发中 很少使用事件捕获 ，更关注事件冒泡
 	5. 有些时间没有冒泡阶段，比如：onblur、onfocus、onmouseenter、onmouseleave
 	6. 事件冒泡有时候会带来麻烦，有时候会帮助很巧妙的做某些事件。



#### Document 文档对象

```
	1. 创建(获取)：在html dom模型中可以使用window对象来获取
			1. window.document
			2. document
	2. 方法：
            1. 获取Element对象：
                1. getElementById('id')	： 参数 id 是一个字符串，id一般唯一
					根据id属性值获取元素对象。返回值是元素对象
                2. getElementsByTagName('标签名')：
                	根据元素名称获取元素对象们。
                	返回值：元素对象集合（伪数组，数组元素是元素对象）
                	element.getElementsByTagName('标签名') ：可以获取element对象下面'标签名'的所有元素
                	
                3. getElementsByClassName('类名'): （H5 新增）
                	根据Class属性值获取元素对象们。
                	返回值：元素对象集合（伪数组，数组元素是元素对象）
                4. document.querySelector('选择器')	（H5 新增）
                	返回值：根据指定 选择器 返回第一个元素对象
                5. document.querySelectorAll('选择器')	（H5 新增）
                	返回值：根据指定 选择器 返回所有元素对象集合
                6. getElementsByName(): 
                	根据name属性值获取元素对象们。
                	返回值：元素对象集合（伪数组，数组元素是元素对象）
                	
                7.获取特殊元素（body、html）
                	获取 body元素：document.body   	返回 body 元素对象
                	获取 html元素：document.documentElement		返回html元素对象
             
             2. 创建其他DOM对象：
				createAttribute(name)
            	 createComment()
            	 createElement()
            	 createTextNode()
```

#### Element：元素对象

	1. 获取/创建：
			通过document来获取和创建
	2. 方法：
			1. removeAttribute()：删除属性
			2. setAttribute()：设置属性	


#### 操作元素

JavaScript的 DOM 操作可以改变网页内容、结构和样式，我们可以利用 DOM 操作元素来改变元素里面的内容、属性等。（注意：这些操作都是通过元素对象的属性实现的）。

##### 操作元素内容

```
1.element.innerHTML：（W3C 标准）
	从起始位置到终止位置的全部内容，包括html标签，同时保留空格和换行
2.element.innerText: （不是标准）
	从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉
	
 例子： div.innerHTML = '<strong>今天是：</strong> 2019';
 		p.innerHTML;	返回的是 元素里面的内容
```

##### 操作元素属性

```
1.获取属性的值
	元素对象.属性名
2.设置属性的值
	元素对象.属性名 = 值
例如：、src、href、title、alt等
```

##### 操作表单的属性

```
1.获取属性的值
	元素对象.属性名
2.设置属性的值
	元素对象.属性名 = 值

表单元素中有一些属性如：type、value、disabled、checked、selected，元素对象的这些属性的值是布尔型。

```

##### 操作元素样式属性

```
通过 JS修改元素的大小、颜色、位置等样式；

1. element.style		行内样式操作
	元素对象.style.样式属性 = 值;
	注意：1.JS 里面的样式采取驼峰命名法 比如：fontSize、backgroundColor
		 2.JS 修改 style 样式操作，产生的是 行内样式，css权重比较高
		 
2. element.className	类名样式操作(更改元素的类名)
	className 会直接更改元素的类名，会覆盖原先的类名
	element.className = '原先的类名 新类名';————这样会有两个类名
```

##### 操作属性（包括自定义）

```
1. 获取属性值：
        1. element.属性：获取元素的属性
            * 获取 内置属性值（元素本身自带的属性）
        2. element.getAttribute('属性')：
            * 主要获得自定义的属性
2. 设置属性值：
		1. element.属性 = '值'；
			* 设置内置属性
		2. element.setAttribute('属性','值');
			* 主要设置自定义属性
3. 移除属性
		1. element.removeAttribute('属性')
```

###### H5自定义属性

H5规定自定义属性   **<u>date-</u>**    开头做为属性名并且赋值

```
自定义属性目的：是为了保存并使用数据,有些数据可以保存到页面中而不用保存到数据库中。

设置 H5自定义属性：H5规定自定义属性 data- 开头做为属性名并且赋值

获取 H5自定义属性
	1. 自定义属性获取是通过 getAttribute('属性') 获取。
	2. H5 新增 element.dataset.index  或者 element.dataset['index']  
		只能获取 data-  开头的自定义属性		(IE 11才支持) 
					index是 data- 后面的字符
	dataset 是一个集合，里面存放了所有以 data 开头的自定义属性
例： data-index='1';
	data-list-name = '0';
	element.dataset.index 获取自定义属性 data-index 的值
	element.dataset.listName 获取自定义属性 data-list-name 的值
注意：如果自定义属性里面有多个 -  连接的单词，获取的时候采取 驼峰命名法
```



##### 排他思想

```
如果有同一组元素，我们想要某一个元素实现某种样式， 需要用到循环的排他思想算法：
    1. 所有元素全部清除样式（干掉其他人）
    2. 给当前元素设置样式 （留下我自己）
    3. 注意顺序不能颠倒，首先干掉其他人，再设置自己
    
    例：
    <script>
    var btn = document.getElementsByTagName('button');
    for (var i = 0; i < btn.length; i++) {
        btn[i].onclick=function(){
            for (var j=0;j<btn.length;j++){
                btn[j].style.backgroundColor = '';
            }
            this.style.backgroundColor='pink';
        }
    }
	</script>
```



#### Node：节点对象，其他5个的父对象

```
   	特点：所有dom对象都可以被认为是一个节点
       方法：
           CRUD dom树：
                appendChild()：向节点的子节点列表的结尾添加新的子节点。
                removeChild()	：删除（并返回）当前节点的指定子节点。
                replaceChild()：用新节点替换一个子节点。
        属性：
           parentNode 返回节点的父节点。
```

#### 操作节点

​	一般的，节点至少拥有 nodeType（节点类型）、nodeName（节点名称）、nodeValue（节点值）这三个基本属性。

```
元素节点： nodeType  为 1
属性节点： nodeType  为 2
文本节点： nodeType  为 3 （文本节点包括文字、空格、换行等）

节点操作主要操作的是：元素节点
```

##### 父节点

```
nopde.parentNode		父节点
得到得是离元素最近的父节点（亲爸爸），如果找不到父节点就返回  null
```

##### 子节点

```
1. parentNode.childNodes	（不常用）
		返回包含指定节点的子节点的集合，该集合为及时更新的集合
		注意：返回值里面包含了所有的子节点，包括元素节点，文本节点等
2. parentNode.children 	（常用）		
		返回所有的子元素节点，它只返回子元素节点，其余节点不返回
		
3. parentNode.firstChild	
		返回第一个子节点（包括文本节点），如果找不到父节点就返回  null
4. parentNode.lastChild		
		返回最后一个子节点
5. parentNode.firstElementChild		
		返回第一个元素子节点
6. parentNode.listElementChild		
		返回最后一个元素子节点
```

##### 兄弟节点

```
1. node.nextSibling
		返回当前元素的下一个兄弟节点，找不到返回 null。
2. node.previousSibling	
		返回当前元素上一个兄弟节点，找不到返回 null。
3. node.nextElementSibling
		返回当前元素的下一个兄弟元素节点，找不到返回 null。
4. node.previousElementSibling
		返回当前元素的上一个兄弟元素节点，找不到返回 null。
```

##### 操作节点

```
1.创建节点：document.createElement('tagName')
		创建指定的元素'tagName'，这些元素原先不存在，是根据我们的需求动态生成的
2.添加节点：
	1. node.appendChild(child)
		将一个节点添加到指定父节点的子节点列表 末尾
		node 父级；child 是子级，后面追加元素
	2. node.insertBefore(child,指定元素)
		将一个节点添加到 父节点的指定子节点 前面，
3. 删除节点：
	   node.removeChild(child)
		从DOM中删除一个子节点，返回删除的节点
4. 复制节点（克隆节点）
		node.cloneNode()
		返回调用该方法的节点的一个副本。也称为克隆节点/拷贝节点
		参数：参数为空或者 false，则是浅拷贝，即只克隆复制节点本身，不复制里面的子节点
			 参数为 true，则是深度拷贝，会复制节点以及里面所有的子节点
		
```

###### 三种动态创建元素的区别

```
1. document.write()
2. element.innerHTML()
3. document.createElement()
区别：
	document.write() 是直接将内容写入页面的内容流，但是文档流执行完毕，则他会导致整个页面重绘
	element.innerHTML() 是将内容写入到某个 DOM节点中，不会导致页面重绘，创建多个元素效率更高（采用数组形式，而不是拼接字符串），结构稍微复杂
	document.createElement() 创建多个元素效率低一点，但是结构清晰
总结：不同浏览器下，innerHTML 效率要比 createElement 高
```



## 事件

#### 概念

```
概念：某些组件被执行了某些操作后，触发某些代码的执行。	
	* 事件：某些操作。如： 单击，双击，键盘按下了，鼠标移动了
	* 事件源：组件。如： 按钮 文本输入框...
	* 监听器：代码。
	* 注册监听：将事件，事件源，监听器结合在一起。 当事件源上发生了某个事件，则触发执行某个监听器代码。
	
 // this 指向的是事件函数的调用者 
```

#### 事件对象

```js
eventTarget.onclick = function(event) {}
eventTarget.addEventListener('click',function(event){})
	//event  就是事件对象，event 还可以写成 e 或者 evt
```

官方解释：event对象代表事件的状态，比如：键盘按键的状态、鼠标的位置、鼠标按钮的状态

```
事件发生后，跟时间相关的一系列数据的集合都放到这个对象里，event对象有很多属性和方法

event 是个形参，系统帮助我们设定为事件对象，不需要传递实参过去

当我们注册事件时，event 对象就会被系统自动创建，并依次传递给事件监听器（事件处理函数）

事件对象的兼容性问题 ie 6 7 8通过 window.event 兼容性的写法  e = e || window.event 
```

##### 事件对象常见的属性和方法

```
1. e.target	(属性)返回 触发事件的对象（元素），【点击了那个元素返回那个元素】
    与 this 的区别：this 返回的是 绑定事件的对象（元素），【绑定了那个元素返回那个元素】
2. e.type	(属性)返回 事件的类型，比如：click、mouseover、不带on
3. e.preventDefault()  该方法 阻止 默认事件(默认行为),比如：不让页面跳转
4. 传统注册方式使用这3种方式：
		e.preventDefault()方法	高版本浏览器支持
		e.returnValue;属性		  IE 6-8使用
         return false；	阻止默认行为，没有兼容性问题，特点是return 后面的代码不执行，只限于传统的注册方式


```

##### 阻止事件冒泡的两种方式

```
事件冒泡：开始时由最具体的元素接收，然后逐级向上传播到DOM最顶层节点。

1. e.stopPropagation()	方法阻止事件冒泡

2. e.cancelBubble   (属性)在IE 6-8 中使用（非标准），阻止事件冒泡
			e.cancelBubble = true;    
```

##### 鼠标对象事件

```
event 对象代表事件的状态，跟事件相关的一系列信息的集合，
    	e.clientX：返回鼠标相对于浏览窗口可视区的 X 坐标
    	e.clientY：返回鼠标相对于浏览窗口可视区的 Y 坐标
常用————e.pageX：返回鼠标相对于文档页面的 X 坐标（IE9+支持）
常用————e.pageY：返回鼠标相对于文档页面的 Y 坐标（IE9+支持）
    	e.screenX：返回鼠标相对于电脑屏幕的 X 坐标
    	e.screenY：返回鼠标相对于电脑屏幕的 Y 坐标
```

##### 键盘对象事件

```
event 对象代表事件的状态，跟事件相关的一系列信息的集合，
	e.keyCode：返回该键的 ASCII值
注意：keydown 和 keyup 不区分大小写；keypress区分大小写
```



#### 事件委托

```
事件委托也称为事件代理，在jQuery里面称为事件委派。

事件委托的原理：不是每个节点单独设置监听效果，而是事件监听器设置在其父节点上，然后利用冒泡原理影响每个子节点。（给父节点添加监听器，利用事件冒泡影响每一个子节点）。

事件委托的作用：只操作了一次DOM，提高了程序的性能。
```



#### 常见的事件



1. 点击事件：

   1. onclick：单击事件
   2. ondblclick：双击事件

2. 焦点事件

   1. onblur：失去焦点
   2. onfocus:元素获得焦点

3. 加载事件：

   1. onload：一张页面或一幅图像完成加载。

4. 鼠标事件：

   1. onmousedown	鼠标按钮被按下。
                      定义方法时，定义一个形参接受 event对象
                      event对象的 button属性可以获取鼠标哪个按钮被点击了
   2. onmouseup	鼠标按键被松开。
   3. onmousemove	鼠标被移动。
   4. onmouseover	鼠标移到某元素之上。
   5. onmouseout	鼠标从某元素移开。

5. 键盘事件：

   1. onkeydown	某个键盘按键被按下。	

   2. onkeyup		某个键盘按键被松开。

   3. onkeypress	某个键盘按键被按下并松开。但是它不识别功能键 比如  ctrl、shift、

      注意： 三个事件的执行顺序是：keydown--->keypress--->keyup；
                  keydown 和 keyup 不区分大小写；keypress区分大小写
                  keydown 和 keypress 在文本框里面的特点：它们两个事件触发的时候，文字还没有落入到文本框中

6. 选择和改变

   1. onchange	域的内容被改变。
   2. onselect	文本被选中。

7. 表单事件：

   1. onsubmit	确认按钮被点击。
      				可以阻止表单的提交
      					方法返回 flase,则阻止提交
   2. onreset	重置按钮被点击。

8. 禁止鼠标右键菜单		contextmenu
   		contextmenu主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单

9. 禁止鼠标选中   selectstart 
   		selectstart  禁止选中文字

10. 鼠标滚动事件   scroll
    		div.addEventListener('scroll',function(){})



#### 注册事件（绑定事件）

```
注册事件有两种方式：传统方式 和 方法监听注册方式

	1. 传统方式
			利用 on 开头的事件
			特点：注册事件的唯一性
			同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数会覆盖前面注册的处理函数
	2. 方法监听注册方式
		addEventListener 事件监听方式
          eventTarget.addEventListener(type,listener [,userCapture])
            type：事件类型字符串，比如click、mouseover、注意这里不要带 on
            listener：事件处理函数，事件发生时会调用该监听函数
            userCapture：可选参数，是一个布尔值，默认是 false
		注意：type 事件类型是字符串，必定加引号，而且不加 on
			 同一个元素，同一个事件可以添加多个监听器（事件处理程序）

```

#### 删除事件（解绑事件）

```
传统注册方式删除事件：
		eventTarget.onclick = null;

方法监听注册方式删除事件
		eventTarget.removeEventListener(type,listener[, userCapture])
	例：divs[1].addEventListener('click',fn);  //fu 调用不需要加小括号
		function fu(){
			alert(22);
			divs[1].removeEventListener('click',fn);	//删除事件
		}
	
```



#### 鼠标事件 mouseenter  与 mouseover

- 鼠标移动到元素上就会触发  mouseenter事件，与  mouseover 类似，它们两者之间的差别是：
  - mouseover 鼠标经过自身盒子会触发，经过子盒子还会触发事件，
  - mouseenter 鼠标只经过自身盒子触发，不会冒泡
- 与 mouseenter 搭配   鼠标离开 mouseleave 同样不会冒泡



#### 触屏事件

##### 触屏事件概述 

移动端浏览器兼容性较好，我们不需要考虑以前 JS 的兼容性问题，可以放心的使用原生 JS 书写效果，但是移动端也有自己独特的地方。比如触屏事件 touch（也称触摸事件），Android和 IOS 都有。

touch 对象代表一个触摸点。触摸点可能是一根手指，也可能是一根触摸笔。触屏事件可响应用户手指（或触控笔）对屏幕或者触控板操作。

常见的触屏事件如下：

![](D:\md\imgs\常见得触屏事件.png)

##### 触摸事件对象（TouchEvent）

touchstart、touchmove、touchend 三个事件都会各自有事件对象。

![](D:\md\imgs\触摸事件对象.png)

##### 案例：移动端拖动元素

1. touchstart、touchmove、touchend可以实现拖动元素

2. 但是拖动元素需要当前手指的坐标值 我们可以使用  targetTouches[0] 里面的pageX 和 pageY 

3. 移动端拖动的原理：    手指移动中，计算出手指移动的距离。然后用盒子原来的位置 + 手指移动的距离

4. 手指移动的距离：  手指滑动中的位置 减去  手指刚开始触摸的位置

   拖动元素三步曲：

   （1） 触摸元素 touchstart： 获取手指初始坐标，同时获得盒子原来的位置

   （2） 移动手指 touchmove： 计算手指的滑动距离，并且移动盒子

   （3） 离开手指 touchend:

   `注意： 手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动 e.preventDefault();`

   ```html
   <script>
           var div = document.querySelector('div')
           var startX = 0; //记录 手指的初始坐标
           var startY = 0;
           var x = 0; //记录 盒子原来的位置
           var y = 0;
           div.addEventListener('touchstart', function(e) {
               //手指的初始坐标
               startX = e.targetTouches[0].pageX;
               startY = e.targetTouches[0].pageY;
               //盒子原来的位置
               x = this.offsetLeft;
               y = this.offsetTop;
           })
           div.addEventListener('touchmove', function(e) {
               // 计算手指得阿移动距离
               var moveX = e.targetTouches[0].pageX - startX;
               var moveY = e.targetTouches[0].pageY - startY;
               //移动盒子
               this.style.left = x + moveX + 'px';
               this.style.top = y + moveY + 'px';
               // 阻止屏幕滚动的默认行为
               e.preventDefault();
           })
       </script>
   ```

   

##### classList 属性

classList属性是HTML5新增的一个属性，返回元素的类名。但是ie10以上版本支持。

该属性用于在元素中添加，移除及切换 CSS 类。有以下方法：

**添加类：**

element.classList.add（’类名’）；

```javascript
focus.classList.add('current');
```

**移除类：**

element.classList.remove（’类名’）;

```javascript
focus.classList.remove('current');
```

**切换类：**

element.classList.toggle（’类名’）;

```javascript
focus.classList.toggle('current');
```

`注意:以上方法里面，所有类名都不带点`

##### 案例: 移动轮播图

`移动端轮播图功能和基本PC端一致。` 

1. 可以自动播放图片
2. 手指可以拖动播放轮播图

1.2.2. 案例分析:

1. 自动播放功能
2. 开启定时器
3. 移动端移动，可以使用translate 移动
4. 想要图片优雅的移动，请添加过渡效果


1. 自动播放功能-无缝滚动
2. 注意，我们判断条件是要等到图片滚动完毕再去判断，就是过渡完成后判断
3. 此时需要添加检测过渡完成事件  transitionend 
4. 判断条件：如果索引号等于 3 说明走到最后一张图片，此时 索引号要复原为 0
5. 此时图片，去掉过渡效果，然后移动
6. 如果索引号小于0， 说明是倒着走， 索引号等于2 
7. 此时图片，去掉过渡效果，然后移动
8. 小圆点跟随变化效果
9. 把ol里面li带有current类名的选出来去掉类名 remove
10. 让当前索引号的小li 加上 current   add
11. 但是，是等着过渡结束之后变化，所以这个写到 transitionend 事件里面
12. 手指滑动轮播图
13. 本质就是ul跟随手指移动，简单说就是移动端拖动元素
14. 触摸元素touchstart：  获取手指初始坐标
15. 移动手指touchmove：  计算手指的滑动距离，并且移动盒子
16. 离开手指touchend:   根据滑动的距离分不同的情况
17. 如果移动距离小于某个像素  就回弹原来位置
18. 如果移动距离大于某个像素就上一张下一张滑动。
19. 滑动也分为左滑动和右滑动判断的标准是 移动距离正负 如果是负值就是左滑 反之右滑 
20. 如果是左滑就播放下一张 （index++）
21. 如果是右滑就播放上一张  (index--)



##### 案例：返回顶部

当页面滚动某个地方，就显示，否则隐藏

点击可以返回顶部

案例分析

1. 滚动某个地方显示
2. 事件：scroll页面滚动事件  
3. 如果被卷去的头部（window.pageYOffset ）大于某个数值
4. 点击，window.scroll(0,0) 返回顶部



##### click 延时解决方案

移动端 click 事件会有 300ms 的延时，原因是移动端屏幕双击会缩放(double tap to zoom) 页面。

解决方案：

1. 禁用缩放。 浏览器禁用默认的双击缩放行为并且去掉300ms 的点击延迟。

   ```html
     <meta name="viewport" content="user-scalable=no">
   ```

2. 利用touch事件自己封装这个事件解决300ms 延迟。 

   ​	原理就是：

   1.  当我们手指触摸屏幕，记录当前触摸时间
   2.  当我们手指离开屏幕， 用离开的时间减去触摸的时间
   3.  如果时间小于150ms，并且没有滑动过屏幕， 那么我们就定义为点击

   ```js
   //封装tap，解决click 300ms 延时
   function tap (obj, callback) {
           var isMove = false;
           var startTime = 0; // 记录触摸时候的时间变量
           obj.addEventListener('touchstart', function (e) {
               startTime = Date.now(); // 记录触摸时间
           });
           obj.addEventListener('touchmove', function (e) {
               isMove = true;  // 看看是否有滑动，有滑动算拖拽，不算点击
           });
           obj.addEventListener('touchend', function (e) {
               if (!isMove && (Date.now() - startTime) < 150) {  // 如果手指触摸和离开时间小于150ms 算点击
                   callback && callback(); // 执行回调函数
               }
               isMove = false;  //  取反 重置
               startTime = 0;
           });
   }
   //调用  
     tap(div, function(){   // 执行代码  });
   
   ```

3. 使用插件。fastclick 插件解决300ms 延迟。 

   将   fastclick.js  文件引入进去

   直接复制下列代码

   ```js
   if ('addEventListener' in document) {
               document.addEventListener('DOMContentLoaded', function() {
                   FastClick.attach(document.body);
               }, false);
           }
   ```

##### 插件

1.  确认插件实现的功能
2.  .去官网查看使用说明
3.  .下载插件
4.  打开demo实例文件，查看需要引入的相关文件，并且引入
5.  复制demo实例文件中的结构html，样式css以及js代码



Swiper 插件——中文官网地址： https://www.swiper.com.cn/ 

lsuperslide： http://www.superslide2.com/

l iscroll： https://github.com/cubiq/iscroll

###### 移动端视频插件       zy.media.js

H5 给我们提供了 video 标签，但是浏览器的支持情况不同。
不同的视频格式文件，我们可以通过source解决。
但是外观样式，还有暂停，播放，全屏等功能我们只能自己写代码解决。
这个时候我们可以使用插件方式来制作。
我们可以通过 JS 修改元素的大小、颜色、位置等样式。



## 元素偏移量



### 元素偏移量 offset 系列

offset 翻译过来就是偏移量， 我们使用 offset系列相关属性可以动态的得到该元素的位置（偏移）、大小等。

作用：

1. ​	获得元素距离带有定位父元素的位置
2. ​    获得元素自身的大小（宽度高度）
3.    注意：返回的数值都不带单位

offset系列常用的属性：

| offset 系列属性      | 作用                                                      |
| :------------------- | --------------------------------------------------------- |
| element.offsetParent | 返回该元素带有定位的父元素，如果父级没有定位则返回body    |
| element.offsetTop    | 返回元素相对带有定位父元素上方的偏移                      |
| element.offsetLeft   | 返回元素相对带有定位父元素左边框的偏移                    |
| element.offsetWidth  | 返回自身包括 padding、边框、内容区域的宽度,返回值不带单位 |
| element.offsetHeight | 返回自身包括 padding、边框、内容区域的高度,返回值不带单位 |



#### offset 与 style的区别

![](D:\md\imgs\offset与style的区别.png)

#### 案例：京东放大图

```
公式：
	大图片移动距离 =  遮挡层移动距离 * 大图片最大移动距离   / 遮挡层最大移动距离
```



### 元素可视区  client

client 翻译过来就是客户端，使用 client 系列的相关属性来获取元元素可视区的相关信息。



| client系列属性       | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.clientTop    | 返回元素上边框的大小                                         |
| element.clientLeft   | 返回元素左边框的大小                                         |
| element.clientWidth  | 返回自身包括 padding、内容区的宽度，不含边框，返回值不带单位 |
| element.clientHeight | 返回自身包括 padding 、内容区的高度，不含边框，返回值不带单位 |







### 元素滚动 scroll 系列属性

scroll 翻译过来就是滚动的，使用 scroll系列相关的属性可以动态得得到元素的大小、滚动距离等。

| scroll 系列属性      | 作用                                             |
| -------------------- | ------------------------------------------------ |
| element.scrollTop    | 返回被卷去的上侧距离，返回数值不带单位           |
| element.scrollLeft   | 返回被卷去的左侧距离，返回数值不带单位           |
| element.scrollWidth  | 返回自身实际的宽度，不包含边框，返回数值不带单位 |
| element.scrollHeight | 返回自身实际的高度，不包含边框，返回数值不带单位 |

页面滚动使用：window.scroll(x,y)    -------->(没有单位)



### 页面滚动距离的计算

页面被卷去的头部兼容性问题的解决方案

1. 新方法：window.pageYOffset (被页面卷去的头部)  和 window.pageXOffset (被页面卷去的头部)   **（IE 9 才开始支持）**

   pageXOffset 设置或返回当前页面相对于窗口显示区左上角的 X 位置。pageYOffset 设置或返回当前页面相对于窗口显示区左上角的 Y 位置。

2. 声明了 DTD，使用document.documentElement.scrollTop

3. 未声明 DTD，使用document.body.scrollTop

```
function getScroll(){
	return {
		left: window.pageXOffset || document.documentElement.scrollLeft ||document.body.scrollLeft || 0,
		top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop ||0
	};
}
使用时： getScroll().left
```



### offset、client、scroll总结

| 三大系列大小对比    | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| element.offsetWidth | 返回自身包括 padding、边框、内容区的宽度，返回数值不带单位   |
| element.clientWidth | 返回自身包括 padding、内容区的宽度，不包含边框，返回数值不带单位 |
| element.scrollWidth | 返回自身实际宽度，不含边框，返回数值不带单位1                |



### 动画函数封装

​		核心原理：通过定时器 setInterval() 不断移动盒子的位置

实现步骤：

1. 获得盒子当前位置
2. 让盒子在当前位置加上1个移动距离
3. 利用定时器不断重复这个操作
4. 加一个结束定时器的条件
5. 注意此元素需要添加定位，才能使用   element.style.left

#### 动画函数给不同元素记录不同的定时器

​		如果多个元素都使用这个动画函数，每次都要var 声明定时器。我们可以给不同的元素使用不同的定时器（自己专门用自己的定时器）。

​		核心原理：利用 JS 是一门动态语言，可以很方便的给当前对象添加属性。

```js
 function animate(obj, target) {
            // 当我们不断的点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
            // 解决方案就是 让我们元素只有一个定时器执行
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function() {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';

            }, 30);
        }

```



#### 缓动效果原理

缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来

**核心算法**：每次移动的距离步长 =  (目标值 - 现在的位置)   /  10    

停止的条件是： 让当前盒子位置等于目标位置就停止定时器  


#### 动画函数多个目标值之间移动  

可以让动画函数从 800 移动到 500。

当我们点击按钮时候，判断步长是正值还是负值

​	1.如果是正值，则步长往大了取整    Math.ceil() ---->向上取整

​	2.如果是负值，则步长 向小了取整   Math.floor()  ---->向下取整

#### 动函数添加回调函数 

回调函数原理：函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，当那个函数执行完之后，再执行传进去的这个函数，这个过程就叫做回调。

回调函数写的位置：定时器结束的位置。



## 本地存储

随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常性在本地存储大量的数据，HTML5规范提出了相关解决方案。

### 本地存储特性

1、数据存储在用户浏览器中

2、设置、读取方便、甚至页面刷新不丢失数据

3、容量较大，sessionStorage约5M、localStorage约20M

4、只能存储字符串，可以将对象JSON.stringify() 编码后存储



### window.sessionStorage

1. 生命周期为关闭浏览器窗口

2. 在同一个窗口(页面)下数据可以共享
3. 以键值对的形式存储使用

存储数据：

```javascript
sessionStorage.setItem(key, value)
```

获取数据：

```javascript
sessionStorage.getItem(key)
```

删除数据：

```javascript
sessionStorage.removeItem(key)
```

清空数据：(所有都清除掉)

```javascript
sessionStorage.clear()
```



### window.localStorage

1. 生命周期永久生效，除非手动删除 否则关闭页面也会存在
2. 可以多窗口（页面）共享（同一浏览器可以共享）
3. 以键值对的形式存储使用

存储数据：

```javascript
localStorage.setItem(key, value)
```

获取数据：

```javascript
localStorage.getItem(key)
```

删除数据：

```javascript
localStorage.removeItem(key)
```

清空数据：(所有都清除掉)

```javascript
localStorage.clear()
```



### 案例：记住用户名

如果勾选记住用户名， 下次用户打开浏览器，就在文本框里面自动显示上次登录的用户名

案例分析

1. 把数据存起来，用到本地存储

2. 关闭页面，也可以显示用户名，所以用到localStorage

3. 打开页面，先判断是否有这个用户名，如果有，就在表单里面显示用户名，并且勾选复选框

4. 当复选框发生改变的时候change事件

5. 如果勾选，就存储，否则就移除



# JS高级



## 1. 面向过程与面向对象对比

|      | 面向过程                                                     | 面向对象                                                     |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 优点 | 性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。 | 易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护 |
| 缺点 | 不易维护、不易复用、不易扩展                                 | 性能比面向过程低                                             |

## 2. 对象与类

### 2.1 对象

对象是由属性和方法组成的：是一个无序键值对的集合,指的是一个具体的事物

- 属性：事物的特征，在对象中用属性来表示（常用名词）
- 方法：事物的行为，在对象中用方法来表示（常用动词）

```js
//以下代码是对对象的复习
//字面量创建对象
var ldh = {
    name: '刘德华',
    age: 18
}
console.log(ldh);

//构造函数创建对象
  function Star(name, age) {
    this.name = name;
    this.age = age;
 }
var ldh = new Star('刘德华', 18)//实例化对象
console.log(ldh);	
```



### 2.2 类

- 在 ES6 中新增加了类的概念，可以使用 class 关键字声明一个类，之后以这个类来实例化对象。类抽象了对象的公共部分，它泛指某一大类（class）对象特指某一个，通过类实例化一个具体的对象

#### 2.2.1创建类

1. 通过class 关键字创建类, 类名我们还是习惯性定义首字母大写
2. 类里面有个**constructor 函数**,可以接受传递过来的参数,同时返回实例对象
3. constructor 函数 只要 new 生成实例时,就会自动调用这个函数, 如果我们不写这个函数,类也会自动生成这个函数
4. 多个函数方法之间不需要添加逗号分隔
5. 生成实例 new 不能省略
6. 语法规范, 创建类 类名后面不要加小括号,生成实例 类名后面加小括号, 构造函数不需要加 function



1. 语法:

   ```js
   //步骤1 使用class关键字
   class name {
     // class body
       constructor(uname,age){
           this.uname = uname;
           this.age = age;
       }
   }     
   //步骤2使用定义的类创建实例  注意new关键字
   var xx = new name();
   ```

   

2. 类创建 添加属性和方法

```js
 // 1. 创建类 class  创建一个类
class Star {
    // 类的共有属性放到 constructor 里面 constructor是 构造器或者构造函数
    constructor(uname, age) {
      this.uname = uname;
      this.age = age;
    }//------------------------------------------->注意,方法与方法之间不需要添加逗号
    sing(song) {
      console.log(this.uname + '唱' + song);
    }
}
// 2. 利用类创建对象 new
var ldh = new Star('刘德华', 18);
console.log(ldh); // Star {uname: "刘德华", age: 18}
ldh.sing('冰雨'); // 刘德华唱冰雨
```



### 类的继承

1. 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,如果有就先执行子类的

2. 继承中,如果子类里面没有,就去查找父类有没有这个方法,如果有,就执行父类的这个方法(就近原则)

3. 如果子类想要继承父类的方法,同时在自己内部扩展自己的方法,利用super 调用父类的构造函数,**super 必须在子类 this 之前调用**

4. 

   时刻注意this的指向问题,类里面的共有的属性和方法一定要加this使用.

   - constructor中的 this 指向的是 new 出来的实例对象 
   - **自定义的方法,一般也指向的 new 出来的实例对象**
   - 绑定事件之后 this 指向的就是触发事件的事件源

5. 在 ES6 中类没有变量提升，所以必须先定义类，才能通过类实例化对象!

   

1. 语法：extend关键字

```js
// 父类
class Father{   
} 

// 子类继承父类
class  Son  extends Father {  
}       
```

2. 示例

```js
class Father {
      constructor(surname) {
        this.surname= surname;
      }
      say() {
        console.log('你的姓是' + this.surname);
       }
}

class Son extends Father{  // 这样子类就继承了父类的属性和方法
}
var damao= new Son('刘');
damao.say();      //结果为 你的姓是刘
```

#### 子类使用super关键字访问父类的方法

```js
//定义了父类
class Father {
   constructor(x, y) {
   this.x = x;
   this.y = y;
   }
   sum() {
   console.log(this.x + this.y);
	}
 }
//子元素继承父类
    class Son extends Father {
   		 constructor(x, y) {
    		super(x, y); //使用super调用了父类中的构造函数
    	}
    }
    var son = new Son(1, 2);
    son.sum(); //结果为3
```



## 3. 构造函数和原型

构造函数方法很好用，但是存在**浪费 内存** 的问题。

### 对象的三种创建方式--复习

1. 字面量方式

   ```js
   var obj = {};
   
    var box = {	//字面量方式
                name : ‘张三',			//创建属性字段
                age : 28
            };
   ```

2. new关键字

   ```js
   var obj = new Object();
   
    var box = new Object();		//new方式
       box.name = '张三';		//创建属性字段
       box.age = 28;			//创建属性字段
   ```

3. 构造函数方式

   ```js
   function Person(name,age){
     this.name = name;
     this.age = age;
       this.sing = function(){}
   }
   var obj = new Person('zs',12);
   ```

   

### 静态成员和实例成员

#### 实例成员

实例成员就是构造函数内部通过 **this** 添加的成员 如下列代码中uname age sing 就是实例成员,实例成员只能通过实例化的对象来访问

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
     this.sing = function() {
     console.log('我会唱歌');
    }
}
var ldh = new Star('刘德华', 18);
console.log(ldh.uname);//实例成员只能通过实例化的对象来访问
```



####  静态成员

静态成员 在构造函数本身上添加的成员  如下列代码中 sex 就是静态成员,静态成员只能通过构造函数来访问

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
     this.sing = function() {
     console.log('我会唱歌');
    }
}
Star.sex = '男';
var ldh = new Star('刘德华', 18);
console.log(Star.sex);//静态成员只能通过构造函数来访问
```



### 构造函数原型   (prototype)

构造函数通过原型分配的函数是所有对象所共享的。

JavaScript 规定，每一个构造函数都有一个prototype 属性，指向另一个对象。注意这个prototype就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。

我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法。

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
Star.prototype.sing = function() {
	console.log('我会唱歌');
}
var ldh = new Star('刘德华', 18);
var zxy = new Star('张学友', 19);
ldh.sing();//我会唱歌
```



### 对象原型   (__proto__)

```
1. 对象都会有一个属性 __proto__ 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 原型对象的属性和方法，就是因为对象有 __proto__ 原型的存在。
2. __proto__对象原型和原型对象 prototype 是等价的
3. __proto__对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个非标准属性，因此实际开发中，不可以使用这个属性，它只是内部指向原型对象 prototype
```

![](D:\md\imgs\对象的原型__proto__ 和原型对象prototype.png)



### constructor     构造函数

```
1. 对象原型（ __proto__）和构造函数（prototype）原型对象里面都有一个属性constructor 属性 ，constructor 我们称为构造函数，因为它指回构造函数本身。
2.  constructor 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。
3.  一般情况下，对象的方法都在构造函数的原型对象中设置。如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor  就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。
```

如果我们修改了原来的原型对象,给原型对象赋值的是一个对象,则必须手动的利用constructor指回原来的构造函数如:

```js
 function Star(uname, age) {
            this.uname = uname;
            this.age = age;
        }
        // Star.prototype.sing = function() {
        //     console.log(this.uname + '会唱歌');
        // }
        // Star.prototype.movie = function() {
        //     console.log(this.uname + '会演电影');
        // }
    Star.prototype = {
        constructor: Star,	//手动添加 constructor 属性
        sing: function() {
            console.log(this.uname + '会唱歌');
        },
        movie: function() {
            console.log(this.uname + '会演电影');
        }
    }
    var ldh = new Star('刘德华', 18);
    var zxy = new Star('张学友', 20);
```

### 构造函数、实例、原型对象三者之间的关系

```
1.构造函数的prototype属性指向了构造函数原型对象
2.实例对象是由构造函数创建的,实例对象的__proto__属性指向了构造函数的原型对象
3.构造函数的原型对象的constructor属性指向了构造函数,实例对象的原型的constructor属性也指向了构造函数
```

![](D:\md\imgs\构造函数、实例、原型对象.png)



### 原型链

```
      每一个实例对象又有一个__proto__属性，指向的构造函数的原型对象，构造函数的原型对象也是一个对象，也有__proto__属性，这样一层一层往上找就形成了原型链。
```

![](D:\md\imgs\原型链.png)

原型链和成员的查找机制：

```
当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
如果没有就查找它的原型（也就是 __proto__指向的 prototype 原型对象）。
如果还没有就查找原型对象的原型（Object的原型对象）。
依此类推一直找到 Object 为止（null）。
__proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。
```



### 原型对象中this指向

构造函数中的this   和   原型对象的this,都指向我们   new出来的实例对象

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
var that;
Star.prototype.sing = function() {
    console.log('我会唱歌');
    that = this;
}
var ldh = new Star('刘德华', 18);
// 1. 在构造函数中,里面this指向的是对象实例 ldh
console.log(that === ldh);//true
// 2.原型对象函数里面的this 指向的是 实例对象 ldh
```

### 通过原型为数组扩展内置方法

```js
 Array.prototype.sum = function() {
   var sum = 0;
   for (var i = 0; i < this.length; i++) {
   sum += this[i];
   }
   return sum;
 };
 //此时数组对象中已经存在sum()方法了  可以始终 数组.sum()进行数据的求
```



## 4. 继承

ES6之前没有给我们提供 extends 继承。我们可以通过 **构造函数+原型对象** 模拟实现继承，称为 **组合继承**

### 方法：call()

参数：[参数一]，参数二，参数三，...

- call()可以调用函数
- call()可以修改this的指向,使用call()的时候 参数一是修改后的this指向,
  - 参数2,参数3..使用逗号隔开连接，为普通参数

```js
 function fn(x, y) {
     console.log(this);
     console.log(x + y);
}
  var o = {
  	name: 'andy'
  };
  fn.call(o, 1, 2);//调用了函数此时的this指向了对象o,
```



### 子构造函数继承父构造函数中的属性

1. 先定义一个父构造函数
2. 再定义一个子构造函数
3. 子构造函数继承父构造函数的属性(使用call方法)



### 借用原型对象继承方法

1. 先定义一个父构造函数
2. 再定义一个子构造函数
3. 子构造函数继承父构造函数的属性(使用call方法)

```js
// 1. 父构造函数
function Father(uname, age) {
  // this 指向父构造函数的对象实例
  this.uname = uname;
  this.age = age;
}
Father.prototype.money = function() {
  console.log(100000);		//money()方法
 };
 // 2 .子构造函数 
  function Son(uname, age, score) {
      // this 指向子构造函数的对象实例
      Father.call(this, uname, age);
      this.score = score;
  }
  // 这个是子构造函数专门的方法
  Son.prototype.exam = function() {
    console.log('孩子要考试');

  }
// Son.prototype = Father.prototype;  这样直接赋值会有问题,如果修改了子原型对象,父原型对象也会跟着一起变化
  Son.prototype = new Father();
  // 如果利用对象的形式修改了原型对象,别忘了利用constructor 指回原来的构造函数
  Son.prototype.constructor = Son;      

  var son = new Son('刘德华', 18, 100);
  console.log(son);
```





## 5. ES5新增方法

### 数组方法：

#### 迭代(遍历)数组

forEach()：

```js
array.forEach(function(currentValue,index,arr){})
//	currentValue：数组当前项的值
//	index：数组当前项的索引
//	arr：数组对象本身
//相当于数组遍历的 for循环 没有返回值
```

filter()：

主要用来筛选元素
返回值是一个新数组（所有满足条件的元素）

```js
array.filter(function(currentValue,index,arr){})
//	currentValue：数组当前项的值
//	index：数组当前项的索引
//	arr：数组对象本身
// 返回值是一个新数组
```

some()：

用来检测数组中的元素是否满足指定条件。
返回值是布尔值，找到元素返回 true，找不到就返回 false
如果找到第一个满足条件的元素则终止循环，不在继续查找

```js
array.some(function(currentValue,index,arr){})
//	currentValue：数组当前项的值
//	index：数组当前项的索引
//	arr：数组对象本身
// 在some()里面遇到 return true，就是终止遍历
```



#### some  和  forEach  区别

- 如果查询数组中唯一的元素, 用some方法更合适,在some 里面 遇到 return true 就是终止遍历 迭代效率更高
- 在forEach 里面 return 不会终止迭代

### 字符串方法：

trim()：

方法会从一个字符串的两端删除空白字符

```js
str.trim();
```

trim()方法并不会影响原字符本身，它返回的是一个新的字符串。

### 对象方法：

Object.kets(obj)：

用于获取对象自身所有的属性

```js
Object.keys(obj)
```

- 效果类似 for...in
- 返回值是一个由属性名组成的数组



Object.defineProperty()：

```js
Object.defineProperty(obj,prop,descriptor)
```

1. 参数1：必需。目标对象
2. 参数2：必需。需定义或修改的属性的名字
3. 参数3：必需。目标属性所拥有的特性
   - 参数3 以对象的形式 { } 书写
   - value：设置属性的值。默认为undefined
   - writable：值是否可以重写。true | false（不允许修改），  默认为 false
   - enumerable：目标属性是否可以被枚举。true | false（不允许遍历）默认为 false
   - configurable：目标属性是否可以被删除或是否可以再次修改特性。true | false（不允许删除这个属性）默认为 false



## 6. 函数

### 函数的定义方式

1. 方式1 函数声明方式 function 关键字 (命名函数)

   ```js
   function fn(){}
   ```

2. 方式2 函数表达式(匿名函数)

   ```js
   var fn = function(){}
   ```

3. 方式3 new Function() 

   ```js
   var f = new Function('a', 'b', 'console.log(a + b)');
   f(1, 2);
   
   var fn = new Function('参数1','参数2'..., '函数体')
   注意
   /*Function 里面参数都必须是字符串格式
   第三种方式执行效率低，也不方便书写，因此较少使用
   所有函数都是 Function 的实例(对象)  
   函数也属于对象
   */
   ```

### 函数的调用

```js
/* 1. 普通函数 */
function fn() {
	console.log('人生的巅峰');
}
 fn(); 
/* 2. 对象的方法 */
var o = {
  sayHi: function() {
  	console.log('人生的巅峰');
  }
}
o.sayHi();
/* 3. 构造函数*/
function Star() {};
new Star();
/* 4. 绑定事件函数*/
 btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
/* 5. 定时器函数*/
setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
/* 6. 立即执行函数(自调用函数)*/
(function() {
	console.log('人生的巅峰');
})();
```



### this指向

#### 函数内部的this指向

这些 this 的指向，是当我们调用函数的时候确定的。调用方式的不同决定了this 的指向不同

一般指向我们的调用者。

![](D:\md\imgs\函数中this指向.png)



#### 改变函数内部 this 指向

1. call() 方法

call()方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的 this 指向

应用场景:  经常做继承. 

```js
var o = {
	name: 'andy'
}
 function fn(a, b) {
      console.log(this);
      console.log(a+b)
};
fn(1,2)// 此时的this指向的是window 运行结果为3
fn.call(o,1,2)//此时的this指向的是对象o,参数使用逗号隔开,运行结果为3
/* 继承 */
function Father(uname){
    this.uname = uname;
}
function Son(uname){
    /* Son的实例可以实现Father的属性和方法 */
    Father.call(this,uname);
}
var son = new Son('刘德华');
console.log(son);
```

2. apply() 方法

apply() 方法调用一个函数。简单理解为调用函数的方式，但是它可以改变函数的 this 指向。

应用场景:  经常跟数组有关系

```js
var o = {
	name: 'andy'
}
 function fn(a, b) {
      console.log(this);
      console.log(a+b)
};
fn(1,2)// 此时的this指向的是window 运行结果为3
fn.apply(o,[1,2])//此时的this指向的是对象o,参数使用数组传递 运行结果为3
/* 数组 */
var arr = [a,66,3,99,4];
var max = Math.max.apply(Math,arr);
console.log(max); //打印结果为 99
```



3. bind() 方法

bind() 方法不会调用函数,但是能改变函数内部this 指向,返回的是原函数改变this之后产生的新函数

如果只是想改变 this 指向，并且不想调用这个函数的时候，可以使用bind

应用场景:不调用函数,但是还想改变this指向

```js
 var o = {
 name: 'andy'
 };

function fn(a, b) {
	console.log(this);
	console.log(a + b);
};
var f = fn.bind(o, 1, 2); //此处的f是bind返回的新函数
f();//调用新函数  this指向的是对象o 参数使用逗号隔开
```



4. call、apply、bind三者的异同

- 共同点 : 都可以改变this指向
- 不同点:
  - call 和 apply  会调用函数, 并且改变函数内部this指向.
  - call 和 apply传递的参数不一样,call传递参数使用逗号隔开,apply使用数组传递
  - bind  不会调用函数, 可以改变函数内部this指向.


- 应用场景
  1. call 经常做继承. 
  2. apply经常跟数组有关系.  比如借助于数学对象实现数组最大值最小值
  3. bind  不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向. 



### 严格模式

严格模式（strict mode）：javaScript 除了提供正常模式外，还提供了严格模式（strict mode）。ES5 的严格模式是采用具有限制性 JavaScript变体的一种方式，即在严格的条件下运行 JS 代码。

严格模式在 IE10 以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略。
严格模式对正常的 JavaScript 语义做了一些更改： 

1. 消除了 Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为。

 	2. 消除代码运行的一些不安全之处，保证代码运行的安全。
 	3. 提高编译器效率，增加运行速度。
 	4. 禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class,enum,export, extends, import, super 不能做变量名



#### 开启严格模式

严格模式可以应用到整个脚本或个别函数中。因此在使用时，我们可以将严格模式分为
为脚本开启严格模式  和  为函数开启严格模式   两种情况。

- 情况一 :为脚本开启严格模式

  - 有的 script 脚本是严格模式，有的 script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他  script 脚本文件。

    ```js
    <script>
        (function (){
      //在当前的这个自调用函数中有开启严格模式，当前函数之外还是普通模式
    　　　　"use strict";
           var num = 10;
    　　　　function fn() {}
    })();
    </script>
    //或者 
    <script>
      　"use strict"; //当前script标签开启了严格模式
    </script>
    <script>
      			//当前script标签未开启严格模式
    </script>
    ```

- 情况二: 为函数开启严格模式

  - 要给某个函数开启严格模式，需要把“use strict”;  (或 'use strict'; ) 声明放在函数体所有语句之前。

    ```js
    function fn(){
    　　"use strict";
    　　return "123";
    } 
    //当前fn函数开启了严格模式
    ```



##### 严格模式下 this 指向问题

- 严格模式下，全局作用域中函数中的this是 undefined，（以前全局作用域函数中this指向window）
- 严格模式下，构造函数不加 new 调用，this会报错, new实例化的构造函数this指向创建的对象实例,（以前构造函数不加 new可以调用，当成普通函数，this指向全局对象）
- 严格模式下，定时器中 this 还是指向 window
- 事件、对象还是指向调用者
- 严格模式下，不能使用未声明的变量
- 严格模式下，不允许删除变量

##### 函数变化

- 函数不能有重名的参数
- 函数必须声明在顶层，新版本的JavaScript会引入"块级作用域"（ES6中引入)。为了与新版本接轨不允许在 非函数的代码块内声明函数。
  - 例如：if(){ }、for(){ }

[更多严格模式要求参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)



### 高阶函数

高阶函数是对其他函数进行操作的函数，它接收函数作为参数或将函数作为返回值输出。

```js
function fn1(callback){	callback && callback();	}	//接收函数作为参数

function fn(){	return function(){ }	}	//	将函数作为返回值输出
```



## 7. 闭包

### 变量作用域

变量根据作用域的不同分为两种：全局变量和局部变量。

1. 函数内部可以使用全局变量。
2. 函数外部不可以使用局部变量。
3. 当函数执行完毕，本作用域内的局部变量会销毁。

### 什么是闭包

闭包（closure）指有权访问另一个函数作用域中变量的函数。简单理解就是 ，一个作用域可以访问另外一个函数内部的局部变量。 

![](D:\md\imgs\闭包.png)

### 闭包的作用

作用：**延伸变量的作用范围**。

```js
 function fn() {
   var num = 10;
   function fun() {
       console.log(num);
 	}
    return fun;
 }
var f = fn();
f();  //10
```



### 思考：

```js
 // 没有产生闭包
   var name = "The Window";
   var object = {
     name: "My Object",
     getNameFunc: function() {
    	 return function() {
     		return this.name;
     };
   }
 };
console.log(object.getNameFunc()())
---------------------------------------------------------------------------
// 产生闭包
  var name = "The Window";　　
  var object = {　　　　
    name: "My Object",
    getNameFunc: function() {
        var that = this;
        return function() {
    		return that.name;
    };
  }
};
console.log(object.getNameFunc()())
       
```



## 8. 递归

### 什么是递归

**递归：**如果一个函数在内部可以调用其本身，那么这个函数就是递归函数。简单理解:函数内部自己调用自己, 这个函数就是递归函数

**注意：**递归函数的作用和循环效果一样，由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件  **return**。





## 9. 浅拷贝 和 深拷贝

### 浅拷贝

浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用

ES6新增浅拷贝方法：Object.assign(target,..sourrces)   
	参数一为：拷贝到哪里，参数二为拷贝谁

### 深拷贝

深拷贝拷贝多层，每一级别的数据都会拷贝

```js
// 深拷贝拷贝多层, 每一级别的数据都会拷贝.
var obj = {
    id: 1,
    name: 'andy',
    msg: {
        age: 18
    },
    color: ['pink', 'red']
};
var o = {};
// 封装函数 
function deepCopy(newobj, oldobj) {
    for (var k in oldobj) {
        // 判断我们的属性值属于那种数据类型
        // 1. 获取属性值  oldobj[k]
        var item = oldobj[k];
        // 2. 判断这个值是否是数组
        if (item instanceof Array) {
            newobj[k] = [];
            deepCopy(newobj[k], item)
        } else if (item instanceof Object) {
            // 3. 判断这个值是否是对象
            newobj[k] = {};
            deepCopy(newobj[k], item)
        } else {
            // 4. 属于简单数据类型
            newobj[k] = item;
        }

    }
}
deepCopy(o, obj);
console.log(o);

var arr = [];
console.log(arr instanceof Object);
o.msg.age = 20;
console.log(obj);
```

