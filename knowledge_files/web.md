# WEB前端开发知识点梳理  

# 移动端
  - App H5
    - hybrid   
    摘自：https://www.cnblogs.com/dailc/p/5930231.html#hybrid_3_1
      - 多View混合型  
````这种模式主要特点是将webview作为Native中的一个view组件,当需要的时候在独立运行显示,也就是说主体是Native,web技术只是起来一些补充作用,这种模式几乎就是原生开发,没有降低什么难度.````
      - 单View混合型  
````这种模式是在同一个view内,同时包括Native view和webview(互相之间是层叠的关系),比如一些应用会用H5来加载百度地图作为整个页面的主体内容,然后再webview之上覆盖一些原生的view,比如搜索什么的,这种模式开发完成后体验较好,但是开发成本较大,一般适合一些原生人员使用````
      - Web主体型  
````这种模式算是传统意义上的Hybrid开发,很多Hybrid框架都是基于这种模式的,比如PhoneGap,AppCan,Html5+等,这种模式的一个最大特点是,Hybrid框架已经提供各种api,打包工具,调试工具,然后实际开发时不会使用到任何原生技术,实际上只会使用H5和js来编写,然后js可以调用原生提供的api来实现一些拓展功能。往往程序从入口页面,到每一个功能都是h5和js完成的,理论上来说,这种模式应该是最佳的一种模式(因为用H5和js编写最为快速,能够调用原生api,功能够完善),但是由于一些webview自身的限制,导致了这种模式在性能上损耗不小,包括在一些内存控制上的不足,所以导致体验要逊色于原生不少,当然了,如果能解决体验差问题,这种模式应当是最优的(比如由于iOS对H5支持很好,iOS上的体验就很不错)````
      - 多主体共存型（灵活型)  
````这种模式的存在是为了解决web主体型的不足,这种模式的一个最大特点是,原生开发和h5开发共存,也就是说,对于一些性能要求很高的页面模块,用原生来完成,对于一些通用型模块,用h5和js来完成,这种模式通用有跨平台特性,而且用户体验号,性能高,不逊色与原生,但是有一个很大的限制就是,采用这种模式需要一定的技术前提,也就是说这种模式不同于web主体型可以直接用第三方框架,这种模式一般是一些有技术支持的公司自己实现的,包括H5和原生的通信,原生API提供,容器的一些处理全部由原生人员来完成,所以说,使用这种技术的前提是得有专业的原生人员(包括Android,iOS)以及业务开发人员(原生开发负责功能,前端解决简单通用h5功能),当然了,如果技术上没有问题,用这种方案开发出来的App体验是很好的,而且性能也不逊色原生,所以是一种很优的方案````
  - 调试数据接口：mock数据测试
  - 组件库建立：阅读过ui框架源码
  - 系统优化与重构： 无。

# 踩坑指南
  - 熟悉框架


# CSS盒模型

  - 谈谈你对CSS盒模型的认识
    基本概念：标准模型(margin+border+padding+content[content 部分不包含其他部分]) + IE模型(margin+border+padding+content[IE 盒子模型的 content 部分包含了border 和 padding])  
    W3C模型宽：margin+border+padding+width;  
    IE盒模型宽：margin+border+padding+width;  
    box-sizing: content-box(标准模型);  
    box-sizing: border-box(ie模型);  
    BFC(解决边距重叠方案)(块级格式化上下文)  
      - BFC原理  
        1.BFC这个元素垂直方向边距发生重叠  
        2.BFC页面上是一个独立的容器互不干扰
        3.BFC里浮动元素会参与计算
        4.BFC的区域不会与float元素重叠
      - 创建BFC  
        1.overflow:hidden  
        2.float属性不为none
        3.overflow不为visible(可以是hidden、scroll、auto)  
        4.position为absolute或fixed  
        5.display为inline-block、table-cell、table-caption
      - BFC使用场景  

    IFC(内联元素格式化上下文)  

  - JS如何设置获取盒模型对应的宽和高  
    dom.style.width/height(内联样式的宽高/不能取到外联样式的宽高)  
    docm.currentStyle.width/height(获得渲染后的宽高,只有ie支持)  
    window.getComputedStyle(dom).width/height(获得渲染后的宽高)  
    dom.getBoundingClientRect().width/height(获取width/height --- 根据左顶点来获取位置)  

