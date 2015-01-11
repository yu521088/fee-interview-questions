**欢迎添加**
------

## HTML问题 ##
1. `doctype（文档类型）`的作用是什么？
      <br/>告诉浏览器页面使用的HTML版本
2. 浏览器标准模式和怪异模式之间的区别是什么？
      <br/>标准模式会以标准模式解释页面，怪癖模式则以兼容模式解释老的页面。
3. 说说HTML5有那些新特性，移除了哪些元素？
      * HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
      * canvas, video, audio, localStorage, sessionStorage, Geolocation,APP Cache,web worker, 语义化标签, 表单控件
      * 移除了纯表现的元素：basefont，big，center，font, s，strike，tt，u；对可用性能产生负面影响的元素：frame，frameset，noframes；
4. iframe有那些缺点？
      <br/>iframe会阻塞主页面的Onload事件；
      <br/>iframe是最费资源的元素；
5. 请描述一下 cookies，sessionStorage 和 localStorage 的区别？
      * cookie在浏览器和服务器间来回传递。 sessionStorage和localStorage不会
      * sessionStorage和localStorage的存储空间更大(>4M)，cookie只有4K；
      * sessionStorage和localStorage有更多丰富易用的接口；
      * sessionStorage和localStorage各自独立的存储空间；
      * sessionStorage的数据在浏览器开着时会一直存在；
      * localStorage的数据会一直存在，即使在浏览器被关闭以后；
6. 行内元素有哪些？块级元素有哪些？什么是可替换元素？什么是不可替换元素？
      1. CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值， 比如div默认display属性值为“block”，成为“块级”元素； span默认display属性值为“inline”，是“行内”元素。
      2. 行内元素有：a b span img input select strong（强调的语气）
      3. 块级元素有：div ul ol li dl dt dd h1… p
      4. 知名的空元素： br hr img input link meta 鲜为人知的是： area base col command embed keygen param source track wbr
  
      替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。如img，input
      不可替换元素，即其内容直接表现给用户端。如p

## JavaScript问题 ##
### 代码问题 ###
1. specify('hello world') // => 'h e l l o   w o r l d' 实现specify函数
   <br/>A: 
    ````javascript
    function specify(s){
      return s.split('').join(' ');
    }
    ````
   如果输出'h e l l o w o r l d'
   
    ````javascript
    function specify(s){
      return s.replace(' ', '').split('').join(' ');
    }
    ````

2. 实现一个log()方法，接收多个参数，在输出前添加"(APP) "
   <br/>A: 
    ````javascript
    function log(){

      var args = Array.prototype.slice.call(arguments);

      args.unshift('(app) ');

      console.log.apply(console, args);

    };
    ````
    
3. 上下文理解
    ````javascript
    var User = {

      count: 1,

      getCount: function() {

        return this.count;

      }

    };
    console.log(User.getCount());
    var func = User.getCount;
    console.log(func());
    ````
   A: 输出1和undefined

4. 数组求合集，要求时间复杂度最小
    ````javascript
      var first = ['a','b','c','d','e'], second = ['a','b','c'], third = ['a','c','d','e'], fourth = ['a','d','e','f'] 
    ````
   A: 第一种方法
    ````javascript
      var result = {};
      var heji = [];
      var whole = first.concat(second, third, fourth);
      for(var i = whole.length-1; i >= 0; i--){
            var part = whole[i];
            result[part]?(result[part] += 1) : result[part] = 1;
      }
      for(var j in result){
            j.length == 4 ? heji.push(j):;
      }
      时间复杂度: n*m*2 (n为数组个数，m为数组长度)
    ````
      第二种方法，假设知道数组的所有元素
    ````javascript
      var whole = first.concat(second, third, fourth).join('');
      var heji = [];
      var tpl = ['a','b','c','d','e','f'];
      for(var i = tpl.length-1 ; i >= 0 ; i--){
            var test = whole.slice();
            test = test.replace(new RegExp(tpl[i],'gi'),'*').replace(/[^\*]/gi,'');
            test.length == 4 && heji.push(tpl[i]);
      }
      时间复杂度: n*m
    ````
5. 如何将7898.567转化成2进制(8进制/16进制)？
    ````
    new Number(7898.567).toString(2); // output: 1111011011010.1001000100100110111010010111100011010101
    ````

