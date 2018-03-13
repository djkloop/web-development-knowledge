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
