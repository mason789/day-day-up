> 将本地项目提交到github上时，默认是将vendor文件夹忽略的，这是我们可以去修改`.gitignore`文件，将最上面的`vendor`去掉
> 有一个`.env`文件，复制自`.env.example`，其中`APP_KEY`要新建一个，在虚拟机项目目录下使用命令`php artisan key:generate`来创建一个
> `git push -f origin master:master `强制提交到origin
> 将本地库提交到github，使用下面两条命令：`git remote add origin https://github.com/mason789/project.git`、`git push -u origin master`