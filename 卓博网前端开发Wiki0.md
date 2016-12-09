# 卓博网前端开发
------

## 一、卓博网总览

### 1. 线上访问地址

> * 个人版 http://www.jobcn.com
> * 企业版 http://hire.jobcn.com
> * 触屏版 http://m.jobcn.com

### 2. 本地开发环境访问地址

> * 个人版 http://*local_ip_address:port*
> * 企业版 http://*local_ip_address:port*
> * 触屏版 http://*local_ip_address:port/touch/*

### 3. 项目结构

以下是个人版项目结构，企业版大同小异
```
|--web/
    |--public/ # 前端JavaScript代码目录
        |--10.0/ # 旧版代码（我也不太清楚，目测已经没有使用了。）
        |--10.2/ # 新版代码（业务代码都放这里）
            |--config.js # seajs的配置文件
            |--p.all.page.js # 业务代码
            |--......
        |--cactus/ # 库、工具
            |--0.1b/ # 组件库
                |--util.js # 常用工具类
                |--ui.widget.box.js # 常用ui组件
                |--......
            |--dic/ # 数据字典
            |--doc/ # 忽略
            |--lib/ # 核心库，如jQuery
            |--test/ # 忽略
        |--script/ # 旧版业务代码（有部分页面有引用）
        |--services/ # 忽略
        |--style/ # 样式文件
        |--util/ # 忽略
        |--build.xml # Ant配置文件（个人版通过Ant对前端代码进行构建）
        |--extract.js # CMD模块依赖提取及更新config.js时间戳（Ant构建过程需要调用）
        |--yuicompressor-2.4.7.jar # YUI压缩包
        |--compiler.jar
    |--touch/ # 触屏版的结构
        |--public/
            |--action/ # 触屏版业务代码
            |--jslib/ # 常用的组件库
            |--min/ # 压缩后的业务代码，发布到线上
            |--node_modules/ # 你懂的，忽略
            |--style/ # 样式文件
            |--Gruntfile.js # 触屏版通过Grunt进行代码构建
            |--package.json
            |--sea-min.js # 触屏版引用的seajs
            |--sea.js # 触屏版的seajs配置文件
```

### 4. 代码构建

__个人版的代码构建__

> 在 Eclipse 中，右键 /web/public/build.xml -> "Run As" -> "Ant Build"

__触屏版的代码构建__

> 1. 打开命令行工具
> 2. 进入目录 /web/touch/pubilc/
> 3. 执行命令 grunt

*注意：*
*1. grunt 构建需要 nodejs 环境，请自行安装 nodejs*
*2. 首次进行构建，需要全局安装 grunt-cli，以及安装相应依赖包*
*3. 全局安装 grunt-cli 命令：npm install grunt-cli -g*
*4. 安装相应依赖包命令：npm install*

## 二、开发流程
------

### 1. 任务分发

前端组组长接收设计中心任务，根据实际情况分配到前端组员手上。前端组组长一位空缺的情况下，由后端开发人员分配任务。

### 2. 编写业务代码

接到任务后，分析文档需求，进行相应业务功能开发。过程中，遇到问题请主动询问相关同事（经理、前端同事、后端同事、设计中心同事）

### 3. 测试

有能力的同事，可以写单元测试。测试过程中，加载开发版代码有两种途径：
> 1. 在 url 后添加参数 *debug=qianduan*
> 2. 使用 Fiddler 搭配代理设置，代理开发版代码

**推荐使用 Fiddler 代理**

### 4. 提交代码到 SVN

> 1. **进行代码压缩构建**
> 2. 同步资源
> 3. 提交相关代码，commit的信息格式：--*任务号* *任务名称* --*开发者姓名*
    ```
    例子：--JOBCNX-2481 简历搜索-浏览过的简历  --卓小博
    ```

### 5. 发送邮件

将自己提交的所有代码，以一下格式规范，发送到研发中心经理邮箱，以便经理打包到内部测试服务器（http://192.168.61.120）

**注意：发送邮件前，需将文件路径进行转换**

> * 个人版的路径以 /web-person/ 开头
> * 企业版的路径以 /web-employer/ 开头

