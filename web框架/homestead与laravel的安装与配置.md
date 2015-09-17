##homestead与laravel安装

####1. 首先要确保已经安装了虚拟机，VMware或者VirtualBox，并且安装了Vagrant,Vagrant将虚拟的开发环境打包成box，这样无论在什么平台都可以使用。

####2.在终端使用1命令来安装homestead，如果是老版本的vagrant,上面命令会失效，可以使用2命令

同样可以通过克隆代码库来安装homestead，输入3命令，然后在homestead目录运行4命令来创建Homestead.yaml配置文件，这个文件位于"~/.homestead"目录下

`1.vagrant box add laravel/homestead
https://atlas.hashicorp.com/laravel/boxes/homestead`

`2.git clone https://github.com/laravel/homestead.git homestead`

`3.bash init.sh`
####3.配置Homestead
(1)设置平台（提供者）:打开"Homestead.yaml"配置文件，设置"provider:virtualbox"

(2)设置SSH key:在mac或者linux下，你可以通过以下命令来创建一个SSH key,在Homestead.yaml"authorize"中

`ssh-keygen -t rsa -C"you@homestead`

(3)设置共享文件夹：共享文件夹内容的改变会同步到你的本地和Homestead环境中，在"Homestead.yaml"的folders项下进行以下配置：

folders:

map: ~/Code

to: /home/vagrant/Code

type: "nfs"(可选)

(4)配置Nginx

sites:

map: homestead.app

to: /home/vagrant/Code/Laravel/public

hhvm: true

HTTP默认端口8000，HTTPS是44300

(5)配置host文件

修改host文件可以将你的访问请求定向到你的Homestead环境中

host文件位于"/etc/hosts"中（在mac/linux），"C:\windows\system32\drivers\etc\hosts"(Windows)

增加"192.168.10.10 homestead.app",确保这个IP在Homestead.yaml中有设置

配置成功就可以在浏览器中输入"http://homestead.app"来验证了

####4.在完成了对Homestead.yaml的修改后，在Homestead目录下使用以下命令来启动虚拟机

`vagrant up`
####5.将Homestead导入你的项目，通过Composer命令

`composer require laravel/homestead --dev`
安装好了以后，使用"make"命令来生成Vagrantfile和Homestead.yaml文件在你的项目根目录中，"make"命令会自动配置你的站点和共享文件夹

`php vendor/bin/homestead make`

接下来运行"vagrant up"并且在浏览器中查看"http://homestead.app"

需要注意的是不要忘了配置你的/etc/hosts文件

####6.启动虚拟机，这里需要注意的是要在虚拟机的homestead目录,因为vagrant命令需要使用vagrant file

`vagrant up`
####7.查看虚拟机状态以及登陆

`vagrant status`

`vagrant ssh`
####8.可以安装一个Sequel pro来可视化管理数据库

在进行连接时有两种方式，一种是通过虚拟IP地址，另一种是通过端口映射，比如：

SSH: 2222 → Forwards To 22
HTTP: 8000 → Forwards To 80
HTTPS: 44300 → Forwards To 443
MySQL: 33060 → Forwards To 3306
Postgres: 54320 → Forwards To 5432
推荐使用虚拟IP来连接，输入IP地址192.168.10.10、账号Homestead、用户名密码homestead/secret



##通过composer创建项目

###由于composer国内被墙等情况，可以使用国内的镜像站[点这里](http://pkg.phpcomposer.com/)
### 在工作目录works中通过如下命令添加
`composer config -g repositories.packagist composer http://packagist.phpcomposer.com`

###安装好以后，首先建立laravel文件夹，然后可以通过以下命令建立一个laravel项目
`composer create-project laravel/laravel --prefer-dist`  prefer-dist大概是强制安装稳定版本
###注：其实composer所有安装的包都在这里https://packagist.org/packages/laravel/framework#v5.1.16
###安装好以后，这时候laravel下就有了一个laravel，把这个删掉，因为我们定义的目录是/home/vagrant/Works/laravel/helloworld/public这个
`rm -Rf laravel`
###注：通过命令加上--help可以查看命令详情
###然后使用以下命令来创建自己的helloworld项目
`composer create-project laravel/laravel --prefer-dist helloworld`
###这样就建好了helloworld项目


