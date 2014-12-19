# 五. Bootstrap 最佳实践

本文档基于Bootstrap 3.x
> <small><cite>Yu Chen (2014/10/24)</cite></small>

## I 基本原则

- Bootstrap 3遵循的设计原则是:**移动优先**，所以如果要扩展，请遵循这个原则
- 不要重复造轮子，使用前先尽量了解Bootstrap，使用时优先使用Bootstrap自带的工具类、功能、组件或者组件组合
- Bootstrap 3是为现代浏览器打造的，对IE的支持从IE8-11(IE7非官方支持)
- 适用网站类型：后台管理系统，快速模型，企业官网

## II 开始使用

### 1. 基础设置
- 让你的页面适应各种设备:
	
   `<meta name="viewport" content="width=device-width, initial-scale=1[, user-scalable=no]">`
- 使用HTML5文档类型: `<!DOCTYPE html>`

### 2. IE的问题
- Bootstrap不支持老的IE兼容模式，所以，确保使用最新的文档模式:
  
	`<meta http-equiv="X-UA-Compatible" content="IE=edge">`
- IE8下需要使用Respond.js来支持媒体查询语句。出于浏览器安全原因，Respond.js需要在服务器环境下才生效

### 3. CSS部分

#### 排版

- 使用h1-h6来表示标题，而不是通过自定义的class

#### 栅格系统

- 栅格系统由container/row/column三部分组成
- 因为`padding`的原因，`.container`和`.container-fluid`都不可嵌套使用
- `.row`必须被包含在`.container`或`.container-fluid`之内
- **只有在需要多列布局时需要栅格系统**，下面的代码是没有必要的，因为H4本来就占据一整行:
	
	```
	<div class="row">
	  <div class="col-md-12">
	    <h4>H4本来就占据整行，不需要使用栅格系统</h4>
	  </div>
	</div>
	```
- 多列的内容需要出现在列内，即`.col-*-*`内
- 只有列才能是行(`.row`)的直接子元素
	
	```
	<!-- 正确的嵌套 -->
	<div class="row">
	  <div class="col-sm-9">
	    Level 1: .col-sm-9
	    <div class="row">
	      <div class="col-xs-8 col-sm-6">
	        Level 2: .col-xs-8 .col-sm-6
	      </div>
	      <div class="col-xs-4 col-sm-6">
	        Level 2: .col-xs-4 .col-sm-6
	      </div>
	    </div>
	  </div>
	</div>
	<!-- 错误的嵌套 -->
	<div class="row">
		<div class="row">
		  <div class="col-sm-9">
		    Level 1: .col-sm-9
		    Level 2: .col-sm-9
		  </div>
		</div>
	  <div class="col-sm-9">
	    Level 1: .col-sm-9
	    <div class="col-xs-8 col-sm-6">
	      Level 2: .col-xs-8 .col-sm-6
	    </div>
	    <div class="col-xs-4 col-sm-6">
	      Level 2: .col-xs-4 .col-sm-6
	    </div>
	  </div>
	</div>
	```
- 当大屏与小屏的布局一样时，使用小屏的布局，如大屏与中屏的布局相同，使用`.col-md-*`而不是`.col-lg-*`:
	
	```
	<div class="row">
	  <div class="col-md-3">3</div><div class="col-md-9">9</div>
	</div>
	```
- 当大屏与小屏布局不一样时，同时使用不同的列布局
	
	```
	<!-- 小屏幕时，为两行，第一行占据一整行，第二行占据一半；大屏时，为2:1布局 -->
	<div class="row"> 
		<div class="col-xs-12 col-md-8">.col-xs-12 .col-md-8</div> 
		<div class="col-xs-6 col-md-4">.col-xs-6 .col-md-4</div> 
	</div>
	```
- 不要为表单元素使用栅格系统
- 避免多层嵌套的栅格系统布局，尽量控制在3层以内

#### 表格

- 给`<table>`加上`.table`类
- 将表头放在`<thead>`中，将内容放在`<tbody>`中
- 要实现小屏幕上表格的正常显示，在`<table>`之外再嵌套一层`.table-responsive
	
	```
	<div class="table-responsive">
	  <table class="table">
	    ...
	  </table>
	</div>
	```

#### 表单

- 使用`disabled`属性来禁用表单域
- 为每个表单控件添加相应的`label`
- 行内表单只能在屏幕宽度大于768px时生效，即对超小屏无效(xs)
- 要禁用`fieldset`内的所以控件，建议使用给所有`fieldset`内的元素添加`disable`属性来解决兼容性问题

#### 按钮

- 可以使用`<a>|<input type="button">|<button>`来制作按钮，但是为了跨浏览器一致性，强烈推荐使用`<button>`来实现

### 4. JavaScript部分

- JS插件的使用有两张方式，可任选其一，但在同一个网站中，请确保统一使用一种方式
- 如果使用的插件少于3个，请使用单独引入JS插件的方式
- 单独引入JS插件时，确保插件依赖的JS已引入
- 当JS被禁用时，Bootstrap不提供优雅降级，如果要处理这种情况，使用`<noscript>`来向你的用户解释情况

### 5. 扩展

#### 扩展原则

- 移动优先，media query语句遵循先小屏后大屏的原则
- 新增组件时，优先采用扩展Bootstrap组件或组件组合的方式

#### 个性化定制

- 如果要修改Bootstrap整体的样式，Bootstrap官网提供了config.json方法和自定义页面，尽量使用自定义页面，防止修改中引入bug
- 当需要自定义样式时，可以选择修改LESS变量名，重新编译；也可以选择在自己的文件中覆写Bootstrap的样式
	这里的原则是：
	1. 当可以通过修改某些LESS变量来达到目的时，采用重新编译的方法，在Bootstrap官网自定义
	2. 当修改LESS变量无法达到目的或修改的样式很少时，采用覆写的方法

#### 插件编写

- 必须提供JS与Data-api两种使用方式
- 必须提供Constructor.DEFAULT修改插件的默认配置
- 使用带命名空间的事件的方式而不是钩子方法来提供用户自定义动作的能力

## III 从2.x迁移到3.x

参照[Bootstrap官方迁移指南](http://getbootstrap.com/migration/)进行迁移