# DOM事件类
  - 基本概念：  
  DOM事件的级别 
    - DOM0  
      - el.onclick=function(){}   
    - DOM2
      - el.addEventListener('click',function(),false)  
    - DOM3  
      - el.addEventListener('keyup',function(){},flase)  

  - DOM事件模型(捕获，目标阶段, 冒泡)  
    ![DOMEVENTLOGO][dom_png]  
    DOM事件流  
    DOM事件捕获的具体流程  
    ````捕获的过程: window -> document -> html -> body -> element````  
    ````冒泡的过程: element -> body -> html -> document -> window````  
    Event对象的常见应用  
    ```javscript
        event.preventDefault() // 阻止默认事件
        event.stopPropagation() // 阻止冒泡行为
        event.stopImmediatePropagation() // element绑定双事件阻止后一个
        event.currentTarget() // 当前所绑定的事件对象
        event.target 
    ``` 
    自定义事件  
    ```javascript
      var eve = new Event('DIYEVENT');
      eve.addEventListener('DIYEVENT', function(){
        console.log(3);
      });
      eve.dispatchEvent(eve);
    ```

# 类型转换
  - 数据类型
    - 原始类型
      - Boolean
      - Null
      - Undefined
      - Number
      - String
      - Symbol
    - 对象
      - Object
  - 显示类型转化
    - Number函数
      - 原始类型转化
        - 数值：数值 -> 数值
        - 字符串： 可以解析数值 -> 数值 否则 转NaN 或者 空字符串 -> 0
        - 布尔值：true -> 1 或者 false -> 0 
        - undefined： undefined -> NaN
        - null：null -> 0
    - String函数
      - 原始类型转化
        - 数值：数值 -> 相对应的字符串
        - 字符串：字符串 -> 字符串
        - 布尔值：true -> "true" | false -> "false"
        - undefined：undefined -> "undefined"
        - null：null -> "null"
    - Boolean函数
      - 原始类型转化
        - undefined：undefined -> false
        - null：null -> false
        - -0：-0 -> false
        - +0：+0 -> false
        - NaN：NaN -> false
        - ''：'' -> false
  - 隐式类型转化
    - 四则运算
     - +,-,*,/
    - 判断语句
     - if, 三目运算
    - Native调用
      - alert, console.log

