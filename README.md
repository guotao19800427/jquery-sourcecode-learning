jquery-sourcecode-learning
==========================
version: 2.0.3
整体框架分析
(function(){
    0--start
    finished --- (21, 94) 定义了一些变量和函数 jQuery = function(){}; rquickExpr: <p>aaa 或 #div; rsingleTag:<p></p> <div></div>
    
    finished --- (96, 283) 给jQuery对象添加一些方法和属性 
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
        map()               : 对集合的2次处理，返回新集合, http://jsfiddle.net/tonyguo/hc84ge52/1/
        end()               : 返回集合的前一个状态,
        push()              : (内部使用）,
        sort()              :（内部使用）,
        splice()            : （内部使用）
    }
    
    finished --- (285, 347) extend: JQ的继承(实例)方法 $.extend() = $.fn.extend() (line 284) 
                       当只写一个对象自变量的时候，实际上是在给jQuery写（扩展）插件：
                       $.extend({
                        aaa:function(){
                                alert('1');
                            },
                        bbb:function(){
                                alert('2');
                            }
                       })
                       调用方式: $.aaa();$.bbb();
                       $.fn.extend({
                        aaa:function(){
                                alert('11');
                            },
                        bbb:function(){
                                alert('22');
                            }
                       })
                       调用方式: $().aaa(); $().bbb();
                       http://jsfiddle.net/tonyguo/hc84ge52/6/
                       所以jQuery中的继承用的是copy继承，我们熟悉的还有原型继承（利用原型prototype），类式集成（new 构造函数）
                       
                       
    (349, 817) jQuery.extend(): 扩展一些工具(静态)方法
        expando    : 生成唯一的jQuery字符串（内部），用来做映射关系（通过这个唯一的字符串去映射到相关的变量）,
        noConflict() : 防止冲突, 妈的jsfiddle.net测试因为网速问题，有时候会有病，我在本地做了测试，以后会把本地代码commit上来
        isReady    : DOM是否加载完(内部) DOMContentLoaded（内部）
        readyWait  : 等待多少文件的计数器(内部)
        holdReady()  : hold（不让dom ready）住DOM的ready
        ready()      : 准备DOM触发
        isFunction()   : 是否为函数 http://jsfiddle.net/y90n8zcy/
        isArray()      : 判断是否为数组   
        isWindow()     : 判断是否是window对象
        isNumeric()      : 判断是否是数字 为什么不用typeof(number)? 因为typeof NaN 也返回 number,
        type()         : 判断数据类型,
        isPlainObject()  : 判断是否为对象自变量, (http://jsfiddle.net/y90n8zcy/2/)(http://jsfiddle.net/y90n8zcy/7/)
        isEmptyObject() : 判断是否为空的对象,
        error()        : 抛出异常,
        parseHTML()    : 解析节点,
        parseJSON()    : 解析JSON, (http://jsfiddle.net/y90n8zcy/9/) JSON.parse(),它的反义词是JSON.stringify()
        paeseXML()     : 解析XML,(console.log(xmlDoc);),
        noop()         : no operation  返回空函数  function() {} (function(){}),
        globalEval()   : 全局解析JS--如果把eval存成一个变量，那JS就会把它当作window的属性来用，如果不存变量直接用eval，JS就把它当关键字来用
        camelCase()    : 转驼峰(内部)
        nodeName()     : 判断是不是指定的节点元素(内部), http://jsfiddle.net/tonyguo/7muv3aor/
        each()         : 遍历集合,(针对jQuery对象（数组，类数组--arguments, childNodes, getElementsByTagName等等，JSON对象等等）的循环) file:///D:/test/each.html,
        trim()         : 去字符串前后空格,$.trim('  hello   '),
        makeArray()    : 把所有东西转成数组,file:///D:/test/makeArray.html,
        inArray()      : 数组版的indexOf(),
        merge()        : 合并数组，内部使用时是转换成jQuery格式的JSON：{0:xxx, 1:xxx, 2:xxx, length:3}
                         if ( typeof l === "number" ) {
                			for ( ; j < l; j++ ) {
                				first[ i++ ] = second[ j ];
                			}
                		} else {
                			while ( second[j] !== undefined ) {
                				first[ i++ ] = second[ j++ ];
                			}
                		}
                		if的情况  : $.merge(['a','b'],['c','d']);
                		else的情况: $.merge(['a','b'],{0:'c','1':'d'});
                		file:///D:/test/merge.html
        grep()         : 用第2个参数（函数）过滤第一个参数（数组或类数组），返回新数组,
        map()          : 用第2个参数（函数）遍历处理第一个参数（数组或类数组），得到并返回处理后的新数组,
        guid           : 唯一标识符（内部）,
        proxy()        : 改变this指向,
        access()       : 多功能值操作(内部),用来帮助jquery完成像attr(),css()等这种既能set又能get，还能写JSON参数的方法
        now()          : 获取当前时间,http://jsfiddle.net/tonyguo/93g9yd44/1/,
        swap()         : CSS交换（内部）
        
        
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