### 描述问题
1. 访问对象属性的两种方法。 
2. 如何判断一个属性是否是对象的自有属性？ ( hasOwnProperty )
3. 遍历对象属性用什么方法？(for in)
4. 谈谈你喜欢的开发环境。(例如操作系统，编辑器，浏览器，工具等等。)
5. 你能描述一下渐进增强和优雅降级之间的不同吗? ([cnblogs](http://www.cnblogs.com/mofish/p/3822879.html))
6. 解释下事件代理。
7. 什么是哈希表？
8. null和undefined的区别是什么？ (null是定义一个变量，它的值未定；undefined是不知道有这个变量)
9. 什么是闭包，如何使用它，为什么要使用它？
10. `.call` 和 `.apply` 的区别是什么？ (参数不同)
11. 你使用过 JavaScript 模板系统吗？
12. 研究过jQuery源码吗？
13. 函数表达式和函数声明的区别 (函数声明会在执行前被解析，因此定义在代码的任意位置都可用)
14. 变量的作用域并解释变量声明提升。(函数作用域。 所有变量都会被提升到作用域的顶端)
15. "attribute" 和 "property" 的区别是什么？(.property, getAttribute, getAttribute('checked') == 'checked', ele.checked == true)
16. 请指出 document load 和 document ready 两个事件的区别。
17. == 和 === 有什么不同？ (值等和全等)
18. 请解释一下 JavaScript 的同源策略。 (脚本只能访问同源的页面属性和资源，同源指协议，地址和端口相同)
19. 什么是 "use strict"; ? 使用它的好处和坏处分别是什么？
20. 函数的参数arguments是数组吗？怎么把它转化成标准数组？(类数组， Array.prototype.slice.call(arguments) )
21. eval()的作用是什么？为什么不推荐使用？
22. 事件、IE与火狐的事件机制有什么区别？ 如何阻止冒泡？
23. "use strict";是什么意思 ? 使用它的好处和坏处分别是什么？
24. 如何判断一个对象是否属于某个类？ (instanceof)
25. 如何编写高性能的Javascript？
26. JSONP的实现机制是怎么样的？
27. WebSocket的实现机制是什么，与现有的解决方案对比的优缺点？
28. 从输入url到显示网页，后台发生了什么？   [SF](http://sfau.lt/bNcdAd) [cnblog](http://www.cnblogs.com/rollenholt/archive/2012/03/23/2414345.html)
29. 数组的排序怎么实现？A: 用sort方法，传递一个function，升序则返回小于0，降序则返回大于0

## CSS相关
0. CSS 基础选择器 ( +: the element right behind first element; ~: the sibling elements after first element )
1. 列举你知道的重要的CSS Hack( IE8: \9, IE7: *, IE6: _)
1. 描述下 “reset” CSS 文件的作用和使用它的好处。(可以消除浏览器默认样式的影响)
2. 解释下浮动和它的工作原理。
3. 列举不同的清除浮动的技巧，并指出它们各自适用的使用场景。
    1. 给父元素加overflow:hidden，迫使父元素包含其浮动的子元素
    2. 同时浮动父元素
    3. 添加非浮动的清除元素
        1. 添加一个空div，clear:both
        2. .clearfix:after{content:'.';display:block;height:0;visibility:hidden;clear:both;}
4. 讨论CSS hacks，条件引用或者其他。
5. link和@import的区别。
      * link属于XHTML标签，而@import是CSS标签;
      * 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;
6. 你用过媒体查询，或针对移动端的布局/CSS 吗？ (  @media (max-width: 1200px) and (min-width: 700px)  )
7. 使用 CSS 预处理器的优缺点有哪些？(SASS，Compass，Stylus，LESS) 
8. 解释下浏览器是如何解析 CSS 选择器的？(从右往左解析)
9. 解释一下你对盒模型的理解，以及如何在 CSS 中告诉浏览器使用不同的盒模型来渲染你的布局。(box-sizing:content-box/border-box)
10. CSS 选择符有哪些？哪些属性可以继承？
11. CSS 优先级算法如何计算？(按权重计算，如果权重相同，后出现的覆盖先出现的)
11. CSS 伪类有哪些？(love, :focus, :first-child)
11. CSS3 新增伪类有那些(:nth-child, :nth-last-child, :nth-of-type, :first-of-type, :last-of-type, :checked, :enabled, :disabled, :target, :empty)？
12. css定义的权重 (ID > Class > tag > * > inherit)
11. CSS3有哪些新特性？ (动画，渐变，透明度，圆角，阴影，字体，多重背景，)
13. CSS3动画在移动端的性能
14. 垂直居中已知高度的元素(使用负边距)
15. CSS3伪元素有那些？(::after, ::before, ::selection, ::first-letter, ::first-line等)
16. CSS1/CSS2/CSS3有什么区别？(CSS2比CSS1新增了选择器，定位；CSS3比CSS2新增了选择器，动画，圆角，阴影，多重背景等)
17. 如何居中浮动元素？(绝对定位+负边距)

## 综合问题
1. 跨域访问的实现   JSONP, [iframe](http://www.cnblogs.com/pigtail/archive/2013/01/24/2875310.html)
2. 邮件数据统计，获取邮件的浏览量
3. 兼容性处理
    1. JS: console, JSON, Array.prototype.forEach()
    2. CSS: \9(IE8), *(IE7), _(IE6)
4. HTTP请求头和响应头的内容
    1. accept, accept-encoding, connection, cache-control, cookie, host, pragma, user-agent, referer
    2. connection, cache-control, content-encoding, content-type, date, expires, server
