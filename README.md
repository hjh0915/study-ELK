安装elasticsearch
==================
下载deb安装包
------------
https://www.elastic.co/cn/downloads/elasticsearch

安装
----
~$ sudo dpkg -i elasticsearch-8.8.2-amd64.deb

查看elasticsearch状态
--------------------
~$ service elasticsearch status
*如果出现dead即没启动*

启动elasticsearch
-----------------
~$ sudo service elasticsearch start
*再次查看状态*

检查是否成功运行
--------------
~$ curl --insecure --user elastic:51LWpBOt7LXxENC777wQ https://localhost:9200

使用https打开
------------
~$ sudo curl --cacert /etc/elasticsearch/certs/http_ca.crt --user elastic:51LWpBOt7LXxENC777wQ https://localhost:9200

网页中出现错误即点击“高级”再点击左下方链接进入网页
------------------------------------------
https://localhost:9200
https://192.168.17.128:9200
输入用户名：elastic 
输入密码：51LWpBOt7LXxENC777wQ

安装8.0版本之后出现如下安全设置
===========================
``` shell
--------------------------- Security autoconfiguration information ------------------------------

Authentication and authorization are enabled.
TLS for the transport and HTTP layers is enabled and configured.

The generated password for the elastic built-in superuser is : 51LWpBOt7LXxENC777wQ

If this node should join an existing cluster, you can reconfigure this with
'/usr/share/elasticsearch/bin/elasticsearch-reconfigure-node --enrollment-token <token-here>'
after creating an enrollment token on your existing cluster.

You can complete the following actions at any time:

Reset the password of the elastic built-in superuser with 
'/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic'.

Generate an enrollment token for Kibana instances with 
 '/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana'.

Generate an enrollment token for Elasticsearch nodes with 
'/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s node'.

-------------------------------------------------------------------------------------------------
### NOT starting on installation, please execute the following statements to configure elasticsearch service to start automatically using systemd
 sudo systemctl daemon-reload
 sudo systemctl enable elasticsearch.service
### You can start elasticsearch service by executing
 sudo systemctl start elasticsearch.service
```

elastic 的内置超级用户生成密码是
=============================
The generated password for the elastic built-in superuser is : 51LWpBOt7LXxENC777wQ


安装Kibana
==========
下载deb安装包
------------
https://www.elastic.co/cn/downloads/kibana

安装
----
~$ sudo dpkg -i kibana-8.8.2-amd64.deb

查看kibana状态
-------------
~$ service kibana status
*如果出现dead即没启动*

启动kibana
----------
~$ sudo service kibana start
*再次查看状态*

进入网页写入token
----------------
http://localhost:5601

*从elasticsearch获取token*
~$ sudo /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana

点击右下角后获取验证码
-------------------
~$ journalctl -u kibana.service


启动Kibana
==========
1、先启动elasticsearch
----------------------
~$ sudo service elasticsearch start

2、启动kibana
------------
~$ sudo service kibana start