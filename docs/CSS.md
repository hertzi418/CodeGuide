# QCloud代码规范 
## **CSS**

### 语法  

 - 缩进使用2个空格；
 - 每个属性独占一行；
 - 每个属性末尾需要加分号；
 - 属性名全小写，用中划线做分隔符；
 - 选择器与 `{` 之间必须添加一个空格；
 - `:` 之前不能有空格，之后必须有空格；
 - 省略小于 1 的小数前面的 0 （ 例如，.5 代替 0.5；）；
 - 选择器中的属性需加双引号，例如，`input[type="text"]`；
 - 十六进制值应该全部小写，尽量使用简写形式，例如，`#fff`；
 - 避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;
   
``` css
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```


### 声明顺序
由于定位（positioning）可以使元素脱离正常文本流，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面；

 - Positioning，相关属性包括：position / top / right / bottom / left / z-index；
 - Box model，相关属性包括：display / float / width / height / padding / margin / border / overflow / ...；
 - Typographic（文本排版），相关属性包括：font / line-height / text-align / word-wrap / ...；
 - Visual（视觉外观），相关属性包括：color / background / list-style / transform / animation / transition / ...；
 
 如果包含 content 属性，应放在最前面
 
### 命名规范
 - 使用语义化、通用的命名方式；
 - 使用中划线`-`连接多个单词；
 - 避免选择器和 Class、ID 叠加使用；
 - 避免选择器嵌套层级过多，尽量少于 3 级；
 - 避免过度简写。.btn表示button，但.a 没有意义；
 - 对于通用元素使用class，少用标签名；
 

推荐使用的css名：
 - 表示状态：.on, .active, .selected；
 - 表示位置：.first, .last, .main, .side；
 - 表示结构：.hd, .bd, .ft, .col, .section；
 - 通用元素：.tb, .nav, .list, .item, .tag, .pic, .info

###注释
注释统一用'/* */'（scss中也不要用'//'），具体参照右边的写法；
缩进与下一行代码保持一致；
可位于一个代码行的末尾，与代码间隔一个空格。

``` css
/* 单行注释 */
.modal-header {
    ...
}

/*
 * 多行注释
 */
.modal-header {
    ...
}

.modal-header {
    /* 50px */
    width: 50px;

    color: red; /* color red */
}
```
 
###不要使用@import
与 `<link>` 相比，`@import` 要慢很多，不光增加额外的请求数，还会导致不可预料的问题。

### 链接的样式顺序
a:link -> a:visited -> a:hover -> a:active（lvha）

###带前缀的属性
当使用特定厂商的带有前缀的属性时，通过缩进的方式，让每个属性的值在垂直方向对齐，这样便于多行编辑。

    '-webkit' : Webkit内核： 主要代表为Chrome和Safari
       '-moz' : Gecko内核：  主要代表为Firefox
        '-ms' : Trident内核：主要代表为IE浏览器
          '-o': Presto内核： 主要代表为Opera
          
###属性缩写
在可以使用缩写的情况下，尽量使用缩写形式（无继承关系时使用缩写，存在继承关系使用分拆方式）

可缩写的属性有：

    padding
    margin
    font
    background
    border
    border-radius
    transition
    animation
    
```css
background-color: #000;
background-image: url(images/bg.png);
background-repeat: no-repeat;
background-position: top right;

/* 可缩写为*/
background: #000 url(images/bg.png) no-repeat top right;
```
###清除浮动
当元素需要撑起高度以包含内部的浮动元素时，通过对伪类设置 clear 或触发 BFC 的方式进行 clearfix。尽量不使用增加空标签的方式。
伪类设置 clear：
```css
.clear:after{display:block;content:"."; clear:both;font-size: 0;height: 0;visibility: hidden;}
```
触发BFC的方式有很多，常见的有：

    float 非 none
    position 非 static
    overflow 非 visible
    
###正确使用display属性
display属性会影响页面的渲染，请合理使用。

 - display: inline后不应该再使用 width、height、margin、padding 以及 float；
 - display: inline-block 后不应该再使用 float；
 - display: block 后不应该再使用 vertical-align；
 - display: table-* 后不应该再使用 margin 或者 float

###不滥用 Float
float在渲染时计算量比较大，尽量减少使用。

###更高效地使用选择器
CSS 选择器对性能的影响主要在于浏览器匹配选择器和文档元素时所消耗的时间，所以优化选择器的原则是应尽量避免使用消耗更多匹配时间的选择器。 CSS 选择器的匹配机制是从右到左进行匹配的，了解了这个机制后，你懂的。

 - 避免使用通用选择器

 ```css
 *{margin: 0;padding: 0;}
 ```
 
 - 避免使用标签选择器限制 class 或 id 选择器
 
```css
div.con{...}
div#con{...}
```

 - 避免使用多层标签选择器。使用 class 选择器替换，减少css查找
 
 ```css
    /* bad */
    dl > dd > p{...}
    
    /* better */
    .describe{...}
 ```
 
 - 避免使用子选择器
 ```css
    /* bad */
    ul > li{...}
    
    /* better*/
    .list{...}
 ```

###杂项

 - 使用字体图标

单色图标推荐使用字体图标
