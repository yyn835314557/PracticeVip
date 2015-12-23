My Javascript Learning

***

# JavaScript 的实现：组成部分

 - 核心(ECMAScript)
 - 文档对象模型(DOM)
 - 浏览器对象模型(BOM)

# 处理事件: 用户在访问页面执行的操作(提交表单，在图像上移动鼠标)。JS 使用 事件处理程序(event handler) 的命令来处理事件,用户在页面上的操作会 触发脚本中的事件处理程序

 - onabort: 用户终止了页面的加载
 - onblur: 用户离开了对象
 - onchange: 用户修改了对象
 - onclick: 用户单机了对象
 - onerror: 脚本遇到了一个错误
 - onfocus: 用户激活了对象
 - onload: 对象完成了加载
 - onmouseover: 鼠标指针移动到对象上
 - onmouseout: 鼠标指针离开了对象
 - onselect: 用户选择了对象的内容
 - onsubmit: 用户提交了表单
 - onunload: 用户离开了页面

  ```
  <!DOCTYPE html>
  <html>
  <head>
    <title>Barely a script at all</title>
    <script type="text/javascript">
        window.onload = function(){
            document.getElementById("myMessage").innerHTML = "Hello, Cleverland!";
        }
    </script>
  </head>
  <body>
  <h1 id="myMessage"></h1>
  </body>
  </html>
  ```

# 基本概念: 6个属性

- async: 表示立即下载脚本(针对外部脚本)，但是不妨碍页面中的其他操作(下载其他资源或等待加载其他脚本)
    - `<script type="text/javascript" async src=""></script>` 不保证执行顺序
- charset: 表示通过 src 属性指定的代码的字符集，但是大多数浏览器忽略它的值
- defer: 表示脚本(针对外部脚本)可以延迟到文档完全被解析和显示之后再执行，`<script type="text/javascript" defer=“defer” src=""></script>`
    - 按照标准是顺序执行，但在现实中延迟脚本并不一定按照顺序执行，也不一定会优先于 DOMContentLoaded 事件触发前执行，因此最好包含一个延迟脚本
- src:
- type:

可以在页面中内嵌 Javascript 代码和外部包含 JavaScript 文件

 ```
    <script type="text/javascript">
        function sayScript(){
            alert("\/script);
        }
    </script>
 ```

在不包含 async 和 defer 属性，浏览器会按照 <script> 元素在页面中出现的先后顺序对它们依次进行解析。

按照传统做法，<script> 元素应该放在页面的 <head> 元素中，现在Web应用一般都把全部JavaScript引用放在 <body> 元素中页面内容的后面


# 在XHTML 中的用法

 ```
 // 方法一: 使用 < 相对应的 HTML 实体 (&lt;) 替换代码中的所有小于号
 <script type = "text/javascript">
    function compare(a,b){
        if (a &lt; b) {
            alert("A is less than B");
        }else if(a > b){}
            alert("A is greater than B");
        }else{
            alert("A is equal to B");
        }
    }
 </script>
 // 方法二： 用一个CData片段来包含JavaScript代码。在XHTML(xml)中，CData 片段是文档中的一个特殊区域，可以包含不需要解析的任意格式的文本内容。
 <script type = "text/javascript">
 <![CData[
        function compare(a,b){
        if (a &lt; b) {
            alert("A is less than B");
        }else if(a > b){}
            alert("A is greater than B");
        }else{
            alert("A is equal to B");
        }
    }
 ]]>
 </script>

 ```

# 嵌入代码与外部文件

 - 可维护性
 - 可缓存
 - 适应未来

# <noscript>元素只有在如下的两种情况中才会显示出来

 - 浏览器不支持脚本
 - 浏览器支持脚本，但是脚本被禁用

 ```
 <html>
    <head>
        <title>testtttt</title>
        <script type="text/javascript" defer="defer" src="... .js"></script>
        <script type="text/javascript" defer="defer" src="... .js"></script>
    </head>
    <body>
        <noscript>
            <p>本页面需要浏览器支持启用JavaScript</p>
        </noscript>
    </body>
 </html>
 ```

# JavaScript 的基本概念

 - 区分大小写
 - 标识符
    - 第一个字符必须是一个字母、下划线、或者美元符号
    - 其他字符可以是字母、下划线、数字、美元符号
 - 严格模式
    - “use strict”
 - 注释
    - 单行注释: //
    - 块机器注释: /* ... */
 - 变量: `var message;`
    - 松散类型: 可以用来保存任何类型的数据，每个变量仅仅是一个用于保存值的占位符
    - 修改变量值的同时可以修改值的类型
    - 使用 `var` 作为局部变量，在退出函数后就会被销毁，直接定义 `message = "hi"` 作为全局变量

    ```
    function test(){
        message = "Hi";
    }
    test();// 只要调用过一次 test 函数，这个变量就有了定义，可以再全局被访问到
    alert(message);
    ```
 - 数据类型:
    - "undefined": 值未定义,只有一个值 undefined 使用 var 声明但是未对其进行初始化时这个变量就是 undefined
     ```
     var message;
     alert(message == undefined); //true
     alert(typeof message); //undefined
     ```
    - "Null": 也是一个只有一个值的数据类型 值为 null 表示一个空对象指针使用,使用 typeof操作符检测 null 值时会返回 “object” 的原因
      ```
      var car = null;
      alert(typeof car); // "object"
      // 如果一个变量将来用于保存对象，将其初始化为 null , undefined == null 输出 true
      // alert(null == undefined); undefined 派生与 null
      ```
    - "Boolean":
    - "Number":
    - "String":

 -  typeof 负责返回给定变量的数据类型，可以返回下列某个字符串
    - "undefined": 值未定义
    - "boolean": 值是布尔值
    - "string": 值是字符串
    - "number": 值是数值
    - "object": 值是对象或者null
    - "function": 值是函数

 ```
 var message = "some string"
 alert(typeof message);// "string"
 alert(typeof(message));// "string"
 alert(typeof 95);// "number"
 // note: typeof 是操作符不是函数
 ```

# class and id: CSS 样式表在规则中使用这些属性定义页面的外观，而JavaScript 文件在代码中使用这些属性来影响页面上元素的行为。

 - class: 标识出可能多次使用的元素

 ```CSS
 .moveTitle{
    font: bold 28px;
    color: #FF0000;
  }
  <h1 id="theaterName">The Raven Theater Presents</h1>
  ```