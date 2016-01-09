#基本语法

***

* alert(警告)对话框:
 ```
 <script type="text/javascript">
 	function alertDialog(){
 		var aletMsg = "alert对话弹出内容";
 		alert(aletMsg);
 	}
 </script>
 <<input type="button" onclick="alertDialog()" value="按钮的内容在value上面">
 ```

* confirm(确认)消息对话框:
 ```
 <script type="text/javascript">
 function rec(){
	 var message = confirm("点击确认按钮");
	 if(message == true){
	 	document.write("male"+"<br>");
	 }else{
	 	document.write("female");
	 }
 }
 </script>
 <input name="button" type="button" onclick="rec()" value="按钮上面显示的信息" />
 ```

* prompt(提问)对话框:
 ```
 <script type="text/javascript">
 function promptDialog(){
 	var score = prompt("请输入你的成绩");
 	if (score>=90) {
 		document.write("你很棒！");
 	}else{
 		document.write("要努力了");
 	}
 }
 </script>
 <input type="button" onclick="promptDialog()" value="点击prompt按钮">
 ```

* 打开新的窗口: window.open('','')
 ```
 <script type="text/javascript">
 function openWindow(){
 	window.open('http:www.baidu.com','_blank(top/self)','width=200','height=100','menubar=yes','toolbar=no','scrollbar=no','statusbar=no')
 }
 </script>
 <input name="button" type="button" onclick="openWindow" value="打开新的窗口" />
 ```

* 关闭窗口: window.close() 或者 <窗口对象>.close

* 总结:
 ```
 <script type="text/javascript">
  function openWindow(){
       var message = confirm("是否打开"){
           if(message==true){
               var dialog = prompt("请输入网址","http：//www.imooc.com/"){
                   window.open(dialog,'_blank','width=400','height=500','menubar=no','toolbar=no');
               }
           }
       }
    }
 </script>
 <input name = "button" type="button" onclick="openWindow()" value="请点击按钮" />
 ```