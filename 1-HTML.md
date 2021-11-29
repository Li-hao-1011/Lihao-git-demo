



# HTML

### 超文本标记语言	Hyper Text Markup Language

标记语言：由标签构成的语言，不是编程语言。

### 标签：

1.围堵标签：有开始标签和结束标签。如 `<html> </html>`	

2.自闭和标签:开始标签和结束标签在一起。如 `<br/>`



##### 1.文件标签

```
html：html文档的根标签。

head：头标签。用于指定html文档的一些属性值。引入外部的资源。

title：标题标签。

body：体标签。
```

html 5中定义该文档是html文档：<!DOCTYPE	html>

##### 2.文本标签

注释： <! --	-->

br：换行。 <br>

h1到h6：标题标签。h1--->h6  字体大小逐渐减小

p：段落标签。<p></p>

hr：显示一条水平线。color颜色	width宽度	size高度	

​			align对齐方式——center居中 left左对齐 right右对齐

b：字体加粗。<strong></strong>

i：字体倾斜。<em></em>

del： 删除线   <del></del>

ins： 下划线    <ins></ins>

font：字体标签（被h5淘汰）。color颜色	size大小	face字体

center：文本居中（被h5淘汰）。<center> </center>

```
<!--	color：rgb(值1，值2，值3)，值的范围：0-255 如： rgb(0,0,255) -->

<!--	color：#值1值2值3，值的范围：00-FF之间	如：#FF00FF	-->

<!--	width： 数值%：占比相对于父元素的比例	-->
```



##### 3.图像标签

<img src="" alt="" title="">

属性：src=""     图片的路径

​			alt="" 	图片错误时显示的替换文本

​			title=""	提示文本，鼠标放到图片上，显示的文字

​			width="" 	给图像设定宽度	px

​			height=""	给图像设定高度	px

​			border=""	给图像设定边框	px

```html
<img src="./img/tv04.jpg" alt="这是个图片">
```

##### 4.列表标签

有序列表：ol —声明有序列表		type 属性     值：1 A a i I

```html
<ol type="A">
    <li>10</li>
     <li>20</li>
     <li>30</li>
     <li>40</li>
 </ol>
```

**无序列表**（重点）：ul —声明无序列表

​		type 属性     值：空心圆：circle  实心圆：disc  实心方块 ：square

```html
<ul type="disc">
     <li>10</li>
      <li>20</li>
     <li>30</li>      
    <li>40</li>
</ul>
```

**自定义列表**（重点）：dl—声明自定义列表   

```html
<!-- <dl> 下面有 <dt> 和 <dd> ,<dt>和<dd>个数没有限制-->
<!-- 经常一个 <dt> 对应多个 <dd>-->
<!-- <dt> 和 <dd> 是并列关系，<dd> 解释说明 <dt> -->
<dl>
    <dt></dt>
    <dd></dd>
    <dd></dd>
</dl>
```

**注意**：<ul></ul>和<ol></ol>之间只能放 li 标签

​			<li></li> 之间相当与一个容器，可以容纳所有元素

##### 5.链接标签

a：定义一个超链接。

属性：	

href：指定访问资源的URL(统一资源定位符)。

target：目标窗口的弹出方式。值：_self：默认值，在当前页面打开 

​														_blank：在新页面中打开

```html
<a href="https://www.baodu.com" target="_self">外部链接</a> <!-- 本页面  外部链接-->
<br/>
<a href="https://www.baodu.com" target="_blank">外部链接</a> 
<!-- 新页面  外部链接-->
<br>
<a href="./2_HTML.html">11</a><!-- 本地链接 -->
<br>
<a href="#">空链接</a><!-- 空链接 -->
<br>
<a href="文件地址">下载链接</a><!-- 下载链接 -->
<br>
<a href="./2_HTML.html"><img src="./img/a.jpg"  width="200" size="150"/></a>
<!-- 图片链接 -->
```

锚点链接

​	在链接文本的 href 属性中，设置属性值为 **#名字**  的形式，

​	找到目标位置的标签，在里面添加一个 id 属性 = **名字** 

```html
<a href="#mubiao">去目标处</a>
<h4 id="mubiao">目标在这儿</h4>
```



##### 6.span和div

没有语义，他们是一个盒子，用来装内容的。

