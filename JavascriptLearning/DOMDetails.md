#DOM 详解

***

文档对象模型DOM(Document Object Model)定义访问和处理HTML文档的标准方法。DOM将HTML文档呈现为带有元素、属性和文本的树形结构(树节点)。

HTML文档可以说由节点构成的集合，三种常见的DOM节点:
1. 元素节点: 即标签
2. 文本节点: 向用户展示的内容,<li></li>中的JavaScript、DOM、CSS等文本。
3. 属性节点: 元素属性，如<a>标签的链接属性href="http://www.imooc.com"。

* 通过ID获取元素:
 ```
 <p id="con">Javascripr</p>p>
 <script type="text/javascript">
 	var mytest=document.getElementById("con").innerHTML;
 	document.write("结果："+mytest);
 </script>
 ```

* innerHTML 属性: Object.innerHTML
 ```
 <h2 id="con">Javascript</h2>
 <script type="text/javascript">
 	var mychar = document.getElementById("con");
 	document.write(mychar.innerHTML);
 	mychar.innerHTML = "Modify"
 	document.write(mychar.innerHTML);
 </script>
 ```

# 改变 HTML 的样式: Object.style.property
 ```
 <h2 id="con">I love Javascript</h2>
 <script type="text/javascript">
 	var mychar=document.getElementById("con");()
 	mychar.style.color = "red";
 	mychar.style.backgroundColor = "#CCC";
 	mychar.style.width = "300px";
 </script>
 ```

# 显示和隐藏(display属性): Object.style.display
 ```
  <script type="text/javascript"> 
        function hidetext()  
		{  
		var mychar = document.getElementById("con");
            mychar.style.display = none;
		}  
		function showtext()  
		{  
		var mychar = document.getElementById("con");
            mychar.style.display = block;
		}
    </script> 
        <p id="con">做为一个Web开发师来说，如果你想提供漂亮的网页、令用户满意的上网体验，JavaScript是必不可少的工具。</p> 
    <form>
       <input type="button" onclick="hidetext()" value="隐藏内容" /> 
       <input type="button" onclick="showtext()" value="显示内容" /> 
    </form>
 ```

# 控制类名(className属性): object.className
 ```
 <style>
    body{ font-size:16px;}
    .one{
		border:1px solid #eee;
		width:230px;
		height:50px;
		background:#ccc;
		color:red;
    }
	.two{
		border:1px solid #ccc;
		width:230px;
		height:50px;
		background:#9CF;
		color:blue;
	}
 </style>
 <body>
    <p id="p1" > JavaScript使网页显示动态效果并实现与用户交互功能。</p>
    <input type="button" value="添加样式" onclick="add()"/>
	<p id="p2" class="one">JavaScript使网页显示动态效果并实现与用户交互功能。</p>
    <input type="button" value="更改外观" onclick="modify()"/>

	<script type="text/javascript">
	   function add(){
	      var p1 = document.getElementById("p1");
	      p1.className="one";
	   }
	   function modify(){
	      var p2 = document.getElementById("p2");
	      p2.className="two";
	   }
	</script>
</body>
 ```

# 综合测试：
 ```
 <!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" Content="text/html; charset=utf-8" />
<title>javascript</title>
<style type="text/css">
body{font-size:12px;}
#txt{
    height:400px;
    width:600px;
	border:#333 solid 1px;
	padding:5px;}
p{
	line-height:18px;
	text-indent:2em;}
</style>
</head>
<body>
  <h2 id="con">JavaScript课程</H2>
  <div id="txt"> 
     <h5>JavaScript为网页添加动态效果并实现与用户交互的功能。</h5>
        <p>1. JavaScript入门篇，让不懂JS的你，快速了解JS。</p>
        <p>2. JavaScript进阶篇，让你掌握JS的基础语法、函数、数组、事件、内置对象、BOM浏览器、DOM操作。</p>
        <p>3. 学完以上两门基础课后，在深入学习JavaScript的变量作用域、事件、对象、运动、cookie、正则表达式、ajax等课程。</p>
  </div>
  <form>
  <!--当点击相应按钮，执行相应操作，为按钮添加相应事件-->
    <input type="button" value="改变颜色" onclick="changeColor()" /> 
    <input type="button" value="改变宽高" onclick="changeAppearance()" />
    <input type="button" value="隐藏内容" onclick="hideContent()" />
    <input type="button" value="显示内容" onclick="displayContent()" />
    <input type="button" value="取消设置" onclick="cancel()" />
  </form>
  <script type="text/javascript">
//定义"改变颜色"的函数
function changeColor(){
    document.getElementById("con").style.color = "red";
    document.getElementById("con").style.backgroundColor = "green";
}

//定义"改变宽高"的函数
function changeAppearance(){
    document.getElementById("con").style.width = "300px";
    document.getElementById("con").style.height = "50px";
}

//定义"隐藏内容"的函数
function hideContent(){
    document.getElementById("txt").style.display = "none";
}

//定义"显示内容"的函数
function displayContent(){
    document.getElementById("txt").style.display = "block";
}

//定义"取消设置"的函数
function cancel(){

    var tt=document.getElementById("txt");

    var mychose=confirm("是否恢复默认设置？")

    if(mychose==true){

    tt.removeAttribute("style");  

    }
}
</script>
</body>
</html>
 ```