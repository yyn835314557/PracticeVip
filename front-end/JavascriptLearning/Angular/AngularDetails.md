# Angular 详解

***

Angular 4大核心特性

* MVC
* 模块化
* 指令系统
* 双向数据绑定

<<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8" />
	<title>test</title>
	<script type="text/javascript" src=""></script>
	<script type="text/javascript" src=""></script>
</head>
<body>
	<div ng-controller="BoxCtrl">
		<div style="width: 100px;height: 100px;background-color: red;" ng-click="click()"></div>
		<p>{{w}} x {{h}}</p>
		<p>W:<input type="text" ng-model="w" /></p>
		<p>H:<input type="text" ng-model="h" /></p>
	</div>
	<script type="text/javascript" charset="utf-8">
	var BoxCtrl = function($scope,$element){
		var e = $element.children().eq(0);
		$scope.w = e.width();
		$scope.h = e.height();

		$scope.click = function(){
			$scope.w = parseInt($scope.w) + 10 ;
			$scope.h = parseInt($scope.h) + 10 ;
		}
		$scope.$watch('w',function(to,from){
			e.width(to);
		}
	};
	</script>
</body>
</html>