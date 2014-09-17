jquery-sourcecode-learning
==========================
version: 2.0.3
整体框架分析
(function(){
    0--start
    finished --- (21, 94) 定义了一些变量和函数 jQuery = function(){}; rquickExpr: <p>aaa 或 #div; rsingleTag:<p></p> <div></div>
    (96, 283) 给jQuery对象添加一些方法和属性 
    jQuery.fn = jQuery.prototype = {
        jquery              : 版本,
        constructor         : 修正指向问题 jQuery,
        init()              : 初始化和参数管理,
        selector            : 存储选择字符,
        length              : this对象的长度,
        toArray()           : 转数组,
        get()               : 转原生集合,
        pushStack()         : jQuery对象的入栈,(http://jsfiddle.net/tonyguo/hc84ge52/) 以栈的方式转换操作对象（this）
        each()              : 遍历集合,
        ready()             : DOM加载的接口,
        slice()             : 集合的截取,
        first()             : 集合的第一项,
        last()              : 集合的最后一项,
        eq()                : 集合的指定项,
        map()               : 返回新集合, http://jsfiddle.net/tonyguo/hc84ge52/1/
        end()               : 返回集合的前一个状态,
        push()              : (内部使用）,
        sort()              :（内部使用）,
        splice()            : （内部使用）
    }
    
    (285, 347) extend: JQ的继承方法
    (349, 817) jQuery.extend(): 扩展一些工具方法r
    (877, 2856) Sizzle: 复杂选择器的实现
    (2880, 3042) Callbacks: 回调对象--对函数的统一管理(http://jsfiddle.net/tonyguo/xnsuk69f/1/)
    (3043, 3183) Deferred : 延迟对象--对异步的统一管理（http://jsfiddle.net/tonyguo/xnsuk69f/2/）原理就是回调函数
    (3184, 3295) support  : 浏览器功能检测，不按浏览器版本，而是按照浏览器功能来检测
    (3308, 3652) data()   : 数据缓存(http://jsfiddle.net/tonyguo/xnsuk69f/3/) 不是简单的把数据挂载到元素身上
    (3653, 3797) queue()  : 队列管理（入队） dequeue  :  队列管理(出队) (http://jsfiddle.net/tonyguo/xnsuk69f/4/)
    (3803, 4299) attr()方法 prop()方法 val()方法 addClass()方法等等 -- 对元素属性的操作
    (4300, 5128) on() off() trigger() :  事件操作的相关方法
    (5140, 6057) DOM操作 : 添加 appendTo， 删除 remove，获取， 包装 wrap, DOM筛选
    (6058, 6620) css()方法 : 样式操作。为什么这么长？做兼容性，浏览器支持程度等的处理
    (6621, 7854) 提交的数据和ajax() : ajax() load() getJSON()
    (7855, 8584) animate() 运动的方法
    (8585, 8792) offset() width() : 位置和尺寸的方法
    (8804, 8821) jQuery支持模块化的模式
    (8826) window.jQuery = window.$ = jQuery; 向匿名自执行函数外部通过window的方式提供接口
    
    8829--end
})();
