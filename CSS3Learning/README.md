# CSS 教程

*yanni.you 2015/12/30 begin*

***

- animation attributes:

 ```CSS
 <style type="text/css">
  	.animation{
 		width: 100px;
 		height: 100px;
 		background: red;
 		position: relative;
		
		/* IE Firefox*/
 		animation: myAnimation 5s ease 2s infinite alternate;
 		/* Chrome and Safari */
 		-webkit-animation: myAnimation 5s ease 2s infinite reverse 
 	}
 	@keyframes myAnimation{
 		from:{top:0px;}
 		to:{top:500px;}
 	}
 	/* Safari and Chrome */
 	@-webkit-keyframes myAnimation{
		0% {top: 0px;}
		50% {top: 200px;}
		100% {top: 250px;}
 	}
 </style>
	<!-- animation-name
		animation-duration
		animation-timeing-function: ease|linear|ease-in|ease-out|ease-in-out 
		animation-delay:
		animation-iteration-count: 
		animation-direction: normal|reverse|alternate|alternate-reverse|initial|inherit
		animation-play-state: pause|running -->
 ```

- background attributes:

 ```CSS
 <style type="text/css">
	body{
		/* background: color position size repeat origin clip attachment image */
		background: #FF0000 url('smile.gif') no-repeat fixed center;
	}
 </style>
	<!-- 
		background-color: red|#FF0000|rgb(255,0,0);
		background-position: x%y%|xposypos|left top left center left bottopm right top center top ;
		background-size: length|percentage|cover|contain;
		background-repeat: repeat|repeat-x|repeat-y|no-repeat|inherit
		background-origin: padding-box|border-box|content-box;
		background-clip: border-box|padding-box|content-box;
		background-attachment: scroll|fixed|inherit;
		background-image: none|inherit|url('');
	 -->
 ```

- Border and Outline attributes:
  
 ```CSS
	<style type="text/css">
		p{
			border: 5px solid red;
		}
	</style>
	<!-- 
	border: border-width border-style border-color
	border-bottom:
	border-bottom-color:
	border-bottom-style:
	border-bottom-width:
	border-color:
	border-left:
	border-left-color: 
	border-left-style:
	border-left-width
	border-right
	border-right-color
	border-right-style
	border-right-width
	border-style
	border-top
	border-top-color
	border-top-style
	border-top-width
	border-width
	ountline
	outline-color
	outline-style
	outline-width
	border-bottom-left-radius
	border-image
	border-image-outset
	border-image-repeat
	border-image-slice
	border-image-source
	border-iamge-width
	border-radius
	border-top-left-raduis
	border-top-right-radius
	box-decoration-break
	box-shadow -->
 ```

- BOX Attributes:

 ```
 <style type="text/css">
	div{
		overflow-x: visible;
	}
 </style>
 <!-- 
	overflow-x: visible/hidden/scroll/auto/no-display/no-content;
	overflow-y: visible/hidden/scroll/auto/no-display/no-content;

  -->
 ```

 - Dimension Attributes:

 ```
   <style type="text/css">
		div{
			height: auto;
			width: auto;
			max-height: inherit;
			max-width: inherit;
			min-height: inherit;
			min-width: inherit;
		}
   </style>
 ```

- Flexible Box:
 
 ```
 <style type="text/css">
	div{
		width: 350px;
		height: 200px;
		border: 1px solid black;

		/* Internet Explorer*/
		display: -ms-flexbox;
		-ms-flex-pack:center;
		-ms-flex-align:center;

		/* Firefox */
		display: -moz-box;
		-moz-box-pack: center;
		-moz-box-align: center;
		
		/* Safari, Opera, and Chrome */
		display: -webkit-box;
		-webkit-box-pack: center;
		-webkit-box-align: center;

	}
 </style>
 ```

