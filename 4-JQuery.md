# JQuery

## 基础

### 概念

```
概念： 一个JavaScript框架。简化JS开发
	* jQuery是一个快速、简洁的JavaScript框架，是继Prototype之后又一个优秀的JavaScript代码库（或JavaScript框架）。jQuery设计的宗旨	是“write Less，Do More”，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优	化HTML文档操作、事件处理、动画设计和Ajax交互。

	* JavaScript框架：本质上就是一些js文件，封装了js的原生代码而已
```

### 快速入门

```
	1. 下载JQuery
		目前jQuery有三个大版本：
				1.x：兼容ie678,使用最为广泛的，官方只做BUG维护，
					 功能不再新增。因此一般项目来说，使用1.x版本就可以了，
					 最终版本：1.12.4 (2016年5月20日)
				2.x：不兼容ie678，很少有人使用，官方只做BUG维护，
					 功能不再新增。如果不考虑兼容低版本的浏览器可以使用2.x，
					 最终版本：2.2.4 (2016年5月20日)
				3.x：不兼容ie678，只支持最新的浏览器。除非特殊要求，
					 一般不会使用3.x版本的，很多老的jQuery插件不支持这个版本。
					 目前该版本是官方主要更新维护的版本。最新版本：3.2.1（2017年3月20日）
				* jquery-xxx.js 与 jquery-xxx.min.js区别：
					1. jquery-xxx.js：开发版本。给程序员看的，有良好的缩进和注释。体积大一些
					2. jquery-xxx.min.js：生产版本。程序中使用没有缩进体积小一些。程序加载更快
				
	2. 导入JQuery的js文件：导入min.js文件
	3. 使用
		var div1 = $("#div1");
```



### jQuery中的顶级对象$

1.  \$是 jQuery 的别称，在代码中可以使用 jQuery 代替，但一般为了方便，通常都直接使用 $ 。
2.  \$是jQuery的顶级对象，相当于原生JavaScript中的 window。把元素利用$包装成jQuery对象，就可以调用jQuery 的方法。



###  jQuery 对象和 DOM 对象

​	使用 jQuery 方法和原生JS获取的元素是不一样的，总结如下 : 

1. 用原生 JS 获取来的对象就是 DOM 对象
2. jQuery 方法获取的元素就是 jQuery 对象。
3. jQuery 对象本质是： 利用$对DOM 对象包装后产生的对象（伪数组形式存储）。

> 注意：
>
> 只有 jQuery 对象才能使用 jQuery 方法，DOM 对象则使用原生的 JavaScirpt 方法。



### JQuery对象和JS对象区别与转换

```
	1. JQuery对象在操作时，更加方便。
    2. JQuery对象和js对象方法不通用的.
    3. 两者相互转换
        * jq -- > js : jq对象[索引] 或者 jq对象.get(索引)
        * js -- > jq : $(js对象)
```

```js
//例子
// 1.DOM对象转换成jQuery对象，方法只有一种
var box = document.getElementById('box');  // 获取DOM对象
var jQueryObject = $(box);  // 把DOM对象转换为 jQuery 对象

// 2.jQuery 对象转换为 DOM 对象有两种方法：
//   2.1 jQuery对象[索引值]
var domObject1 = $('div')[0]

//   2.2 jQuery对象.get(索引值)
var domObject2 = $('div').get(0)
```



###  选择器

#### 基本操作学习：

1. 事件绑定
   1.获取b1按钮
            $("#b1").click(function(){
                alert("abc");
            });

2. 入口函数

   ```js
   // 第一种: 简单易用。
   $(function () {   
       ...  // 此处是页面 DOM 加载完成的入口
   }) ; 
   
   // 第二种: 繁琐，但是也可以实现
   $(document).ready(function(){
      ...  //  此处是页面DOM加载完成的入口
   });
   ```

   window.onload  和 $(function) 区别

   - window.onload 只能定义一次,如果定义多次，后边的会将前边的覆盖掉
   - $(function)可以定义多次的。

   总结：

   1. 等着 DOM 结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery 帮我们完成了封装。
   2. 相当于原生 js 中的 DOMContentLoaded。
   3. 不同于原生 js 中的 load 事件是等页面文档、外部的 js 文件、css文件、图片加载完毕才执行内部代码。
   4. 更推荐使用第一种方式。

3. 样式控制：css()方法

   ​	$("#div1").css("background-color","red");
   ​    $("#div1").css("backgroundColor","pink");

#### 隐式迭代

```js
// 遍历内部 DOM 元素（伪数组形式存储）的过程就叫做隐式迭代。
// 对相同的 DOM 元素做相同的操作
// 简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用。
$('div').hide();  // 页面中所有的div全部隐藏，不用循环操作
```

