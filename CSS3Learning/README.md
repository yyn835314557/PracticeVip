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
	transition-property
	transition-duration
	transition-timing-function
	transition-delay -->
 ```

- Transform 2D/3D Attributes:

 ```
  <style type="text/css">
	div{
		transform:rotate(7deg);
	}
  </style>
 ```

- Transition Attributes:

 ```CSS
 <style type="text/css">
	
 </style>
	<!-- 
	transition-property
	transition-duration
	transition-timing-function
	transition-delay
	 -->
 ```

- User-interface Attributes:

 ```CSS
 	<style type="text/css">
 		s
 	</style>
 ```