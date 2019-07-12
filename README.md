# zabbix
Bastille Template to create a Zabbix Monitoring Jail

 STATUS:  Testing

first modify the /usr/local/etc/zabbix42/zabbix_agentd.conf file.  Example below:

############ GENERAL PARAMETERS #################

	LogFile=/tmp/zabbix_agentd.log
	SourceIP=192.168.1.11
	Server=192.168.1.13
	ListenIP=192.168.1.11
	Hostname=server.example.net
	Include=/usr/local/etc/zabbix34/zabbix_agentd.conf.d/*.conf



	UserParameter=vfs.zpool.discovery,/usr/local/etc/zabbix34/scripts/zpool-discovery.sh
	UserParameter=vfs.zfs.discovery,/usr/local/etc/zabbix34/scripts/zfs-discovery.sh
	UserParameter=vfs.zfs.get[*],/sbin/zfs get -Hp -o value $2 $1 | sed -e 's/[x%]//'
	UserParameter=vfs.zpool.get[*],/sbin/zpool get -Hp -o value $2 $1 | sed -e 's/[x%]//'


Edit the zabbix_server.conf file and make any necessary modifications. 

	SourceIP=192.168.1.13
	LogType=file
	LogFile=/tmp/zabbix_server.log
	DBHost=db.example.net
	DBName=zabbix
	DBUser=zabbix
	DBPassword=zabbixpw
	StartPollers=50
	StartPreprocessors=6
	StartDiscoverers=10
	Timeout=4
	ExternalScripts=/usr/local/etc/zabbix34/externalscripts
	LogSlowQueries=3000


Now restart the jail and test.
