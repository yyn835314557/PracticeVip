#AngularJS应用解析

Software Development Intern in VIP
***

描述AngularJS应用程序的三个组成部分，并解释它们如何映射到模型-视图-控制器设计模式：

* 模板(Templates): 展现应用的视图
* 应用程序逻辑(Logic)和行为(Behavior)
* 模型数据(Data):

### 核心特性:

- MVC
- Module
- Directive
- Two-Way Data Binding(jQueryUI、BackBone、Flex都是 One-Way Data Binding)

### 调试工具:

- Angular调试插件Batarang

###Problems:

- ng-model: `<div class="remote_div_css" ng-model=""></div>`
- ng-bind: `<span ng-bind="item.attributes"></span>`
- {{attribute}}:


### Angular指令

>Note:
    ```
    <!Doctype>
    <html>
        <head>
            <script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js">
        </script>
        </head>
        <body ng-app="myApp" ng-controller="ctrl">
            {{first + " " + last}}
            <script>
                var app = angular.module("myApp",[]);
                app.controller("",function($scope,$compile,$http){
                    $scope.first = "You";
                    $scope.lastName = "Yinan";
                });
            </script>
        </body>
    </html>

    ```

 + ng-app: 告诉AngularJS应用，当前的这个元素是根元素,所有的ng应用都必须要一个根元素 
 + ng-cloak:
     * 在应用正要加载时防止其闪烁
 + ng-copy:
     * 规定拷贝事件的行为
 + ng-init:
 + ng-bind-html = "test"
     * `$scope.test = "<h1>内嵌HTML</h1>"`
 + ng-bind-template:
     * `<div ng-app="myApp" ng-bind-template="{{firstName}} {{lastName}}" ng-controller="myCtrl"></div>`
 + ng-