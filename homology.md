**homology文档**
#项目介绍
#快速开始
- 1.一键部署
	按要求装好龙晰系统（Anolis OS7.9）镜像下载地址`https://openanolis.cn/download`
	部署服务器要求
	- CPU内存要求：最低要求4C8G，推荐8C16G
	- 部署目录空间（默认/opt/目录）要求：不低于50G
- 2.安装步骤（离线安装）
	(1).以root用户ssh登录部署目标服务器，创建并进入 /opt/homology，从xxx网站下载安装包到此。
	(2).执行以下命令：
	```shell
	mkdir /opt/homology && cd /opt/homology && ./init-homology.sh
	```
    (3).选择startall初始化机器，这里需要你输入服务器的ip地址。安装脚本默认使用 /opt/homology 目录作为安装目录，homology 的配置文件、数据及日志等均存放在该安装目录。
- 3.激活步骤（离线激活）
	(1).重新执行init-homology.sh脚本，输入getofflinebind参数，会生成机器信息码，用浏览器打开：本机IP/offline_bind.c2d下载离线激活文件，并提供给客服。
	(2).我们会发送给你激活文件，在用浏览器打开：本机IP:8000/form.html 上传离线激活文件（不可重复上传，多次上传请更换文件名），
	(3).执行init-homology.sh脚本，输入offlinebind参数，然后在输入刚刚的离线激活文件名。
	-----
	激活步骤（在线激活）
	确保机器有外网，执行init-homology.sh脚本，输入onlinebind然后输入激活码（激活码可咨询客服获取）。
- 4.重新启动服务
	(1).执行init-homology.sh脚本，选择restartsvc参数，重新启动服务
- 5.登录并使用
	安装成功后,在浏览器打开一下地址页面，输入用户名和密码。
	```
	地址: http://目标服务器IP地址:3011
	用户名: 
	密码: 
	```
- 6.常见问题
	(1).服务器ip有更改
	执行init-homology.sh脚本，输入replaceip，输入新的ip地址。
	(2).web服务需要更新
	从xxx网站下载最新代码包，拷贝替换到/opt/homology/images/目录下，执行init-homology.sh脚本，选择你需要更新的服务
	(3).查看容器状态
	我们提供两种监控方式，一种执行init-homology.sh脚本，输入stats,可以看到服务实时信息。第二种，用浏览器打开：本机IP:8888