```
--JOBCNX-2480 V2.0简历搜索-智能推荐 --卓小博
--修复  “速配推荐”、“挖掘推荐”切换状态记录有误的问题
/web-employer/WEB-INF/jsp/company/companyJob/comPosList4Box.jsp
/web-employer/WEB-INF/jsp/search/resume/choosePos2Recommend.jsp
/web-employer/WEB-INF/jsp/search/resume/result_content_body.jsp
/web-employer/WEB-INF/jsp/search/resume/resumeMatch.jsp
/web-employer/WEB-INF/jsp/search/resume/resumeMining.jsp
/web-employer/public/10.2/config.js
/web-employer/public/10.2/config.min.js
/web-employer/public/10.2/c.resume.view.js
/web-employer/public/10.2/c.resume.view.min.js
/web-employer/public/10.2/c.search.public.js
/web-employer/public/10.2/c.search.public.min.js
/web-employer/public/10.2/c.search.result.js
/web-employer/public/10.2/c.search.result.min.js
/web-employer/public/style/14.9/search.css
/web-employer/public/style/14.9/resume.css
/web-employer/commImage/10.2/ui/icon/60.png
/web-employer/commImage/10.2/ui/icon/58.png
/web-employer/commImage/10.2/ui/bg/670_300_1.jpg
```

### 6. 功能测试与修复

测试组同事在内部服务器上进行相应的功能测试，反馈问题，相关同事进行问题修复。

## 三、对前端新同事的要求

### 1. 了解前端模块化知识

卓博网前端使用 seajs 进行模块化管理，新同事需要了解并熟悉使用 seajs，[seajs文档](http://seajs.org/docs/#docs)。

### 2. 了解 Node.js 及相关前端构建工具

> * 了解 Node.js 的诞生背景、解决什么问题、以及使用场景
> * 了解流行、常用的前端构建工具：Webpack、Grunt、Gulp（主要会使用 Grunt 或 Gulp）
> * 了解什么是前端工程化

### 3. 了解 Web 开发相关技术知识

> * Web 缓存
> * Cookie、Session、localStorage、sessionStorage
> * 关于浏览器和网络的知识 (http://www.20thingsilearned.com/zh-CN/home)
> * 了解代码管理的使用SVN/Git
> * 简单了解互联网协议： [互联网协议入门一](http://www.ruanyifeng.com/blog/2012/05/internet_protocol_suite_part_i.html)、[互联网协议入门二](http://www.ruanyifeng.com/blog/2012/06/internet_protocol_suite_part_ii.html)
> * [火狐开发者社区-Web Api](https://developer.mozilla.org/en-US/docs/Web/API)

### 4. 知识拓展阅读

> * [JavaScript的运行机制](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)
> * [JavaScript闭包](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)
> * [ECMAScript 6入门](http://es6.ruanyifeng.com/)
> * [JavaScript标准参考教程](http://javascript.ruanyifeng.com/)
> * [JavaScript秘密花园](http://bonsaiden.github.io/JavaScript-Garden/zh/)
> * [jQuery最佳实践](http://www.ruanyifeng.com/blog/2011/08/jquery_best_practices.html)
> * [免费的编程中文书籍索引](https://github.com/justjavac/free-programming-books-zh_CN)
> * [前端资源教程](https://cnodejs.org/topic/56ef3edd532839c33a99d00e)
> * [Chrome浏览器客户端调试大全](http://www.igeekbar.com/igeekbar/post/156.htm?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)

## 四、题外话

善用搜索引擎，当然我说的是 Google :) ，百度只是最后的退路，请学会使用 Google。

用好Chrome开发者工具，学会调试和查看错误信息。

在写代码的同时，要思考如何优化执行效率、如何写好易于维护的代码。

有时候遇到问题，困惑很久，去阳台透透气。跳出问题，再思考问题的表征，猜测其出现的原因。有时候，解决方法不止一个，可以尝试换种途径去实现，不必死磕不放。

拓展自己收集信息的渠道，保持了解开发圈的最新讯息，不论是哪个领域，只要你感兴趣，都可以去了解一下。


推荐几个网站：

> * [伯乐在线](http://jobbole.com/)
> * [开源中国](http://www.oschina.net/)
> * [CNode-Node.js中文社区](https://cnodejs.org/)
> * [阮一峰博客](http://www.ruanyifeng.com/blog/)
> * [博客园](http://www.cnblogs.com/)
> * [开发者头条](https://toutiao.io/)
> * [腾讯前端Alloy Team团队博客](http://www.alloyteam.com/)
> * [百度前端FEX博客](http://fex.baidu.com/)
> * [前端导航网](http://jsdig.com/)
> * [InfoQ](http://www.infoq.com/cn/)
> * [极客学院Wiki](http://wiki.jikexueyuan.com/)