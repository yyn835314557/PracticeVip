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
 	var mychar=document.getElementById("con");
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