#### jQuery 里面的排他思想

```javascript
// 想要多选一的效果，排他思想：当前元素设置样式，其余的兄弟元素清除样式。
$(this).css(“color”,”red”);
$(this).siblings(). css(“color”,” ”);
```

   

#### 选择器的分类

##### 基本选择器

```
    1. 标签选择器（元素选择器）
        语法： $("html标签名") 获得所有匹配标签名称的元素
    2. id选择器 
        语法： $("#id的属性值") 获得与指定id属性值匹配的元素
    3. 类选择器
        语法： $(".class的属性值") 获得与指定的class属性值匹配的元素
    4. 并集选择器
        语法： $("选择器1,选择器2....") 获取多个选择器选中的所有元素
    5. 交集选择器
    	语法： $('li.current') 	获取交集元素
   	6. 全选选择器
   		$('*')		匹配所有元素
```

##### 层级选择器

```
 	1.后代选择器
    	语法： $("A B ") 选择A元素内部的所有B元素

 	2. 子选择器
     	语法： $("A > B") 选择A元素内部的所有B子元素
```

##### 属性选择器

```
			1. 属性名称选择器 
				语法:$("A[属性名]") 包含指定属性的选择器
			2. 属性选择器
				语法:$("A[属性名='值']") 包含指定属性等于指定值的选择器
			3. 复合属性选择器
				语法:$("A[属性名='值'][]...") 包含多个属性条件的选择器
			4.$("A[属性名!='值']")  不含有指定元素
			5.$("A[属性名^='值']")  以某些值开始的元素
			6.$("A[属性名$='值']")	以某些值结尾的元素
			7.$("A[属性名*='值']")	包含某些值的元素
```

##### 过滤选择器(筛选选择器)

```
			1. 首元素选择器 
				* 语法： :first 获得选择的元素中的第一个元素
			2. 尾元素选择器 
				* 语法： :last 获得选择的元素中的最后一个元素
			3. 非元素选择器
				* 语法： :not(selector) 不包括指定内容的元素
			4. 偶数选择器
				* 语法： :even 偶数，从 0 开始计数
			5. 奇数选择器
				* 语法： :odd 奇数，从 0 开始计数
			6. 等于索引选择器
				* 语法： :eq(index) 指定索引元素
			7. 大于索引选择器 
				* 语法： :gt(index) 大于指定索引元素
			8. 小于索引选择器 
				* 语法： :lt(index) 小于指定索引元素
			9. 标题选择器
				* 语法： :header 获得标题（h1~h6）元素，固定写法
```

![](D:\md\imgs\筛选选择器.png)

过滤方法(过滤方法)
![](D:\md\imgs\jQuery筛选方法.png)

返回指定祖先元素：  parents("选择器")		





##### 表单过滤选择器

```
			1. 可用元素选择器 
				* 语法： :enabled 获得可用元素
			2. 不可用元素选择器 
				* 语法： :disabled 获得不可用元素
			3. 选中选择器 
				* 语法： :checked 获得单选/复选框选中的元素
			4. 选中选择器 
				* 语法： :selected 获得下拉框选中的元素
```

### DOM操作

##### 内容操作

```
	1. html(): 获取/设置元素的标签体内容   
			<a><font>内容</font></a>  --> <font>内容</font>
	2. text(): 获取/设置元素的标签体纯文本内容   
			<a><font>内容</font></a> --> 内容
	3. val()： 获取/设置元素的value属性值
```



##### CSS样式操作

jQuery 可以使用 css 方法来修改简单元素样式； 也可以操作类，修改多个样式。

​	常用以下三种形式 : 

```javascript
// 1.参数只写属性名，则是返回属性值
var strColor = $(this).css('color');

// 2.  参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号
$(this).css(''color'', ''red'');

// 3.  参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号
$(this).css({ "color":"white","font-size":"20px"});

```

​	注意：css() 多用于样式少时操作，多了则不太方便。



##### 属性操作

###### 通用属性操作

```
    1. attr(): 获取/设置元素的属性(值)
    2. removeAttr():删除属性
    3. prop():获取/设置元素的属性
    4. removeProp():删除属性
    5. 数据缓存 data()
    	data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构。一旦页面刷新，之前存放的数据都将被移除。 
    	注意：同时，还可以读取 HTML5 自定义属性  data-index ，得到的是数字型。
      
   * attr和prop区别？
     1. 如果操作的是元素的固有属性，则建议使用prop()
     2. 如果操作的是元素自定义的属性，则建议使用attr()	
```

###### 对class属性操作