```html
 <span>黑马</span>
 <!-- 一行可以写多个span -->
 <!-- 展示文本信息，无任何样式，行内标签，内联标签 -->
 
 <div>黑马</div>
 <!-- 一行只能写一个div -->
 <!-- div：每一个div占满一整行，无任何样式，块级标签 -->
```

##### 7.语义化标签

html5中为了提高程序的可读性，提供的一些标签。

```
<header>:头部，页眉
<footer>:尾部，页脚
```

#####  8.表格标签

table：定义表格

```
table 的属性：
    border="1" 有无边框
    width="500px" 宽度
    height="400px" 宽度
    cellpadding="0" 单元格和内容之间的距离，默认为1px 
    cellspacing="0" 单元格之间的距离，为0，单元格的线合并为一条
    bgcolor="#FF0000"背景色
    align="center"对齐方式，center 居中  left 左对齐 right 右对齐
```

tr：定义行。

th：表头单元格。自动将内容 加粗 居中

td：定义单元格。

```
合并单元格：
    跨行合并：rowspan——合并列
		rowspan="合并单元格的个数"
    跨列合并：colspan——合并行
    	colspan="合并单元格的个数"
```

**thead：表示表格的头部分。**

**tbody：表示表格的主体部分。**

caption：表格的标题，居中。

tfoot：表示表格的尾部分。

##### 9.表单标签

**表单域**：包含表单元素的区域；

​				<form>会把它范围内的表单元素信息提交给服务器。

表单：用于采集用户输入的数据，用于和服务器进行交互。

```
form:用于定义表单，可以定义一个范围，范围代表采集用户数据的范围 

    属性：
     name: 表单域的名称
     action：指定数据提交的URL
     method：指定数据提交方式
        GET:
         1.请求参数会在地址栏中显示
         2.请求参数的大小有限制
         3.不太安全
       POST:
         1.请求参数会在地址栏中显示，会封装在请求体中（HTTP协议）
         2.请求参数的大小没有限制
         3.较为安全
```

```
 表单项中的数据要想被提交，必须指定其name属性
例：    <form action="#" method="POST">
        用户名：<input name="username" ><br>
        密码：<input name="password" ><br>
        <input type="submit" value="登录">
    </form>
```

表单项标签：

input：输入表单元素 			<input type="">

```tex
	type:
		"text"：文本输入框，为默认值。
				1.placeholder属性指定输入框的提示信息，输入框的内容发生变化则自动清空		placeholder="请输入用户名"	placeholder="请输入密码"
				2.name 文本框的名称
				3.value 文本框的初始值
				4.size 文本框的长度
				5.maxlength 可输入的最大字符
				
		"password"：为密码输入框
				1.name 密码框的名称
				2.value 密码框的初始值
				
		"radio"：单选框
					1.name   	必须一样，才能单选
					2.value  	用来区分传输的值
					3.checked   可以指定默认值	checked="checked"
					
		"checkbox"：多(复)选框
					1.value属性指定其被选中后提交的值
					2.checked属性可以指定默认值	checked="checked" 表示被选中
					3.1.name   	必须一样
										
		"file"：文件域
		"color"：拾色器
		"date"：日期，不带时间
		"datetime-local"：日期，带时间
		"email"：邮箱，提醒邮箱格式
		"number"：数字，只能输入数字
		"hidden": 隐藏域，用于提交一些信息
	—————————————————————————————
		"submit"：提交按钮
		"reset":  重置按钮
		"button"：普通按钮
		"image"：图片提交按钮
				src属性指定图片的路径
	label：指定输入项的文字描述信息
			label的for属性一般会和 input 的 id 属性对应，
				点击了label区域则会让input输入框获取焦点
        例：    <label for="password">
            	密码：<input type="password" name="password" id="password">
           		 </label>

```

###### select：下拉表单元素	(至少包含一对<option>)

```
	name属性：name="province"
	选择多个：添加mutiple  <select name="abc" id="" multiple>
	子元素：option指定列表项
			<option value=""--请选择--></option>
			<option value="1">1</option>           
			<option value="1">2</option>           
			<option value="1">3</option>           
            属性：selected="selected"  则默认选中该选项
```

###### textarea:文本域	<texterae></texterae>

```
cols：列数		cols="10" 
rows：行数 	rows="10"
```



###### 表单中可用到的属性

```
disabled	不可用 
hidden		隐藏
readonly	只读
```

  

# HTML5新特性

#### 结构标签

