#### 新建一个centos虚拟机

选择自定义高级

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705102546050.png" alt="image-20220705102546050" style="zoom:50%;" />

下一步 ->下一步->选择稍后安装

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705102622078.png" alt="image-20220705102622078" style="zoom:50%;" />



向图中一样配置

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705102655828.png" alt="image-20220705102655828" style="zoom:50%;" />

此处尽量不要放在c盘



根据电脑情况选择处理器数量 不要选择太多。

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705102724725.png" alt="image-20220705102724725" style="zoom:50%;" />

选择4GB即可

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705102753750.png" alt="image-20220705102753750" style="zoom:50%;" />

选择单个文件

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705102842383.png" alt="image-20220705102842383" style="zoom:50%;" />

自定义配件

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705102950414.png" alt="image-20220705102950414" style="zoom:50%;" />

配置

关闭即可 完成安装。





## 配置 安装系统

开启

选择第一个安装

选择语言-建议中文 

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705105526250.png" alt="image-20220705105526250" style="zoom:50%;" />

分别点击  安装位置  和 网络和主机名

一定要搭配好网路设置

进入安装位置 点击完成即可

打开网络 点击完成 (如果此处 无法连接 在windows上打开任务管理器)

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705105605937.png" alt="image-20220705105605937" style="zoom:50%;" />

找到 ssh 启动

![image-20220705105837809](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705105837809.png)

找到vmnetDHCP、VMUSBArbService、VMware NAT Service等启动

![image-20220705105858792](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705105858792.png)

这样即可 开始安装

先设置root密码：

再新建一个个人用户

等待安装完成  重新启动

<img src="C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705110123531.png" alt="image-20220705110123531" style="zoom:50%;" />

进入后先登陆root账户(Linux是隐式密码 不用担心没有输入进去)

![image-20220705110218952](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705110218952.png)

登陆成功

![image-20220705110256318](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705110256318.png)

输入查看网络状态

```shell
ip addr
```

出现ip地址则表示网络已连接

![image-20220705110315117](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20220705110315117.png)

## 配置ssh

yum -y install openssh-server

安装软件

安装完成后

vi /etc/ssh/sshd_config  如图配置 （使用vi的插入模式(进入文件后 按i为插入模式 删除两处的注释，按esc 输入:wq)

~~~ 
port 22
PermitRootLogin yes
~~~



写入成功。

1. 启动ssh服务

   systemctl start sshd.service

2. 重启网络

   service network restart

3. 设置开机启动ssh服务

   systemctl enable sshd.service

到此配置完成