```
        1. addClass():添加class属性
        2. removeClass():删除class属性
        3. toggleClass():切换class属性
                * toggleClass("one"): 
                * 判断如果元素对象上存在class="one"，则将属性值one删除掉。  如果元素对象上不存在class="one"，则添加
//注意：不用写 .  ，直接写类名
```

注意：

1. 设置类样式方法比较适合样式多时操作，可以弥补css()的不足。
2. 原生 JS 中 className 会覆盖元素原先里面的类名，jQuery 里面类操作只是对指定类进行操作，不影响原先的类名。



##### CRUD操作

创建：

```js
$("<li></li>")     // 动态的创建了一个<li>
```

内部添加：（父子关系）

```js
element.append("内容")	// 把内容放入到匹配元素内部最后面
element.prepend("内容")	// 把内容放入匹配元素内部最前面
```

外部添加：（兄弟关系）

```js
element.after("内部")		// 把内容放入目标元素后面
element.before("内部")	// 把内容放入目标元素前面
```

删除元素：

```js
element.remove()		// 删除匹配的元素(本身) 
element.empty()			// 删除匹配的元素集合中所有的子节点
element.html("")		// 清空匹配的元素内容
```



```
1. append():父元素将子元素追加到末尾
	对象1.append(对象2): 将对象2添加到对象1元素内部，并且在末尾
2. prepend():父元素将子元素追加到开头
	对象1.prepend(对象2):将对象2添加到对象1元素内部，并且在开头
3. appendTo():
	对象1.appendTo(对象2):将对象1添加到对象2内部，并且在末尾
4. prependTo()：
	对象1.prependTo(对象2):将对象1添加到对象2内部，并且在开头
5. after():添加元素到元素后边
	对象1.after(对象2)： 将对象2添加到对象1后边。对象1和对象2是兄弟关系
6. before():添加元素到元素前边
	对象1.before(对象2)： 将对象2添加到对象1前边。对象1和对象2是兄弟关系
7. insertAfter()
	对象1.insertAfter(对象2)：将对象1添加到对象2后边。对象1和对象2是兄弟关系
8. insertBefore()
	对象1.insertBefore(对象2)： 将对象1添加到对象2前边。对象1和对象2是兄弟关系
	
9. remove():移除元素
	对象.remove():将对象删除掉
10. empty():清空元素的所有后代元素。
	对象.empty():将对象的后代元素全部清空，但是保留当前对象以及其属性节点
```

##### jQuery尺寸、位置操作

###### jQuery尺寸

<img src="D:\md\imgs\jQuery尺寸操作.png" style="zoom:150%;" />

###### jQuery 位置

<img src="D:\md\imgs\jQuery位置offset.png" style="zoom:150%;" />

<img src="D:\md\imgs\jQuery位置position.png" style="zoom:150%;" />

<img src="D:\md\imgs\jQuery位置scroll.png" style="zoom:150%;" />





## 高级

### 动画

三种方式显示和隐藏元素

##### 默认显示和隐藏方式

```
1. show([speed,[easing],[fn]])：显示
	1. 参数：
		1. speed：动画的速度。三个预定义的值("slow","normal", "fast")或表示动画时长的毫秒数值(如：1000)
		2. easing：用来指定切换效果，默认是"swing"，可用参数"linear"
			* swing：动画执行时效果是 先慢，中间快，最后又慢
			* linear：动画执行时速度是匀速的
		3. fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

2. hide([speed,[easing],[fn]])：隐藏
3. toggle([speed],[easing],[fn])：显示和隐藏(切换)
```

#####  滑动显示和隐藏方式   

```
1. slideDown([speed],[easing],[fn])：显示
2. slideUp([speed,[easing],[fn]])：隐藏
3. slideToggle([speed],[easing],[fn])：显示和隐藏(切换)
```

##### 淡入淡出显示和隐藏方式

```
1. fadeIn([speed],[easing],[fn])：显示
2. fadeOut([speed],[easing],[fn])：隐藏
3. fadeToggle([speed,[easing],[fn]])：显示和隐藏(切换)

4. fadeTo(speed,opacity,[easing],[fn])：
		修改透明度  speed 和 opacity要必须写
         opacity 为：0~1 之间
```



##### 自定义动画

自定义动画非常强大，通过参数的传递可以模拟以上所有动画，

方法为：

```js
animate(params,[speed],[easing],[fn]);
```

​	语法规范如下:
![](D:\md\imgs\animate.png)



##### 停止动画排队

​	动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。

​	停止动画排队的方法为：stop() ; 

- stop() 方法用于停止动画或效果。
- stop() 写到动画或者效果的前面， 相当于停止结束上一次的动画。

​        总结: 每次使用动画之前，先调用 stop() ,在调用动画。



### 遍历

##### js的遍历方式

```
* for(初始化值;循环结束条件;步长)
```

