# web框架基础
### 在学习web框架Laravel的过程中，举步维艰，相关基础知识太薄弱，之前有过接触，但没有完整的了解过，因此将相关知识点总结如下：

#### 1. web的工作方式
#### 当我们在浏览器中输入一个URL的时候，在服务器端的web应用程序会返回一个相应的HTML文件给你。这是web服务器对你请求的一个响应，这种响应模型是基于HTTP协议的。

#### 2. HTTP协议请求方法
#### 在HTTP协议中，每条报文都关联方法，不同的方法代表了你请求的不同意图，比较常见的有GET和POST方法
 
（1）	GET方法

#### GET方法就是从服务器请求数据，web应用程序在对相应的HTML进行响应之外就不要做任何事情了，即这种请求方式不会改变应用的状态，仅用来获取数据而不会对服务器有其他改动，因此这种请求通常被认为是“安全”。
（2） 	POST方法

#### POST方法就是除了简单的查看页面之外，还与网站有着交互的操作，比如创建用户等等。这种方法与GET方法不同的地方在于：不总是生成一个新的HTML页面发送到客户端，而是客户端使用相应的响应码来绝对对应用的操作是否成功。比如200，代表一切正常

**get与post方式区别**

* GET请求数据都可以在URL中看到
* GET提交的数据都会有长度限制
* 一般规范，POST用来修改数据，GET用来获取数据
* GET请求提交的数据放置在HTTP请求协议中，而POST提交的数据则放在实体数据中

（3）	HEAD方法

####获取某个URI响应头信息，基本与GET相同但是不返回响应主体。

（4）	PUT方法

####通过提供的URI获取到特定的内容主体，如果存在则修改内容，如果不存在则创建。

（5）	DELETE方法

####通过URI删除指定内容

（6）	TRACE方法

####返回接受到的请求，用来查看数据经过中间服务器时发生了哪些变动

（7）	OPTIONS方法

####返回给定URL支持的所有HTTP方法

（8）	CONNECT方法

####要求使用SSL和TLS进行TCP通信

（9）	PATCH方法

####请求修改局部数据

#### 3. 路由
#### 路由是处理请求URL到负责生成相关的HTML的代码之间映射的过程。我的理解是，如何解析URL，并调用相应的处理代码来生成客户端所要的HTML页面。比如可以通过解析出POST请求中的"ID"的值，然后调用handle_id()函数来进行响应。可以建立一个映射表，枚举出我们应用所支持的所有URL与他们相关的函数。可是这样又会非常臃肿，因此可以通过给函数传参数的方法来简化。

#### 4. HTML生成
#### 完成了上面的路由过程后，接下里就是HTML页面生成的问题，在通用的web框架中，都是通过专门的view层来处理，这一块还没有学习，只是知道可以有模板引擎之类的可以生成HTML

#### 5. web框架是什么
#### 大概流程就是这样，那么web框架究竟是什么呢？我的理解就是通过框架来将各种基础代码功能进行封装，隐藏了处理HTTP请求和响应相关的过程。那么有的框架比较全面，比如Django/Laravel，但是还有一种微框架，比如Flask/Lumen,其仅仅实现了web应用需要的最小功能，其他的不常用的任务交由第三方库来完成。
### ***不论哪种框架，都是以相同的方式来工作：接受HTTP请求，分配代码（路由），产生HTML，创建带有内容的HTTP响应。***

 > 引用：[点这里](http://www.cnblogs.com/hazir/p/what_is_web_framework.html) 