# HTTP协议类
  - HTTP协议的主要特点
   - 简单快速
    - 通过URI
   - 无连接
    - 连接一次就会断开
   - 无状态
    - 客户端和服务端无法区分两次连接的身份
   - 灵活
    - 通过一个http连接可以完成不同数据的传输
  - HTTP报文的组成部分
    - 请求报文
      - 请求行
        - http方法
        - 页面地址
        - http协议
        - http版本
      - 请求头
        - key,value值
      - 空行
        - 断行
      - 请求体
    - 响应报文
      - 状态行
      - 响应头
      - 空行
      - 响应体
  - HTTP方法
    - GET
      - 获取资源
    - POST
      - 传输资源
    - PUT
      - 更新资源
    - DELETE
      - 删除资源
    - HEAD
      - 获得报文首部
  - POST和GET的区别
    - GET在浏览器回退时是无害的, 而POST会再次提交请求
    - GET产生的URL得知可以被收藏, 而POST不可以
    - GET请求会被浏览器主动缓存, 而POST不会,除非手动设置
    - GET请求只能进行URL编码, 而POST 支持多种编码方式
    - GET请求参数会被完整保留在浏览器历史记录里, 而POST中的参数不会被保留
    - GET请求在URL中的传送的参数是有长度限制, 而POST理论上没有限制
    - 对参数的数据类型, GET只接受ASCII字符,而POST没有限制
    - GET比POST更不安全,因为参数直接暴露在URL上,所以不能用来传输敏感信息
    - GET参数通过URL传递, POST放在Requestbody中
  - HTTP状态码
    - 1xx
      - 指示信息：表示请求已接收,继续处理
    - 2xx
      - 成功：表示请求已被成功接收
        - 200 OK：客户端请求成功
        - 206 Partial Content：客户发送了一个带有Range头的GET请求,服务器完成了它
    - 3xx
      - 重定向：要完成请求必须进行更进一步的操作
        - 301：所请求的页面已经转移到新的URL
        - 302：所请求的页面已经临时转到新的url
        - 304：客户端有缓冲的文档并发出了一个条件性的请求，服务器告诉客户，原来缓冲的文档还可以继续使用
    - 4xx
      - 客户端错误：请求有语法错误或请求无法实现
        - 400：客户端请求有语法错误，不能被服务器所理解
        - 401：请求未经授权，状态码必须和WWW-Authenticate报头域一起使用
        - 403：对被请求页面的访问被禁止
        - 404：请求资源不存在
    - 5xx
      - 服务器错误：服务器未能实现合法的请求
        - 500：服务器发生不可预期的错误原来缓冲的文档还可以继续使用
        - 503：请求未完成，服务器临时过载或宕机,一段时间后可能恢复正常
  - 什么是持久连接(HTTP/1.1才支持)
    - HTTP协议采用"请求-应答"模式,当使用普通模式,即非Keep-Alive模式时,每个请求/应答客户和服务器都要新建一个连接，完成之后立即断开连接(HTTP协议为无状态协议)
    - 当使用Keep-Alive模式(又称持久连接,连接重用)时,Keep-Alive功能使客户端到服务器端的连接持续有效，当出现对服务器的后继请求时，Keep-Alive功能避免了建立或者重新建立连接
  - 什么是管线化
    - 在使用持久连接的情况下,某个连接上消息的传递类似于
      - ````请求1 -> 响应1 -> 请求2 -> 响应2 -> 请求3 -> 响应3````
    - 某个连接上的消息变成了类似这样
      - ````请求1 -> 请求2 -> 请求3 -> 响应1 -> 响应2 -> 响应3````

# 原型链
  - 创建对象
    ```javascript
      var o1 = {name: 'o1'}
      var o11 = new Object({
        name: 'o1'
      });

      var M = function(){
        this.name = 'o2'
      };
      var o2 = new M();

      var P = {name: 'o3'}
      var o3 = Object.create(P);
    
    ```
  - 原型链类
    - 
  - 构造函数
  - 实例
  - 原型链
  - instanceof原理
  - new运算符
# 面向对象
  - 类于实例
    - 类的声明
    - 生成实例
  - 类于继承
    - 如何实现继承
    - 继承的集中方式

# 通信类
  - 同源策略及限制
    - 同源策略限制从一个源加载的文档或脚本如何与来自另一个源的资源进行交互这是一个用于隔离潜在恶意文件的关键安全机制
    - 限制了些什么?
      - Cookie,LocalStorage,IndexDB 无法读取
      - DOM 无法获得
      - AJAX 请求不能发送
    - 源是什么？
      - 协议
      - 端口
      - 域名
  - 前后端如何通信
    - Ajax
      - 同源下通信手段
    - WebSocket
      - 不受同源策略
    - CORS
      - 支持同源
  - 如何创建Ajax
    - XMLHttpRequest对象的工作流程
    - 兼容性处理
    - 事件的触发条件
    - 事件触发的顺序
  - 跨域通信
    - JSONP
      - 
    - Hash
      - 
    - postMessage
      - 
    - WebSocket
      - 
    - CORS
      - 


<!--  -->
[dom_png]: ../static/DOM.png "DOM图片6666"