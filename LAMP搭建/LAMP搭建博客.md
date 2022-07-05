# LAMP搭建博客

## (1)虚拟机的安装

虚拟机：VMware workstation pro 

Linux版本：CentOS7

虚拟机安装教程：

## (2)环境配置

在虚拟机上先下载安装vim

sudo yum -y install vim

安装httpd，会自动安装apache,启动http服务，并设置为开机自动启动

~~~shell
yum -y install httpd
yum -y install wget
yum -y install unzip
~~~

![image-20220705111612971](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705111612971.png)

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705111617616.png" alt="image-20220705111617616"  />



~~~shell
systemctl status httpd  用于列出httpd状态；
systemctl start httpd  用于启动httpd服务；
systemctl enable httpd  将httpd设置为每次开机自动启动。
~~~

![image-20220705111648757](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705111648757.png)

![image-20220705111656189](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705111656189.png)

调用下列代码让防火墙放行

~~~shell
firewall-cmd --add-port=80/tcp --permanent
firewall-cmd --reload
~~~

![image-20220705111740369](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705111740369.png)

现在便可以在浏览器上搜索自己的网址：即自己的ip地址

![image-20220705111835405](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705111835405.png)

## (3)安装PHP

~~~shell
sudo yum -y install php-\* --skip-broken php-mysqlnd
cd /var/www/html
~~~

![image-20220705112040453](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112040453.png)

下载雅黑探针安装

~~~shell
wget http://www.yahei.net/tz/tz.zip
将压缩包解压
unzip tz.zip
~~~

![image-20220705112116600](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112116600.png)

在网址后加/tz.php查看网页

![image-20220705112844296](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112844296.png)

## (4) 安装MARIADB

~~~shell
yum -y install mariadb-server 下载安装mariadb服务；
systemctl status mariadb  用于列出mariadb状态；
systemctl start mariadb  用于启动mariadb服务；
systemctl enable mariadb  将mariadb设置为每次开机自动启动。
mysql_secure_installation  mysql安装安全
~~~

![image-20220705112330345](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112330345.png)

![image-20220705112336329](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112336329.png)

![image-20220705112344343](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112344343.png)

设置root password

mysql -u root -p **

show databases;

create database belog;

show databases;

![image-20220705112524320](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112524320.png)

![image-20220705112528706](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112528706.png)

在网页中的mysql中输入用户名和密码，检测数据库连接是否正常。

![image-20220705112838058](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112838058.png)

![image-20220705112601477](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112601477.png)

## (5) 安装typecho

下载并解压typecho

~~~shell
wget https://github.com/typecho/typecho/releases/download/v0.9-13.12.12-release/0.9.13.12.12.-release.tar.gz
解压
tar -xzvf 0.9.13.12.12.-release.tar.gz
~~~

访问网页 域名为：Linux的ip地址

设置自己博客的数据库的名称和密码，记得将数据库名改成blog，数据库前缀是blog_。

然后点击下一步，就可以发现需要我们自己设置一个默认库，那么我们的操作是在虚拟机里输入：vim config.inc.php 然后将其改成插入模式。将网页上的那部分代码黏贴上去即可。

![image-20220705112719082](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112719082.png)

![image-20220705112722509](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112722509.png)

![image-20220705112726368](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705112726368.png)

查看blog，即可编辑、发表。 

![image-20220705113042207](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705113042207.png)

我们可以对他进行一些美化，在typecho主题模板里可以下载：

再把这个主题包移动到主题下就可以应用主题了。

## (6)内网穿透

打开NATAPP的官网，先注册登录再在右侧购买免费隧道。后下载对应的客户端：

![在这里插入图片描述](https://img-blog.csdnimg.cn/9878df3b08e64aeeba63d653e5ec96a3.png)
选择免费版的使用，注册
![在这里插入图片描述](https://img-blog.csdnimg.cn/08496d84154444eb8372a2ab8ed05971.png)
配置所有的内容
![在这里插入图片描述](https://img-blog.csdnimg.cn/f4efde3131a5467292dc6cc52501c6c3.png)
点击客户端下载
![在这里插入图片描述](https://img-blog.csdnimg.cn/994e11633e1543b5a53d4b97081d67c0.png)

选择linux64位，复制其链接地址[右键复制链接即可获取下载链接](https://cdn.natapp.cn/assets/downloads/clients/2_3_9/natapp_linux_amd64/natapp)，在虚拟机中输入代码：
~~~
cd /var/www/html/
wget https://cdn.natapp.cn/assets/downloads/clients/2_3_9/natapp_linux_amd64/natapp
~~~
然后在官网下载config.ini文件，下载地址:http://download.natapp.cn/assets/downloads/config.ini
~~~
wget http://download.natapp.cn/assets/downloads/config.ini
~~~
那么我们在我的隧道里可以看见自己的购买隧道，可以得知自己的authtoken。然而，并不能直接运行，将获取到的authtoken填入。
![在这里插入图片描述](https://img-blog.csdnimg.cn/6d171c42515b42a1a6c22b7cf072ce4f.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/47bc76ae0de44a05b6ca92247900be1a.png)
此时运行
~~~
./natapp
~~~
出现此图中的内容时可以得知，我们的内网穿透已经成功，他人可以通过链接进入我们的博客。

![在这里插入图片描述](https://img-blog.csdnimg.cn/f89fdaa518cc41a9a65d2559d7b50b2d.png)