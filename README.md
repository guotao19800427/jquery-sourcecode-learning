jquery-sourcecode-learning
==========================
version: 2.0.3
整体框架分析
(function(){
    (21, 94) 定义了一些变量和函数 jQuery = function(){};
    (96, 283) 给jQuery对象添加一些方法和属性
    (285, 347)extend: JQ的继承方法
    (349, 817)jQuery.extend(): 扩展一些工具方法
    (877, 2856) Sizzle: 复杂选择器的实现
    (8826) window.jQuery = window.$ = jQuery; 向匿名自执行函数外部通过window的方式提供接口
})();