##### jq的遍历方式

```
1. jq对象.each(callback)
	1. 语法：
		jquery对象.each(function(index,element){});
			* index:就是元素在集合中的索引
			* element：就是集合中的每一个元素对象，是js对象，不是jq对象

			* this：集合中的每一个元素对象
    2. 回调函数返回值：
        * true:如果当前function返回为false，则结束循环(break)。
        * false:如果当前function返回为true，则结束本次循环，继续下次循环(continue)
        
2. $.each(object, [callback])
3. for..of: jquery 3.0 版本之后提供的方式
			for(元素对象 of 容器对象)
```





### 事件绑定

##### 1. jquery**标准的绑定方式**

```js
//单个事件注册
jq对象.事件方法(回调函数)；
* 注：如果调用事件方法，不传递回调函数，则会触发浏览器默认行为。
			* 表单对象.submit();//让表单提交
```

##### 2. on绑定事件/off解除绑定

```js
* jq对象.on({"事件名称":回调函数,"事件名称":回调函数,...})
	//	(1). on可以绑定1个或者多个事件处理程序
    //   (2). on可以实现事件委托（委派）
           	/* 给ul 里面的 a 绑定click事件 
			$("ul").on("click", "a", function() {
                $(this).parent().remove();
            })*/
    //   (3). on可以给未来动态创建的元素绑定事件

* jq对象.one()	//只能触发事件一次
           
* //解除事件
    jq对象.off("事件名称")
	* 如果off方法不传递任何参数，则将组件上的所有事件全部解绑

* //自动触发事件
  1.  jq对象.trigger("事件")	//会触发元素的默认行为
  2.  jq对象.事件()		//会触发元素的默认行为
  3.  jq对象.triggerHandler("事件")		//不会触发元素的默认行为
```

##### 3. 事件切换：toggle

```
* jq对象.toggle(fn1,fn2...)
	* 当单击jq对象对应的组件后，会执行fn1.第二次点击会执行fn2.....
	* 注意：1.9版本 .toggle() 方法删除,jQuery Migrate（迁移）插件可以恢复此功能。
<script src="../js/jquery-migrate-1.0.0.js" type="text/javascript" charset="utf-8"></script>
```

##### 4.jQuery事件对象

```js
element.on(events,[selector],function(event){});
```

阻止默认行为：event.preventDefault()  或者  return  false

阻止冒泡：event.stopPropagation()



### jQuery拷贝对象

如果把某个对象拷贝（合并）给另外一个对象使用，此时可以使用 $.extend() 方法

x1$.extend([deep],target,object1,[objectN])2/*3    1. deep:如果设为 true为深拷贝，默认为false 浅拷贝4    2. target:要拷贝的目标对象5    3. object1:待拷贝到第一个对象的对象6    4. objectN:待拷贝到第N个对象的对象7    5. 浅拷贝是把被拷贝的对象 复杂数据类型中的地址拷贝给目标对象，修改目标对象会影响被拷贝对象8*/js

​	

### jQuery多库共存

问题：jQuery使用$作为标识符，随着jQuery的流行，其他js库也会用这种$作为标识符，这样会引起冲突

jQuery解决方案：

1. 把里面的 $ 符号 统一改为 jQuery。比如 jQuery("div")
2. jQuery变量规定新的名称：$.noConflict()       var xx = $.noConflict()





### 插件

​	jQuery插件常用的网站：

1. jQuery插件库：http://www.jq22.com
2. jQuery之家：http://www.htmleaf.com



#### 图片懒加载

​	图片使用延迟加载在可提高网页下载速度，也能帮助减轻服务器负载

​	当我们页面滑动到可视区域，再显示图片

​	使用 jQuery插件库 EasyLazyload ,注意，此时的js文件和js调用必须写到DOM元素（图片）最后面











```
插件： 增强JQuery的功能
 1. 实现方式：
     1. $.fn.extend(object) 	(jQuery对象进行方法扩展)
         * 增强通过Jquery获取的对象的功能  $("#id")

      2. $.extend(object)		(jQuery对象进行方法扩展)
         * 增强JQeury对象自身的功能  $/jQuery
```

```
        //定义jQuery的对象插件
        //jQuery对象进行方法扩展
        $.fn.extend({
            check: function() {
                //让复选框选中
                this.prop("checked", true);
            },
            uncheckFn: function() {
                //让复选框不选中
                this.prop("checked", false);
            }
        });
    $("input[type='checkbox']").check();
```

```
 $.extend({
            max: function(a, b) {
                return a >= b ? a : b;
            },
            min: function(a, b) {
                return a <= b ? a : b;
            }
        });
        var max = $.max(2, 3);
        alert(max);
```

