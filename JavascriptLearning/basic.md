JavaScript 的主要用途之一是向浏览站点的人提供反馈

*向用户发出警告，创建一个弹出的警告窗口

// 脚本 2-4
window.onload = writeMessage;
function writeMessage(){	
	document.getElementById("helloMessage").inneerHTML = "Hello, world!";
} 

* 确认用户的选择

if (confirm("Are you sure you want to do that、")) {
	alert("You said yes");
}else{
	alert("You said no");
}; 

* 提示用户

var ans = prompt("Are you sure you want to do that?","");
if (ans) {
	alert("You said"+ans);
};else{ 
	alert("Welcome to my JacaScript page!"); 
}

* 用链接对用户进行重定向 

 <!DOCTYPE html>
 <html>
 <head>
 	<title>Welcome to our site</title>
 	<script src = ></script>
 </head>
 <body>
 	<h2 class= >
 	</h2>
 </body>
 </html>