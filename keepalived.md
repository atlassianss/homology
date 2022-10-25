**keepalived部署安装**
- 1. **方案规划**
| VIP | 服务器IP | 默认主从 |
| :----- | :--: | -------: |
|192.168.60.88 | 192.168.60.109 | MASTER |
|192.168.60.88 | 192.168.60.80 | BACKUP |
- 2. **安装**
	- 1. 安装工具：rpm -ivh keepalived-1.3.5-19.el7.x86_64.rpm 离线下载地址：`https://www.keepalived.org/download.html`
	- 2. 开机自启 chkconfig keepalived on
- 3. **修改配置**
	- 1. MASTER配置文件详解，路径/etc/keepalived/keepalived.conf
	```
	! Configuration File for keepalived
	global_defs {
	## keepalived 自带的邮件提醒需要开启 sendmail 服务。 建议用独立的监控或第三方 SMTP
	router_id app01 ## 标识本节点的字条串，通常为 hostname
	} 
	## 定义虚拟路由， VI_1 为虚拟路由的标示符，自己定义名称
	vrrp_instance VI_1 {
	state MASTER ## 主节点为 MASTER， 对应的备份节点为 BACKUP
	interface eth0 ## 绑定虚拟 IP 的网络接口，与本机 IP 地址所在的网络接口相同。
	virtual_router_id 33 ## 虚拟路由的 ID 号， 两个节点设置必须一样， 可选 IP 最后一段使用, 相同的 VRID 为一个组，他将决定多播的 MAC 地址
	mcast_src_ip 192.168.60.109 ## 本机 IP 地址
	priority 200 ## 节点优先级， 值范围 0-254， MASTER 要比 BACKUP 高
	advert_int 1 ## 组播信息发送间隔，两个节点设置必须一样， 默认 1s
	## 设置验证信息，两个节点必须一致
	authentication {
	auth_type PASS
	auth_pass 1111 ## 真实生产，按需求对应该过来
	}
	# 虚拟 IP 池, 两个节点设置必须一样
	virtual_ipaddress {
	192.168.60.88 ## 虚拟 ip，可以定义多个
	}
	}
	```
	- 2. BACKUP节点配置文件
	```
	! Configuration File for keepalived
	global_defs {
	router_id localhost.localdomain
	}
	vrrp_instance VI_1 {
	state BACKUP
	interface eth0
	virtual_router_id 33
	mcast_src_ip 192.168.60.80
	priority 90
	advert_int 1
	authentication {
	auth_type PASS
	auth_pass 1111
	}
	virtual_ipaddress {
	192.168.60.88
	}
	}
	```