```
header标签：<header>		头部标签
	1.用于设置页面的标题部分，通常会包含标题、LOGO、导航
    2.通常会放在网页的头部
    3.和div相同，本身没有样式的
nav标签：<nav>				导航标签
article标签：<article>		内容标签
	1.用于定义一个独立的内容区块，比如一篇文章，一个帖子
	2.article标签内部可以嵌套其他的标签，它可以有自己的头部、尾部、主体等
	3.在使用的时候，我们要注意内容的独立性，一个对于独立完整的内容，我们才使用article标签，如果是一段内容则使用section标签

section标签：<section>		块级标签
	1.用来定义文章中的章节
	2.用来定义文档中特定内容的区块，可视为一个区域的分组元素，用来给页面上内的内容分块
	3.section标签可以定义文档的主体内容
	4.给内容分段，给页面分区
aside标签：<aside>			侧边栏标签	

fotter标签：<footer>		尾部标签
	1.通常用于设置一个网页的底部区域，会包含友情链接、版权声明等
    2.通常会放在网页的底部
    3.和div相同

article标签与section标签的区别
	1.语义不同
        article标签更强调的是内容的独立性
        section强调的是内容的关联性
        article标签独立完整的内容 
        section标签是页面的内容分块
    2.相同点
    	本质上都是带有语义化的div
```

<img src="D:\md\imgs\Snipaste_2020-12-14_10-45-02.png" style="zoom:60%;" />

注意：	在IE9中，需要把这些元素转化为块级元素



#### 表单标签

```
form的属性
	action；指表单的发送地址
	method：表单数据发送的方式	get/post

input标签
	用来设置表单中的内容项
	type属性：指定输入内容的类型  默认位text	单行文本框
		属性值：
*			number	限制用户输入必须为数字类型
*			tel		手机号码
*			search	搜索框
			email	限制用户输入必须为Email类型
			url		限制用户输入必须为URL类型
			date	限制用户输入必须为日期类型
			time	限制用户输入必须为时间类型
			month	限制用户输入必须为月类型
			week	限制用户输入必须为周类型
			color	生成一个颜色选择表单
```

```
	name属性：
	value属性：
	required属性：不能为空吗，必填项
			required="required"
*	placeholder属性：（提示文本）表单的提示信息，存在默认值将不显示
			placeholder="请输入用户名"
	autofocus属性：自动获取焦点，页面加载完成自动聚焦到指定表单
			auuofocus="autofocus"
	autocomplete属性：
			当用户在字段开始键入时，浏览器基于之前键入过的值，应该显示出在字段中填写的选项。
			默认已经打开：autocomplete="on"
				关闭：   autocomplete="off"
			条件：需要放在表单内同时加上name属性
				 同时成功提交
*	multiple属性：可以多选文件提交
			multiple="multiple"
	maxlength属性：输入的最大值
	readonly属性：只读
	disabled属性：禁用
	
	
	
	
datalist标签
	H5新增标签	用来建立一个选项列表 
	datalist的内容不会显示在网页上
```



#### 多媒体标签

```
音频：<audio>
	属性：
		autoplay	如果出现该属性，则音频在就绪后马上播放
		controls	如果出现该属性，则向用户显示控件，比如播放按钮
		loop		如果出现该属性，则每当音频结束时重新开始播放
		src			要播放的音频的URL
<audio src="文件地址" controls="controls" ></audio>
```

```html
<!--不同浏览器支持的音频格式不同，解决方案是：为这个浏览器准备多个格式-->
<audio controls="controls">
    <source src="media/snow.mp3" type="audio/mpeg" >
    <source src="media/snow.ogg" type="audio/ogg" >
    您的浏览器不支持播放音频
</audio>
<!--浏览器会执行自己支持播放格式的音频-->
```

![](D:\md\imgs\Snipaste_2020-12-14_10-57-56.png)

------



```
视频：<video>

<video src="文件地址" controls="controls" ></video>
```

```
<!--不同浏览器支持的视频格式不同，解决方案是：为这个浏览器准备多个格式-->
<video controls="controls" width="300px">
    <source src="media/snow.mp4" type="video/mpeg" >
    <source src="media/snow.ogg" type="video/ogg" >
    您的浏览器不支持播放音频
</video>
<!--浏览器会执行自己支持播放格式的音频-->
```

![](D:\md\imgs\video的标签属性.png)



![](D:\md\imgs\Snipaste_2020-12-14_10-57-56.png)

