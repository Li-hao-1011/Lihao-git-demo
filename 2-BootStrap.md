# BootStrap

### 基本概念

```
    概念： 一个前端开发的框架，Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、JavaScript 的，它简洁灵活，使得 Web 开发更加快捷。
        * 框架:一个半成品软件，开发人员可以在框架基础上，在进行开发，简化编码。
     好处：
        1. 定义了很多的css样式和js插件。我们开发人员直接可以使用这些样式和插件得到丰富的页面效果。
        2. 响应式布局。
             * 同一套页面可以兼容不同分辨率的设备。
```

快速入门

```
	1. 下载Bootstrap
	2. 在项目中将这三个文件夹复制
	3. 创建html页面，引入必要的资源文件
```

### 响应式布局

```
	同一套页面可以兼容不同分辨率的设备。
	实现：
		依赖于栅格系统：将一行平均分成12个格子，可以指定元素占几个格子
```

```
	步骤：
        1. 定义容器。相当于之前的table、
            * 容器分类：
                1. container：两边留白
                2. container-fluid：每一种设备都是100%宽度
        2. 定义行。相当于之前的tr   样式：row
        3. 定义元素。指定该元素在不同的设备上，所占的格子数目。样式：col-设备代号-格子数目
            * 设备代号：
                1. xs：超小屏幕 手机 (<768px)：col-xs-12
                2. sm：小屏幕 平板 (≥768px)
                3. md：中等屏幕 桌面显示器 (≥992px)
                4. lg：大屏幕 大桌面显示器 (≥1200px)
```

### CSS样式和JS插件

##### 全局CSS样式

```
 1.按钮：class="btn btn-default"
 2.图片：
    	*  class="img-responsive"：图片在任意尺寸都占100%
	*  图片形状
    	*  <img src="..." alt="..." class="img-rounded">：方形
    	*  <img src="..." alt="..." class="img-circle"> ： 圆形
    	*  <img src="..." alt="..." class="img-thumbnail"> ：相框
 3.表格
    	* table
    	* table-bordered
    	* table-hover
 4.表单
    	* 给表单项添加：class="form-control" 
```

#####  组件

```
	* 导航条
	* 分页条
```



##### 插件

```
	* 轮播图
```

