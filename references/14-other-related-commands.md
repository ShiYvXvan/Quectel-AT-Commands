# 14 其他相关指令 (Other Related Commands)

14 其他相关指令 (Other Related Commands)

14.1. GNSS 相关 AT 指令

有关 GNSS 功能的详细信息，请参阅 Quectel_EC2x&EG9x&EG2x-G&EM05_Series_GNSS_Application_Note。

表 9：GNSS 相关 AT 指令

指令 描述
AT+QGPSCFG GNSS 配置
AT+QGPSDEL 删除辅助数据
AT+QGPS 开启 GNSS
AT+QGPSEND 关闭 GNSS
AT+QGPSLOC 获取定位信息
AT+QGPSGNMEA 获取 NMEA 语句
AT+QGPSXTRA 启用 gpsOneXTRA 辅助功能
AT+QGPSXTRATIME 注入 gpsOneXTRA 时间
AT+QGPSXTRADATA 注入 gpsOneXTRA 数据文件

14.2. DFOTA 相关 AT 指令

有关 DFOTA 功能的详细信息，请参阅 Quectel_EC2x&EG9x&EM05_DFOTA_User_Guide。

表 10：DFOTA 相关 AT 指令

14.3. FTP(S) 相关 AT 指令

有关 FTP(S) 功能的详细信息，请参阅 Quectel_EC2x&EG9x&EG2x-G&EM05_Series_FTP(S)_Application_Note。

表 11：FTP(S) 相关 AT 指令
指令 描述
AT+QFOTADL 通过 DFOTA 升级固件
指令 描述
AT+QFTPCFG 配置 FTP(S) 服务器参数
AT+QFTPOPEN 登录 FTP(S) 服务器
AT+QFTPCWD 配置 FTP(S) 服务器上的当前目录
AT+QFTPPWD 获取 FTP(S) 服务器上的当前目录
AT+QFTPPUT 向 FTP(S) 服务器上传文件
AT+QFTPGET 从 FTP(S) 服务器下载文件
AT+QFTPSIZE 获取 FTP(S) 服务器上的文件大小
AT+QFTPDEL 删除 FTP(S) 服务器上的文件
AT+QFTPMKDIR 在 FTP(S) 服务器上创建文件夹
AT+QFTPRMDIR 删除 FTP(S) 服务器上的文件夹
AT+QFTPLIST 列出 FTP(S) 服务器上目录的内容
AT+QFTPNLIST 列出 FTP(S) 服务器上目录的文件名

14.4. HTTP(S) 相关 AT 指令

有关 HTTP(S) 功能的详细信息，请参阅 Quectel_LTE_Standard_HTTP(S)_Application_Note。

表 12：HTTP(S) 相关 AT 指令

AT+QFTPMLSD 列出标准化的文件和目录信息
AT+QFTPMDTM 获取 FTP(S) 服务器上文件的修改时间
AT+QFTPRENAME 重命名 FTP(S) 服务器上的文件或文件夹
AT+QFTPLEN 获取已传输数据的长度
AT+QFTPSTAT 获取 FTP(S) 服务器的状态
AT+QFTPCLOSE 从 FTP(S) 服务器退出登录
指令 描述
AT+QHTTPCFG 配置 HTTP(S) 服务器参数
AT+QHTTPURL 设置 HTTP(S) 服务器的 URL
AT+QHTTPGET 向 HTTP(S) 服务器发送 GET 请求
AT+QHTTPGETEX 向 HTTP(S) 服务器发送范围 GET 请求
AT+QHTTPPOST 通过 UART/USB 向 HTTP(S) 服务器发送 POST 请求
AT+QHTTPPOSTFILE 通过文件向 HTTP(S) 服务器发送 POST 请求
AT+QHTTPREAD 通过 UART/USB 读取来自 HTTP(S) 服务器的响应
AT+QHTTPREADFILE 通过文件读取来自 HTTP(S) 服务器的响应
AT+QHTTPSTOP 取消 HTTP(S) 请求

14.5. MMS 相关 AT 指令

有关 MMS 功能的详细信息，请参阅 Quectel_LTE_Standard_MMS_Application_Note。

表 13：MMS 相关指令

14.6. SMTP 相关 AT 指令

有关 SMTP 功能的详细信息，请参阅 Quectel_EC2x&EG2x-G&EG9x&EM05_SMTP_Application_Note。

表 14：SMTP 相关 AT 指令

指令 描述
AT+QMMSCFG 配置 MMS 参数
AT+QMMSEDIT 编辑 MMS 消息
AT+QMMSEND 发送 MMS 消息
指令 描述
AT+QSMTPCFG 配置 SMTP 服务器参数
AT+QSMTPDST 添加或删除收件人
AT+QSMTPSUB 编辑电子邮件主题
AT+QSMTPBODY 编辑电子邮件正文
AT+QSMTPATT 为电子邮件添加或删除附件
AT+QSMTPCLR 清除电子邮件内容
AT+QSMTPPUT 发送电子邮件

14.7. TCP(IP) 相关 AT 指令

有关 TCP(IP) 功能的详细信息，请参阅 Quectel_LTE_Standard_TCP(IP)_Application_Note。

表 15：TCP(IP) 相关 AT 指令

指令 描述
AT+QICSGP 配置 TCP/IP 上下文参数
AT+QIACT 激活 PDP 上下文
AT+QIDEACT 去激活 PDP 上下文
AT+QIOPEN 打开 socket 服务
AT+QICLOSE 关闭 socket 服务
AT+QISTATE 查询 socket 服务状态
AT+QISEND 发送数据
AT+QIRD 获取接收到的 TCP/IP 数据
AT+QISENDEX 发送十六进制字符串
AT+QISWTMD 切换数据访问模式
AT+QPING Ping 远程服务器
AT+QNTP 与 NTP 服务器同步本地时间
AT+QIDNSCFG 配置 DNS 服务器地址
AT+QIDNSGIP 通过域名获取 IP 地址
AT+QICFG 配置可选参数
AT+QISDE 控制是否回显 AT+QISEND 的数据
AT+QIGETERROR 查询最后一个错误代码

14.8. SSL 相关 AT 指令

有关 SSL 功能的详细信息，请参阅 EC2x&EG9x&EG2x-G&EM05_SSL_Application_Note。

表 16：SSL 相关 AT 指令

指令 描述
AT+QSSLCFG 配置 SSL 上下文参数
AT+QSSLOPEN 打开 SSL Socket 以连接远程服务器
AT+QSSLSEND 通过 SSL 连接发送数据
AT+QSSLRECV 通过 SSL 连接接收数据
AT+QSSLCLOSE 关闭 SSL 连接
AT+QSSLSTATE 查询 SSL 连接状态
