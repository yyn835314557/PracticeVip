#My Javascript Learning

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
            alert("\/script");
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

# html 基本属性

 * 一个基本的table: table>(thead>tr>th*5)+(tbody>tr>td*5)+(tfoot>tr>td*5)

   ```html
    <table width="100%" border="1">
        <col></col>
        <caption>table的标题</caption>
       <thead>
           <tr>
                <th>Month</th>
                <th>Savings</th>
           </tr>
        </thead>
        <tbody>
            <tr>
                <td>Jannuary</td>
                <td>$100</td>
            </tr>
             <tr>
                <td>February</td>
                <td>$80</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>Sum</td>
                <td>$180</td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </tfoot>
    </table>
   ```

 * 列表: dl>(dt+dd)*2
    - 无序: ul>li 类似 md 的 *-
    - 有序: ol>li
    - 选择列表: select>(optgroup>option*2)*2,optgroup定义选项组
        ```
        <select name="" id="">
            <optgroup label="Swedish Cars">
                <option value ="volvo">Volvo</option>
                <option value ="saab">Saab</option>
            </optgroup>
            <optgroup>
                <option value ="mercedes">Mercedes</option>
                <option value ="audi">Audi</option>
            </optgroup>
        </select>
        ```
    - 选择列表: <datalist> 与 input 元素配合使用该元素，来定义 input 可能的值。datalist 及其选项不会被显示出来，它仅仅是合法的输入值列表,使用 input 元素的 list 属性来绑定 datalist。
        ```
        <input id="" list="cars" />
        <datalist id="cars">
            <option value="BMW"></option>
            <option value="Ford"></option>
            <option value="Volvo"></option>
        </datalist>
        ```

 * 表单: form 用于向服务器传输数据，元素是块级元素，前后会产生折行,在HTML表单中使用 input元素来创建按钮
    - input : `type="button\checkbox\file\hidden\image\password\radio\reset\submit\text"`
    - fieldset: 将表单内的相关元素分组，表单内容的一部分打包，生成一组相关表单的字段
    - menus
    - textarea
    - legend: 为 fieldset 元素定义标题
    - label: 为 input 元素定义标注
    - keygen: 表单的密钥对生成器字段，当提交表单时，私钥存储在本地，公钥发送到服务器
    - oninput:

    ```
    <form action="表单提交的地址" method="get/post"></form>
        <p>firstName: <input type="text" name="fname" /></p>
        <p>lastName: <input type= "text" name="lname" /></p>
        <label for="male">Male</label>
        <input type="radio" name="sex" id="male" />
        Encryption: <keygen name="security" />
        <input type="submit" value="Submit" />
    </form>
    <form oninput="x.value = parseInt(a.value) + parseInt(b.value)">0
       <input type="range" id="a" value="50"> 100 + 
       <input type="number" id="b" value="50">=
       <output name="x" for="a b"></output>
    </form> 
    ```
 
 * 页面框架: frameset>frame*3,noframes为那些不支持框架的浏览器显示文本

    ```
    <frameset cols="25%,50%,25%">
        <noframes>
             <body>Your browser does not handle frames!</body>
        </noframes>
        <frame src="1.html" />
        <frame src="2.html" />
        <frame src="3.html" />
    </frameset>
    ```

 * <button type="button">按钮</button> 在元素内部可以放置内容，比如文本或者图像这是使用input与该元素创建按钮的不同之处。
 * 多行输入文本框: <textarea row="3"  cols="20">在这里面输入内容</textarea>
 * 定义时间和日期: <time>9:00</time>,<time datetime="2010-02-14">情人节</time>
 * <canvas>标签定义图形(图表和图像)，只是图形容器，使用脚本来绘制图形

 ```
 <canvas>your broswer is not support canvas tag</canvas>
 <script type="text/javascript">
    var canvas = document.getElementById('myCanvas');
    var ctx = canvas.getContext('2d');
    ctx.fillStyle = '#FF0000';
    ctx.fillRect(0,0,80,100);
 </script>
 ```

 * 播放视频(video),音频(audio): track(字幕)，source(2分源文件浏览器选择支持的文件)

 ```
 <video width="320" height="240" controls="controls">
      <source src="forrest_gump.mp4" type="video/mp4" />
      <source src="forrest_gump.ogg" type="video/ogg" />
      <track kind="subtitles" src="subs_chi.srt" srclang="zh" label="Chinese">
      <track kind="subtitles" src="subs_eng.srt" srclang="en" label="English">
 </video>
 ```

 * 页面上所有链接规定默认地址或者默认目标，浏览器随后将不再使用当前文档的 URL，而使用指定的基本 URL 来解析所有的相对 URL. <a>、<img>、<link>、<form> 都有作用

    ```
    <head>
    <base href="http://baidu.com/i/"/>
    <base target="_blank"/>;
    </head>
    <body>
    <img src="eg_smile.gif"/>
    <a href="http:www.baidu.com">百度</a>
    </body>
    ```

 * 定义图像映射中区域(图像映射指的是带有可点击区域的图像)，area元素总是嵌套在 map 标签中 

    ```
    <img src="planets.jpg" border="0" usemap="#planetmap" alt="Planets" />
    <map name="planetmap" id="planetmap">
        <area shape="circle" coords="180,139,14" href ="venus.html" alt="Venus" />
        <area shape="circle" coords="129,161,10" href ="mercur.html" alt="Mercury" />
        <area shape="rect" coords="0,0,110,260" href ="sun.html" alt="Sun" />
    </map>
    ```
 
 * 元素提供有关页面的元信息(针对搜索引擎和更新频度的描述和关键词)，元数据总是以名称/值的形式被成对传递的: meta。
     - 必须属性: <meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
        - content(定义与 http-equiv 或 name 属性相关的元信息),必须包含 `<meta http-equiv="content-type" content="text/html" />`
        - 始终要和 name 属性或者 http-equiv 属性一起使用
     - 可选属性:
        - http-equiv: 把content属性关联到HTTP头部,指示服务器在发送实际的文档之前先在要传送给浏览器的 MIME 文档头部包含名称/值对。
            - `http-euqiv = "content-type" content = "text/html"`
            - `http-equiv = "expires" content = "31 Dec 2008"`
            - `http-equiv = "refresh" content="5;url=http://www.w3school.com.cn"` 域名重定向
            - `http-equiv = "set-cookie"`
            - `http-equiv = "chrset" content = "utf-8"`
        - name:
            - `name="keywords" content="HTML,ASP,PHP,SQL"`
            - `name="author" content=""`
            - `name="description" content=""`
            - `name="generator" content="Sublime Text 3 en"` 定义编辑软件
            - `name="revises" conent="yanni.you,26/12/15"` 定义创作者
            - `name="others" content=""`
        - scheme:
            - scheme 属性用于指定要用来翻译属性值的方案。此方案应该在由 <head> 标签的 profile 属性指定的概况文件中进行了定义
 * 定义导航链接: nav, `nav>a*3`
 * 链接样式表，定义文档与外部资源的关系 `<head><link rel="stylesheet" type="text/css" href="theme.css /></head>`
 * 定义文档或文章的作者的联系信息: `<address>Written by <a href="mailto:webmaster@example.com">Donald Duck</a>.<br> 作者的个人信息</address>`
 * 简称或缩写: `<abbr title="People's Republic of China">PRC</abbr>` ,通过对缩写进行标记，能够为浏览器、拼写检查和搜索引擎提供有用的信息
 * 定义超链接: `<a href="http://www.baidu.com">百度</a>`
 * <style>标签为文档定义样式信息, `<style type="text/css">h1{color: red},p{color: blue}</style>`
 * 为表格定义不同的对齐方式: `<col align="right"></col>`
 * 短语元素:标准属性(id,class.title.style.dir.lang,xml:lang)
    - 强调: <em> <strong>
    - 定义一个定义项目: dfn
    - 定义文本: code(定义计算机代码文本), samp(定义样本文本), kbd(定义键盘文本)
    - 定义变量: var()
    - 定义引用: cite(对参考文献的引用进行定义，书籍或杂志)
 * 标量测量(已知范围或分数值内,gauge): meter，不能用于指示进度，若使用，用<progress>标签: `<meter value="3" min="0" max="10">十分之三</meter><meter value="0.6">60%</meter>`
 * 标签标示任务的进度 `<progress value="22" max="100"></progress>`
 * 下划线: <u></u>,<ins></ins>
 * 删除线: <del></del>,<s></s>,strike
 * 带有记号的文本: <mark></mark>
 * 定义短引用: <q></q>
 * 带有 word break opportunity 的文本: <wbr>单词换行时机</wbr>
 * 文档中的区段: <section></section>
 * 改变字体大小: <big></big>，<small></small>
 * span 标签组合行内元素，当对它应用样式时它才会产生视觉上的变化,应用 id 或者 class 属性
 * <summary> 标签包含 details 元素的标题，"details" 元素用于描述有关文档或文档片段的详细信息。<details><summary>包含在summary里面</summary>details的内容</details>
 * 标签规定独立的自包含内容, <article>独立的自包含内容</article>
 * 作为文章的侧栏定义其所处内容之外的内容: <aside></aside>
 * 规定粗体文本 <b></b>
 * 规定斜体文本 <i></i>
 * 元素可覆盖默认文本的方向 <bdo dir="rtl"></bdo> dir有两个属性 ltr和rtl
 * <blockquote>定义块引用从常规文本中分离出来,左右两边进行缩进</blockquote>
 * 定义嵌入的内容，比如插件 <embed src="helloworld.swf" />
 * 规定文本的字体、字体尺寸、字体颜色 <font size = "3" color="red">This is a text!</font>
 * 规定独立的流内容（图像、图表、照片、代码等等），使用 figcaption 元素为 figure 添加标题 <figure><figcaption>这里面是figcaption</figcaption><img src="..." height="" width=""></figure>
 * `<iframe src="/i/eg_landscape.jpg"></iframe>` 内联框架
 * 标签规定文档的主要内容 <main>,一个文档中,不能出现一个以上的 <main> 元素。<main> 元素不能是<article>、<aside>、<footer>、<header> 或 <nav>元素的后代
 * pre 元素可定义预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体.用来表示计算机的源代码
 * <rt> 标签定义字符（中文注音或字符）的解释或发音。
 * <rp> 标签在 ruby 注释中使用，以定义不支持 ruby 元素的浏览器所显示的内容
 * 向HTML代码添加一个对象:定义一个嵌入的对象。请使用此元素向您的 XHTML 页面添加多媒体。此元素允许您规定插入 HTML 文档中的对象的数据和参数，以及可用来显示和操作数据的代码
    - param 参数定义用于对象的 run-time 设置
    - 不要对图像使用 <object> 标签，使用<img>标签代替