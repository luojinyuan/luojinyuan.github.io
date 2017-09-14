---
layout: post
title: Linux安装mysql教程
---

linux版本：CentOS7

 1.安装包下载

	下载链接：
	http://cdn.mysql.com/archives/mysql-5.6/mysql-5.6.26-linux-glibc2.5-x86_64.tar.gz 

 2.安装依赖
{% highlight java %}
 	yum -y install perl perl-devel autoconf libaio
{% endhighlight %}

 3.把下载的安装包移动到/usr/local/下。

 4.解压安装包(以提供的下载安装包为例)
{% highlight java %}
 	tar zxvf mysql-5.6.26-linux-glibc2.5-x86_64.tar.gz
{% endhighlight %}

 5.复制解压后的mysql目录到系统的本地软件目录

{% highlight java %}
 	cp mysql-5.6.26-linux-glibc2.5-x86_64 /usr/local/mysql -r
{% endhighlight %}

 6.添加系统mysql组和mysql用户
 {% highlight java %}
 	groupadd mysql
 	useradd -r -g mysql -s /bin/false mysql
{% endhighlight %}

 7.进入安装mysql软件目录，修改目录拥有者为mysql用户
{% highlight java %}
 	cd mysql/
 	chown -R mysql:mysql ./
{% endhighlight %}

 8.安装数据库
 {% highlight java %}
 	./scripts/mysql_install_db --user=mysql
{% endhighlight %}

 9.修改当前目录拥有者为root用户
 {% highlight java %}
 	chown -R root:root ./
{% endhighlight %}

 10.修改当前data目录拥有者为mysql用户

{% highlight java %}
 	chown -R mysql:mysql data
{% endhighlight %}
	
============== 到此数据库安装完毕 =============


 11.添加mysql服务开机自启动

 添加开机启动，把启动脚本放到开机初始化目录。

{% highlight java %}
 	cp support-files/mysql.server /etc/init.d/mysql
	# 赋予可执行权限
	chmod +x /etc/init.d/mysql
	# 添加服务
	chkconfig --add mysql 
	# 显示服务列表
	chkconfig --list 
{% endhighlight %}

![screenshot]({{site.url}}/assets/5.png)

如果看到mysql的服务，并且3,4,5都是on的话则成功，如果是off，则执行
{% highlight java %}
 	chkconfig --level 345 mysql on
{% endhighlight %}

 12.启动mysql服务

	#创建缺少的文件夹
 {% highlight java %}
mkdir /var/log/mariadb
service mysql start
{% endhighlight %}
提示 Starting MySQL. SUCCESS!或者OK，即完成启动服务

 13.把mysql客户端放到默认路径
 {% highlight java %}
 	ln -s /usr/local/mysql/bin/mysql /usr/local/bin/mysql
{% endhighlight %}




本文参考链接：<a href="http://www.cnblogs.com/xxoome/p/5864912.html#undefined">http://www.cnblogs.com/xxoome/p/5864912.html#undefined</a>

<a href="http://www.cnblogs.com/phpxiebin/p/4988156.html">http://www.cnblogs.com/phpxiebin/p/4988156.html</a>
<!--![screenshot]({{site.url}}/assets/3.png)-->

<!--![My helpful screenshot]({{site.url}}/assets/1.png)-->