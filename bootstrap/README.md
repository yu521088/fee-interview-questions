# Bootstrap 最佳实践
------

> Yu Chen (2014/10/24)

### 基础设置
- 让你的页面适应各种设备:
   `<meta name="viewport" content="width=device-width, initial-scale=1[, user-scalable=no]">`
- 使用HTML5文档类型: `<!DOCTYPE html>`
- IE8下需要使用Respond.js来支持媒体查询语句

### 栅格系统

- 将`.row`必须被包含在`.container`或`.container-fluid`之内
- **只有在需要多列布局时需要栅格系统**，下面的代码是错误的，因为H4本来就占据一整行:
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

### 表格

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

### 表单

- 使用`disabled`属性来禁用表单域
- 为每个表单控件添加相应的`label`
