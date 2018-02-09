# 代码规范 
## **JavaScript**

### 语法  

 1. 缩进使用4个空格；
 2. 适合使用空格的地方
 
    - for循环中的分号之后，比如for (var i = 0; i < 10; i ++ ) {...}
    - 用于分隔数组元素的逗号之后，比如var a = [1, 2, 3];
    - 对象属性后的逗号以及名值对之间的冒号之后，比如var o = {a: 1, b: 2};
    - 函数参数中，比如myFunc(a, b, c);
    - 在运算符和操作数之间也添加空格。也就是说在+、-、*、=、<、>、<=、>=、===、!==、&&、||、+= 符号前后都添加空格。
 3. 最外层使用单引号`''`；
 ```javascript
 var div = '<div id="test"></div>';
 
 ```
 4. 数组、对象：
 对象属性名不需要加引号；
 对象以缩进的形式书写，不要写在一行；
 数组、对象最后不要有逗号。
   
``` javascript
// not good
var a = {
    'b': 1
};

var a = {b: 1};

var a = {
    b: 1,
    c: 2,
};

// good
var a = {
    b: 1,
    c: 2
};

```



 
### 命名规范
 - 变量，使用驼峰命名法；
 ```javascript
    var loadingModules = {};
    
 ```
 - 常量，字母大写，使用下划线连接`_`；
  ```javascript
    var LOGIN_URL = '/login.do';
    
 ```
 
 - 私有属性、变量或方法，在变量名前加`_`下划线前缀；
 ```javascript
     var person = {
        getName: function () {
            return this._getFirst() + ' ' + this._getLast();
        },
        _getFirst: function () {
            // ...
        },
        _getLast: function () {
            // ...
        }
};
 ```
 - 全局变量，使用g作为前缀，如gUserName；
 - ID在变量名中全大写；
 - URL在变量名中全大写；
 - Android在变量名中大写第一个字母；
 - iOS在变量名中小写第一个，大写后两个字母；
 - 构造函数首字母大写；
 - boolean 类型的变量使用is或has开头；
 ```javascript
    var isReady = false;
    var hasName = false;
    
 ```
 
###声明变量
 
 - 每个变量必须声明，并使用单var模式；变量声明必须放在函数顶部，避免声明提前的问题。
```javascript
    /* bad */
    var a = 1;
    function func(){
        console.log(a); // undefinde
        var a = 2;  // 声明提前了，但是赋值并没有提前
    }

    /* good */
    function func(){
        var pageNum = 1,
            pageSize = 10,
            options = {};
    }
```
 
 - 函数声明要用表达式，不使用直接声明；
 - 除了构造函数和时间（Date）, 尽量不要用 new 来声明;

> 使用 {}, [] 替代 new Object(); new Array();

```javascript
    /* bad */
    function abs (){
    };
    var abc = new function(){};
    
    /* good */
    var abc = function(){
    };
```
    
###注释

 - 单行注释；
 必须独占一行。`//` 后跟一个空格，缩进与下一行被注释说明的代码一致。
 - 多行注释；
最少三行, '*'后跟一个空格；
```javascript
/*
 * 多行注释
 */
var x = 1;
```

    建议在以下情况下使用：
    - 难于理解的代码段
    - 可能存在错误的代码段
    - 浏览器特殊的HACK代码
    - 业务逻辑强相关的代码
 

 - 函数/方法注释
1、函数/方法注释必须包含函数说明，有参数和返回值时必须使用注释标识。；
2、参数和返回值注释必须包含类型信息和说明；
3、当函数是内部函数，外部不可访问时，可以使用 @inner 标识；
```javascript
/*
 * 函数描述
 * @param {element} tag 目标容器
 * @param {number} sum 总金额
 * @param {number} num 商品数量
 * @return {Object} 返回值描述
 */
 
function Cart(tag, sum, num) {
    return {
        tag: tag,
        sum: sum,
        num: num
    };
}
```

 - 事件注释
 必须使用 @event 标识事件，事件参数的标识与方法描述的参数标识相同；
```javascript
/**
 * 值变更时触发
 *
 * @event Select#change
 * @param {Object} e e描述
 * @param {string} e.before before描述
 * @param {string} e.after after描述
 */
this.fire(
    'change',
    {
        before: 'foo',
        after: 'bar'
    }
);
```

###杂项
- 拼接字符串，需根据实际情况进行合理的转义；
```javascript
    
// HTML 转义
var str = '<p>' + htmlEncode(content) + '</p>';

// HTML 转义
var str = '<input type="text" value="' + htmlEncode(value) + '">';

// URL 转义
var str = '<a href="/?key=' + htmlEncode(urlEncode(value)) + '">link</a>';

// JavaScript字符串 转义 + HTML 转义
var str = '<button onclick="check(\'' + htmlEncode(strLiteral(name)) + '\')">提交</button>';
```
- 使用模板引擎；
推荐使用 [artTemplate][1]
具体用法请移步官方文档。
    


  [1]: https://github.com/aui/artTemplate