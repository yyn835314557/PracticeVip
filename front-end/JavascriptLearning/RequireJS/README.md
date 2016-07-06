#Require.JS Essay
*my study diary*
***
###1. define 定义模块

`define(["util","page"],function(util,page){});`

###2. require 加载模块

`require(['./util'],function(){});`

**baseUrl: RequireJS 模块路径解析**
 baseUrl指定一个目录，RequireJS基于这个目录来寻找依赖模块
 `<script src = "js/require.js" data-main = "js/main.js"></script>`
 在 demo.html 里加载 require.js 然后加载 js/main.js,并将 baseUrl 设置为 data-main 指定的文件所在路径，这里是 js/

 ```JavaScript
 requirejs.config({
    baseUrl: 'js/lib',
    paths:{
        // the left side is the module ID,
        // the right side is the path to
        // the jQuery file, relative to baseUrl.
        // Also, the path should NOT include
        // the '.js' file extension. This example
        // is using jQuery 1.9.0 located at
        // js/lib/jquery-1.9.0.js, relative to
        // the HTML page.
        jquery: 'jquery-1.9.0'
    }
 });
 ```

`define([query],function($){});`

