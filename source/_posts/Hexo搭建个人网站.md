title: 如何使用Hexo搭建个人网站
---
Hello！大家好！今天是公历2015年11月11日，没错，就是花式虐笔者等的节日，欢迎见证Voyager's Website的诞生。
废话不多说，第一篇博客讲讲本网站是如何诞生的吧。
关于购买云服务器、域名、DNS解析什么的还请自行百度，此文开始前假设读者会基本Linux操作命令，并且已经租借了云服务器
# 配置java环境
1. 从oracle官网下载jdk-8u66-linux-x64.gz
2. 通过tar -zxvf jdk-8u66-linux-x64.gz解压文件
	然后为了便与管理，将解压后的文件移动到/opt/java/
3. 配置环境变量
	用vim编辑器编辑/etc/profile文件，如图
4. 检验是否安装成功
	注销重启或者source /etc/profile命令刷新环境变量
	输入java命令，观察是否有如图效果

# 配置apache-tomcat
1. tomcat官网下载apache-tomcat-8.0.28.tar.gz
2. tar解压文件，笔者将其移动到/home/apache-tomcat/
3. 配置环境变量，如图
4. 检验是否安装成功，startup.sh命令开启服务器(不要少了.sh)
	

# 安装GIT
傻瓜式命令操作，不细讲，如图
``` bash
sudo apt-get install git-core
```

# 安装Node.js
这是hexo官方给出的推荐安装方法，不过安装下载速度实在是太慢
The best way to install Node.js is with nvm.
``` bash
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
Once nvm is installed, restart the terminal and run the following command to install Node.js.
$ nvm install 0.12
```
所以笔者采用的是下面的源码编译的方法
1.首先去Node.js官网下载源码包node-v5.0.0.tar.gz
	此处讲个小技巧，就是下载网速慢可以使用百度云的离线下载功能先下载到网盘再从网盘下载
2.tar解压
3.编译源码，漫长的等待...
``` bash
./configure --prefix=/opt/nodejs      #这里可以不指定目录，直接执行./configure命令也可以。
make  #这里有些慢，需要耐心等待
make install
```
4.最后别忘了配置环境变量/opt/nodejs/bin，如图




# 安装hexo
官网https://hexo.io/
已经讲得很清楚了，此处笔者简单概括即可(虽说是英文，但基本都还是很容易理解)
## 安装
``` bash
pm install hexo-cli -g
```
安装完成如图所示
## 初始化
1. hexo init <folder>
2. cd folder
3. npm install
4. npm install hexo-server --save   #解决Cannot GET/问题
5. hexo server
安装到此完成.