- Font Attributes:

 ```
  <style type="text/css">
	p.ex1{
		font: 15px arial,sans-serif;
	}
	p.ex2{
		font: italic bold 12px/30px Georgia,serif;
		/*font: font-style font-variant font-weight font-size/line-height font-family*/
	}
  </style>
  <!-- font-size,font-family is essential
  font-style: normal/italic/oblique/inherit
  font-variant: normal/small-caps/inherit
  font-weight: normal/bold/bolder/lighter
  font-size/line-height: smaller/larger/length/%/inherit
  fobt-family: "Times New Roman",Georgia,Serif;
  font-size-adjust:
  font-stretch:
  @font-face: -->
 ``` 

- Margin Attributes:
 
 ```
  <style type="text/css">
	div{
		margin: 20%;
		margin-top: 1px;
		margin-right: 10%;
		margin-bottom: 1cm;
		margin-left: 20%;
	}
  </style>
 ```

- Multi-column Attributes

 ```
  <style type="text/css">
		div{
			column-count: 3;
			/* Firefox */
			-moz-column-count: 3;
			/* Safari and Chrome */
			-webkit-column-count: 3;
			/*column-width: number|auto;*/
			/* column spacing */
			column-gap: 40px;
			-webkit-column-gap: 100px;
			-moz-column-gap: 110px; 
		}
  </style>
  <!-- 
  	column-rule: column-rule-width column-rule-style column-rule-color;
  	column-rule-style: none|hidden|dotted|dashed|solid|double|groove|ridge|inset|outset;

  	columns: column-width column-count;
  	column-width: 2 
  	column-span: 1|all; -->
 ```
 
- Padding Attributes:
 
 ```
  <style type="text/css">
	p.ex1{padding: 2cm;}
	p.ex2{padding: 20px 20px 20px 20px;}
	p.ex3{padding: 20px 20px 20px;}
	p.ex4{padding: 20% 20p%;}	
  </style>
  <!-- 
	padding-top:
	padding-right:
	padding-bottom:
	padding-left:
   -->
 ```

- Position Attributes:

 ```
  <style type="text/css">
	h2{
		position: absolute;
		left: 100px;
		top: 150px;
		/*right: 20px;*/
		/*bottom: 10px;*/
	}
	img{
		/* 如果先有"overflow：visible"，clip属性不起作用。*/
		clip: rect(0px,60px,200px,0px);
		display: none;
		/* 绝对定位忽略float属性 */
		float: right|none|inherit|left;
		/* 制定元素的左侧或者右侧不允许浮动元素 */
	}
	p.clear{
		/* 制定段落左侧或者右侧不允许浮动元素 */
		clear: none|both|left|right;
		left|right|top|bottom: 
	}
	div{
		width: 150px;
		height: 200p;
		overflow: visible|scroll|hidden|auto|inherit;
		visibility: visible|hidden|collapse|inherit; 
	}
  </style>
  <!-- 
	position: static|absolute|fixed|relative|fixed|relative|inherit
	<span style="cursor:auto|crosshair|default|e-resize|help|mvoe|n-resize|ne-resize|help|move|n-resize|ne-resize|nw-resize|pointer|progress|s-resize|se-resize|sw-resize|text|w-resize|wait"></span>
   -->
 ```

- Transform 2D/3D Attributes:

 ```
  <style type="text/css">
	div{
		transform:rotate(45deg);
		transform-origin:20% 40%;
		/* Safari and Chrome */
		-webkit-transform: rotate(45deg);
		-webkit-transform-origin: 20% 40%;
	}
  </style>
  <!-- 
  transform-origin
  transform-style
  perspective
  perspective-origin
  backface-visibility -->
 ```

- Transition Attributes:

 ```CSS
	<style type="text/css">
		div{
			width: 100px;
			height: 100px;
			transition:width 2s;    

			/* Safari */
			-webkit-transition: width 2s;

			transition-timing-function: ease;
			/* Safari */
			-webkit-transition-timing-function: ease;
		}
		div:hover(width: 300px);
	</style>
	<!-- 
	transition-property: myName;
	transition-duration:0s;
	transition-timing-function: ease;
	transition-delay: 2s; -->
 ```

- User-interface Attributes:

 ```CSS
 	<style type="text/css">
 		
 	</style>
 ```