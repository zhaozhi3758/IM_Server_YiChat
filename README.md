#1、 IM 运行环境
	1. Linux CentOS
	2. Oracle jdk 1.8。

#2、 运行文件部署
##2.1 数据库建表
	1. 在数据库创建数据库tigase，并给tigase库授权用户(建议创建新用户，例如：tigase)。
	2. 导入tigase.sql文件
	3. 执行下面命令，手动创建管理员用户名和密码(可以自定义domian，与init.properties文件中对应，例如 app.im)：call TigAddUserPlainPw('admin@domian',xx);

##2.2 部署文件包tigase.tar.gz
	1. 将tigase.gz解压到/usr/local目录。
	2. 执行ln -s /usr/local/tigase/scripts/tigase.sh /usr/bin/tigase创建软连接。
	3. 修改 /usr/local/tigase/etc/init.properties文件。修改下列数据库连接的相关配置项（ip、port、user、pwd）
	
```
		--admins=admin@domain
		--virt-hosts = domain
		--user-db-uri=jdbc:mysql://ip:port/tigase?user=user&password=pwd&useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull
		#维护apns记录
		sess-man/plugins-conf/urn\:ietf\:params\:xml\:ns\:\xmpp-bind/apns-token-db-uri=jdbc:mysql://ip:port/tigase?user=user&password=pwd&useUnicode=true&characterEncoding=UTF8
```


	4.创建 /usr/local/tigase/etc/init-apns.properties文件。APNs_HTMessage_Dev.p12文件保存在etc目录下
```
		cert_file=APNs_HTMessage_Dev.p12
		#cert_file=htmessage_production_APNs.p12
		#cert_file=HTMessage_Dev_APNs.p12
		pwd=123456
		executor_size=20
		maxConnections=20
```


##2.3 系统相关设置
	1.添加环境变量。修改 /etc/profile 文件，在末尾添加如下，然后执行source /etc/profile 使环境变量立即生效
```
	export TIGASE_HOME=/usr/local/tigase
	export JAVA_HOME=/usr/java/jdk1.8.0_45/
	export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
	export PATH=$JAVA_HOME/bin:$PATH
	
	JAVA_HOME指向jdk实际安装目录
```
	
##2.4 IM服务器的启动，停止，重启
	启动命令： tigase start
 	停止命令： tigase stop
 	
##2.5 登录测试

![](/images/002.jpg)
![](/images/001.jpg))
	
#3.为所有消息加上时间戳 C-101
	 OfflineMessages.java  
	 Message.java	

#4.类型为5000的消息不存库 C-102
	OfflineMessages.java 
	
#5. Apns 相关 C-103
	BindResource.java
	Tigase.apns.*
	MessagePush.java
	
#6.消息回执相关 C-110
	Message.java
	MessageReceipts.java
	Tigase.receipt.*
	
	
	
----------
# 相关工程 #
 
#最具诚意的开源IM系统 YiChat#
1. github地址:[https://github.com/YiChat](https://github.com/YiChat)
2. 开源中国地址:[https://git.oschina.net/zhangfeng_tech](https://git.oschina.net/zhangfeng_tech)


##本项目的开源内容##


###已开源的所有源码:###
1. IM服务器(负责即时通讯消息)-直接部署,无需修改参数
2. api服务器(非IM模块相关的其他业务逻辑)-修改一处参数,详见工程下文档
3. android客户端-配置参数,连接自己的服务器ip.详见工程文档

###待开源的工程源码:###

- iOS客户端:前面三个工程的github star数超过3000马上开源

##这个开源项目的意义在于##
1. 拥有自己的IM服务器,不再受制于第三方通讯云的限制.
2. 提供了一个完善优化的客户端源码,具体参见体验包:
    
 - Android:[https://www.pgyer.com/YiChatLite](https://www.pgyer.com/YiChatLite)
 - iOS:[https://www.pgyer.com/9sVQ](https://www.pgyer.com/9sVQ)


	
##QQ:84543217 (技术相关请提交Issus,商务合作可联系QQ)
	
	
	
	
	
	
	
	

