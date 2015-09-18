> 将laravel、homestead、composer等等都安装好以后，新建一个helloworld项目，这个项目是一个blog，在这里记录一下过程以及出现的问题

**[引用1](https://laravist.com/article/12)[引用2](http://9iphp.com/web/laravel/laravel-post-data-to-view.html)**

> 1. 路由与控制器


+ 我们在浏览器中输入helloworld.local的时候,laravel是做了这样一些事情，首先到我们的app/Http/Requests/routs.php下找我们定义的路由，可以看到我们定义的是如果我们访问网站的根目录，那么对调用匿名函数，返回`welcome`视图，或者我们可以定义具体的返回值：
`Route::get('user/{name?}', function ($name = 'lihongsheng') {
    return 'Hello '.$name;
});`
这样我们访问helloworld.local/user就会显示`hello lihongsheng`

+ 可以如何将控制器与路由的定义联系起来呢，我们可以在路由文件中将其他的路由定义都删掉，只剩`Route::get('/','ArticleController@index');`,这就是说，当我们访问我们网站的根目录，会调用ArticleController控制器的index方法，首先我们要创建我们的ArticleController控制器，在项目目录下使用命令`php artisan make:controller ArticleController`创建控制器，然后打开就会看到这个控制器里面自动写入了index、update等方法，在这里我们在index方法中写入`return view('articles.lists');`，就是说会返回articles文件夹下的list视图（.是路径别名，等于/），因此我们进入views文件夹下，使用命令`mkdir articles``vi lists.blade.php`然后esc键入冒号wq就保存退出,然后在里面键入HTML代码，打开helloworld.local就可以看到这个模板所显示的内容了

	**因此，在这里就可以看到路由、控制器与视图的工作流程了，首先注册路由，然后创建控制器，最后在控制器中相应方法加载视图**


> 2. Blade的用法以及向视图中传递变量


+ 向视图中传递变量有以下几种用法：

	（1）`return view('articles.lists',['title'=>$title]);`传递数组，title是key，$title是value
	（2）`return view('articles.lists'）->with('title',$title);`
	（3）使用`return view('articles.lists',compact('title'));`,字符串就是变量的名字
	
+ Blade模板
	**占，以后补充**

> 3. 数据库和Eloquent

+ 在项目文件夹下的config中的database.php配置文件记录了从.env中读入的数据库配置信息，在这里可以对数据库进行配置，为了便于团队协作开发，使用migration来管理数据库，这个就类似于git，使用`php artisan make:migration create_articles_table --create='articles'`命令在database/migrations下建立了一个数据迁移文件，这个文件带有日期标示，以后其他项目组成员要使用你的数据库的话，可以直接根据这个文件来生成,比如在`.env`中设置好数据库名称的话，就可以执行`php artisan migrate`这个命令来在自己的数据库中新建表。需要注意的是，migration提供了很好的数据库管理，甚至数据库的操作都可以回滚，使用`php artisan migrate:rollback`命令来调用迁移文件中的down方法来执行操作，修改完up中的定义以后，再执行`php artisan migrate`就好了

+ 当数据表创建好了以后，我们可以为这个表写一个Model类了，使用`php artisan make:model Article`来创建了一个Article模型，需要注意的是，在模型的创建中，模型名的定义要遵守`数据部复数而模型名单数并且首字母大写`这个规则。建好的模型位于app/Article.php,其中这个类继承自Eloquent/Model类。通过`php artisan tinker`工具提供了一个Eloquent跟数据库表交互的命令行界面，通过这个界面可以直接对数据库表进行操作。比如先实例化一个Article:`$article = new App\Article`,可以对表中字段进行赋值`$article->title='';`