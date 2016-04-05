# QCloud代码规范 
## **HTML**

### 语法  

 - 缩进使用4个空格；
 - 嵌套的节点应该缩进；
 - 属性名全小写，用中划线做分隔符；
 - 在属性上，使用双引号，不要使用单引号；
 - 自闭合标签，无需闭合 ( 例如： img input 等 )；
 - 可选的闭合标签，需闭合 ( 例如：li 或 body 等 )；
   
``` html
    <!DOCTYPE html>
    <html>
      <head>
        <title>Page title</title>
      </head>
      <body>
        <img src="images/logo.png" alt="Company">
        <h1 class="hello-world">Hello, world!</h1>
      </body>
    </html>
```


### HTML5 doctype
为每个 HTML 页面的第一行添加标准模式（standard mode）的声明， 这样能够确保在每个浏览器中拥有一致的表现。
``` html
<!DOCTYPE html>
<html>
	...
</html>
```
### 字符编码

 - 以无 BOM 的 utf-8 编码作为文件格式;
 - 指定字符编码的 meta 必须是 head 的第一个直接子元素；
 
 ```html
 <!DOCTYPE html>
<html>
        <head>
            <meta charset="UTF-8">
        </head>
    ...
</html>
 ```
 
### IE 兼容模式
 优先使用最新版本的IE 和 Chrome 内核；
 
```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```
### 属性顺序
HTML 属性应该按照特定的顺序出现以保证易读性；
 - id
 - class
 - name
 - data-*
 - src,for,type,href
 - title,alt
 - required, readonly, disabled
 
### 布尔（boolean）型属性
HTML5 规范中 disabled、checked、selected 等属性不用设置值；

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

### 标签嵌套
a 不允许嵌套 div这种约束属于语义嵌套约束，与之区别的约束还有严格嵌套约束，比如a 不允许嵌套 a；
#### 语义嵌套约束

 - `<li>` 用于 `<ul>` 或 `<ol>` 下；
 - `<dd>`, `<dt>` 用于 `<dl>` 下；
 - `<thead>`, `<tbody>`, `<tfoot>`, `<tr>`, `<td>` 用于 `<table>` 下；
  
 
#### 严格嵌套约束
 - inline-Level 内联元素，仅可以包含文本或其它 inline-Level 内联元素;
 - `<a>`里不可以嵌套交互式元素`<a>`、`<button>`、`<select>`等；
 - `<p>`里不可以嵌套块级元素`<div>`、`<h1>~<h6>`、`<p>`、`<ul>/<ol>/<li>`、`<dl>/<dt>/<dd>`、`<form>`等；

   更多详情请参考 [WEB标准系列-HTML元素嵌套][1]


### 引入 CSS 和 JavaScript 文件

 - link 必须声明 rel="stylesheet"；
 - CSS 没有特殊要求的情况下写在 head 标签内部；
 - &nbsp;JS &nbsp;&nbsp;没有特殊要求的情况下写在 body 内部末尾；
 - 引入 CSS 和 JS 时不需要指明 type，因为 text/css 和 text/javascript 分别是他们的默认值；

```html
<!-- External CSS -->
<link rel="stylesheet" href="code_guide.css">

<!-- In-document CSS -->
<style>
    ...
</style>

<!-- External JS -->
<script src="code_guide.js"></script>

<!-- In-document JS -->
<script>
    ...
</script>
```

### 图片

【强制】禁止 img 的 src 取值为空；延迟加载的图片也要增加默认的 src；src 取值为空，会导致部分浏览器重新加载一次当前页面；

【建议】添加 width 和 height 属性，以避免页面抖动；

【建议】为重要图片添加 alt 属性；可以提高图片加载失败时的用户体验；

【建议】有下载需求或者预期会灵活变动的图片采用 img 标签实现，无下载需求的图片采用 CSS 背景图实现；
用户头像、用户产生的图片等有潜在下载需求的图片，以 img 形式实现，能方便用户下载；
无下载需求的图片，比如：icon、背景、代码使用的图片等，尽可能采用 css 背景图实现。

### 表单
有文本标题的控件必须使用 label 标签将其与其标题相关联；

 - 将控件置于 label 内；
 - label 的 for 属性指向控件的 id；
    推荐使用第一种，减少不必要的 id。如果 DOM 结构不允许直接嵌套，则应使用第二种；
```html
<label><input name="confirm" type="checkbox" value="on"> 我已确认上述条款</label>

<label for="username">用户名：</label> <input id="username" name="username" type="checkbox">
```
在针对移动设备开发的页面时，根据内容类型指定输入框的 type 属性；根据内容类型指定输入框类型，能获得能友好的输入体验；
```html
<input type="number" value="1">
```


 
 
 


  [1]: http://www.smallni.com/element-nesting/