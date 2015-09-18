###通过熟悉laravel的目录结构，来学习一下一个完整的web框架都需要哪些东西，具体是如何运作的


####1.`.env`是项目全局变量的配置，根据你的本机服务器或者线上环境需求，可以自由修改环境变量，需要注意的是，这个`.env`文件不应该被提交到版本控制系统，其他人使用可能需要不同的环境配置，因此可以将`.env.example`文件包含到应用程序中，这样其他开发人员可以看到执行你的应用程序所需的环境变量。
	可以使用Application实例的environment方法来取得目前环境
	$environment = $app->environment();
	也可以传参到environment方法中，来确认目前环境与参数是否相符合

* PHP中“：：”代表调用类的静态方法，可以直接使用 类名：：get() 方式来进行调用 
* URI：统一资源标识符（Uniform Resource Identifier，或URI)是一个用于标识某一互联网资源名称的字符串。 该种标识允许用户对任何（包括本地和互联网）的资源通过特定的协议进行交互操作。URI由包括确定语法和相关协议的方案所定义。


> ### 路由

#### 定义所有的HTTP请求处理逻辑
#### 通过调用Route类的相应静态方法，可以对基本的GET、POST等请求进行处理，注册路由、注册路由相应所有HTTP请求
#### 为防止程序受到CSRF（跨网站请求伪造）攻击，可以自动为在用户session中放置随机的token
####HTML 表单没有支持 PUT 、PATCH 或 DELETE 请求。所以当定义 PUT 、PATCH 以及 DELETE 路由并在 HTML 表单中被调用的时候，您将需要添加隐藏 _method 字段在表单中。
#### 可以通过路由获取URL区段，比如ID、NAME等，并且可以限制区段的类型
#### 可以为路由起别名、可以进行路由模型绑定（针对某一个特定的参数）
#### 如果想将路由的设置应用到群组中的所有路由上，可以使用Route::group来定义


> ### 中间件

#### HTTP中间件提供一个方便的机制来过滤进入应用程序的HTTP请求，我的感觉是，可以理解为这就是为HTTP请求提供服务的一个插件，比如身份验证、维护、CSRF保护等,在HTTP请求到达应用程序之前，可以设置许多中间件，这样每一层中间件都可以对请求进行检查，甚至是完全拒绝请求。此外，中间件可以执行在请求执行前，也可以执行在请求执行后，所谓“中间”，即是在整个HTTP请求响应的过程之间提供某种服务
#### 可以通过在请求前后制定Before/After中间件来在请求之前或之后执行一些操作
#### 可以注册中间件来指派特定路由使用，也可以让所有的路由都使用，同时，可以定义“可终止”中间件，这种中间件一般在HTTP响应发送到客户端之后在执行，比如记录Session等


> ### HTTP控制器

#### 控制器可以用来组织路由的行为，是在路由完成HTTP请求处理之后交由控制器来处理，可以注册路由来导向具体的控制器，需要注意的是在注册的时候无需指明完整的控制器命名空间，在类名称`App\Http\Controllers`之后的部分即可用于表示“根”命名空间
#### 可以使用“action”辅助方法来产生一个指向控制器行为的URL
#### 中间件可以在控制器路由中指定，还可以在控制器构造类中指定
#### 可以使用隐式控制器来将HTTP请求与控制器处理整合
#### RESTful资源控制器是基于RESTful架构规范，关于RESTful的详细解释可以点击[这里](http://www.ruanyifeng.com/blog/2011/09/restful.html)，此外，关于路由控制器还有一篇不错的讲解，[在这里](https://phphub.org/topics/688)
#### 依赖注入和控制器感觉是对控制器输入参数的一个限制
#### 可以通过路由缓存来减少注册路由所花的时间

>###HTTP请求  

* 取得请求实例有两种方法，一种是通过Facade,另一种是通过依赖注入，就是在控制器的构造函数或方法中对该类使用类型提示
* 可以取得输入数据通过`Request::input（'name'）`等方法
* 对于旧的输入数据可以通过`flash`方法将其存进`session`中，并且可以保存成一次性`session`
* 如果想取得旧的输入数据，可以通过`Request`实例中的`old`方法，如果想在Blade模板中显示旧输入数据，可以使用辅助方法`old`
* Laravel所建立的cookie会加密并加上认证记号，这样修改过的cookie会失效，可以取得cookie值、加上新的cookie到响应、建立永久有效的cookie
* 可以通过`Request::file()`取得上传的文件，其返回对象是`Symfony\Component\HttpFoundation\File\UploadedFile`类的实例，可以对文件进行有效性判断、移动文件等等
* `Request`还提供很多方法来检查HTTP请求，比如可以取得请求的URI、取得请求方法、确认请求路径是否符合特定格式、取得请求URL


>###HTTP响应

+ 返回完整的响应实例，其实是`Illuminate\Http\Response`类的一个实例，可以自定义响应的HTTP状态吗及响应头，可以使用`new`一个`Response`实例或者使用`response`辅助方法来自定义
+ 如果想要使用`Response`方法但最终返回视图，那么可以使用`view`方法，同时可以使用`withcookie`方法附加cookies到响应，并且，大部分的`Response`方法可以使用链式调用,即`response()->view()->header()->withCookie()`
+ 重定向会产生`RedirectResponse`的实例，并且重定向至新的URL时会一并将数据存进一次性Session中
+ 可以使用`back()`方法重定向到前一个位置
+ 掉用辅助方法`redirect`且不带任何参数时，返回的`Redirector`实例可以调用任何方法，比如重定向到一个路由名称，路由可以带参数
+ 当使用辅助方法`response`不带任何参数时，可以返回`Illuminate\Contracts\Routing\ResponseFactory`的contract实例，可以建立JSON、JSONP响应，并且可以建立文件下载的响应
+ 如果想自定义被很多路由和控制器重复使用的响应，可以使用宏，`Illuminate\Contracts\Routing\ResponseFactory`的方法macro
他会在`ResponseFactory`实例或者辅助方法`response`调用宏名称的时候被执行