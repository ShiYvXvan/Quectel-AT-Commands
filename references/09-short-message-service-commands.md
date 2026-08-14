# 9 短信服务指令 (Short Message Service Commands)

## 9.1. AT+CSMS 选择消息服务 (Select Message Service)

本命令用于选择消息服务 <service>，并返回 ME 支持的消息类型。

测试命令
AT+CSMS=?
响应
+CSMS: (list of supported <service>s)

OK
读取命令
AT+CSMS?
响应
+CSMS: <service>,<mt>,<mo>,<bm>

OK
写入命令
AT+CSMS=<service>
响应
+CSMS: <mt>,<mo>,<bm>

OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性 该命令立即生效。
配置将自动保存。
参考
3GPP TS 27.005

<service> 整型。消息服务类型。
0      3GPP TS 23.040 和 3GPP TS 23.041（短信 AT 指令语法与 3GPP TS 27.005
Phase 2 版本 4.7.0 兼容；支持不需要新指令语法的 Phase 2+ 特性，例如对
使用新 Phase 2+ 数据编码方案的消息进行正确路由）。
1      3GPP TS 23.040 和 3GPP TS 23.041（短信 AT 指令语法与 3GPP TS 27.005
Phase 2+ 版本兼容；<service> 设置为 1 的要求在相应指令描述中说明）。
<mt>  整型。移动终呼（下行）消息。
   0   不支持该类型
   1   支持该类型
<mo>  整型。移动始呼（上行）消息。
   0   不支持该类型
   1   支持该类型
<bm>  整型。小区广播类型消息。
   0   不支持该类型
   1   支持该类型
<err>       错误码。更多详情请参见第 15.5 章。

示例
AT+CSMS=?                        //测试命令。
+CSMS: (0,1)

OK
AT+CSMS=1                                 //将消息服务类型设置为 1。
+CSMS: 1,1,1

OK
AT+CSMS?                                  //读取命令。
+CSMS: 1,1,1,1

OK

## 9.2. AT+CMGF 消息格式 (Message Format)

本命令用于指定短信的输入和输出格式。<mode> 指示在测试、读取、写入和执行命令以及收到消息
所产生的主动上报结果码中所使用的消息格式。

消息格式可以是 PDU 模式（使用完整的 TP 数据单元）或文本模式（消息的报头和正文作为独立参数
给出）。文本模式下，使用 AT+CSCS 命令指定的参数 <chset> 的值，来告知 TA-TE 接口上消息正文
所使用的字符集。

测试命令
AT+CMGF=?
响应
+CMGF: (list of supported <mode>s)

OK
读取命令
AT+CMGF?
响应
+CMGF: <mode>

OK
写入命令
AT+CMGF[=<mode>]
响应
TA 设置参数以指示所使用的消息 I/O 格式。
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置将自动保存。
参考
3GPP TS 27.005

<mode>  整型。
0  PDU 模式
   1  文本模式

## 9.3. AT+CSCA 短信中心地址 (Service Center Address)

该写入命令用于在发送移动始呼短信时更新 SMSC 地址。在文本模式下，该设置用于写入命令。在 PDU
模式下，该设置用于同一命令，但仅在 <pdu> 参数中编码的 SMSC 地址长度等于零时使用。

测试命令
AT+CSCA=?
响应
OK
读取命令
AT+CSCA?
响应
+CSCA: <sca>,<tosca>

OK
写入命令
AT+CSCA=<sca>[,<tosca>]
响应
OK

如果出现与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该命令立即生效。
配置将自动保存。
参考
3GPP TS 27.005

<sca>          短信中心地址。3GPP TS 24.011 RP SC 地址的 Address-Value 字段，以字符串格式
表示；BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的字符
（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <tosca> 给出。
<tosca>        短信中心地址类型。3GPP TS 24.011 RP SC 地址的 Type-of-Address
八位组，以整型格式表示（参见 <toda>）。
<err>            错误码。更多详情请参见第 15.5 章。

示例
AT+CSCA="+8613800210500",145  //设置短信中心地址。
OK
AT+CSCA?        //查询短信中心地址。
+CSCA: "+8613800210500",145

OK

## 9.4. AT+CPMS 首选消息存储 (Preferred Message Storage)

本命令用于选择用于读取、写入等操作的消息存储器 <mem1>、<mem2> 和 <mem3>。

测试命令
AT+CPMS=?
响应
+CPMS: (list of supported <mem1>s),(list of supported
<mem2>s),(list of supported <mem3>s)

OK
读取命令
AT+CPMS?
响应
+CPMS:
<mem1>,<used1>,<total1>,<mem2>,<used2>,<total2>,<mem3>,<used3>,<total3>

OK
写入命令
AT+CPMS=<mem1>[,<mem2>[,<mem3>]]
响应
+CPMS:
<used1>,<total1>,<used2>,<total2>,<used3>,<total3>

OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性 该命令立即生效。
配置将自动保存。
参考
3GPP TS 27.005

参数
<mem1>  字符串类型。从该存储器中读取和删除消息。
    "SM"  (U)SIM 消息存储
    "ME"  移动设备消息存储
    "MT"  与 "ME" 存储相同
    "SR"  短信状态报告存储位置
<mem2>  字符串类型。消息将被写入该存储器并从此存储器发送。
    "SM"  (U)SIM 消息存储
    "ME"  移动设备消息存储
    "MT"  与 "ME" 存储相同
    "SR"  短信状态报告存储位置
<mem3>  字符串类型。如果未设置路由到 PC（AT+CNMI），收到的消息将被放入该存储器。
    "SM"  (U)SIM 消息存储
    "ME"  移动设备消息存储
    "MT"  与 "ME" 存储相同
    "SR"  短信状态报告存储位置
<usedx>  整型。<memx> 中当前消息的数量。
<totalx>      整型。<memx> 中可存储的消息总数。
<err>           错误码。更多详情请参见第 15.5 章。

示例
AT+CPMS?        //查询当前短信消息存储。
+CPMS: "ME",0,255,"ME",0,255,"ME",0,255

OK
AT+CPMS="SM","SM","SM"    //将短信消息存储设置为 "SM"。
+CPMS: 0,50,0,50,0,50

OK
AT+CPMS?        //查询当前短信消息存储。
+CPMS: "SM",0,50,"SM",0,50,"SM",0,50

OK

## 9.5. AT+CMGD 删除消息 (Delete Message)

本命令用于从首选消息存储 <mem1> 的位置 <index> 删除短信。如果提供了 <delflag> 且其值不为 0，
则 ME 应忽略 <index>，并遵循如下所示的 <delflag> 规则。

测试命令
AT+CMGD=?
响应
+CMGD: (range of supported <index>s),(range of supported
<delflag>s)

OK
写入命令
AT+CMGD=<index>[,<delflag>]
响应
TA 从首选消息存储 <mem1> 的位置 <index> 删除消息。
OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间
300 ms。
注：<delflag> 的操作取决于被删除消息的存储位置。
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.005

参数
<index>  整型。相关存储器支持的位置编号。
<delflag> 整型。
0  删除 <index> 中指定的消息
1  从 <mem1> 存储中删除所有已读消息
2  从 <mem1> 存储中删除所有已读消息以及已发送的移动始呼消息
3  从 <mem1> 存储中删除所有已读消息、已发送和未发送的移动始呼消息
   4  从 <mem1> 存储中删除所有消息
<mem1> 字符串类型。从该存储器中读取和删除消息。
   "SM"  (U)SIM 消息存储
   "ME"  移动设备消息存储
   "MT"  与 "ME" 存储相同
<err>       错误码。更多详情请参见第 15.5 章。

示例
AT+CMGD=1       //删除 <index>=1 中指定的消息。
OK
AT+CMGD=1,4       //从 <mem1> 存储中删除所有消息。
OK

## 9.6. AT+CMGL 列出消息 (List Message)

读取命令将首选消息存储 <mem1> 中状态值为 <stat> 的消息返回给 TE。如果消息状态为 "REC
UNREAD"，则存储中的状态将变为 "REC READ"。执行不带状态值 <stat> 的命令 AT+CMGL 时，将
报告状态为 "REC UNREAD" 的短信列表。

测试命令
AT+CMGL=?
响应
+CMGL: (list of supported <stat>s)

OK
写入命令
AT+CMGL[=<stat>]
响应
如果处于文本模式（AT+CMGF=1）且命令执行成功：
对于 SMS-SUBMIT 和/或 SMS-DELIVER：
+CMGL: <index>,<stat>,<oa/da>,[<alpha>],[<scts>][,<tooa/toda>,<length>]<CR><LF><data>[<CR><LF>
+CMGL: <index>,<stat>,<da/oa>,[<alpha>],[<scts>][,<tooa/toda>,<length>]<CR><LF><data>[...]]

对于 SMS-STATUS-REPORT：
+CMGL: <index>,<stat>,<fo>,<mr>,[<ra>],[<tora>],<scts>,<dt>,<st>[<CR><LF>
+CMGL: <index>,<stat>,<fo>,<mr>,[<ra>],[<tora>],<scts>,<dt>,<st>[...]]

对于 SMS-COMMAND：
+CMGL: <index>,<stat>,<fo>,<ct>[<CR><LF>
+CMGL: <index>,<stat>,<fo>,<ct>[...]]

对于 CBM 存储：
+CMGL: <index>,<stat>,<sn>,<mid>,<page>,<pages><CR><LF><data>[<CR><LF>
+CMGL: <index>,<stat>,<sn>,<mid>,<page>,<pages><CR><LF><data>[...]]

OK

如果处于 PDU 模式（AT+CMGF=0）且命令执行成功：
+CMGL: <index>,<stat>,[<alpha>],<length><CR><LF><pdu><CR><LF>
+CMGL: <index>,<stat>,[alpha],<length><CR><LF><pdu>[...]]

OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
执行命令
AT+CMGL
响应
列出消息存储 <mem1> 中所有状态为 "REC UNREAD" 的消息，然后存储中的状态
变为 "REC READ"。
最大响应时间 300 ms。
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.005

参数
<stat>         字符串类型。在文本模式下：
      "REC UNREAD"      已收到未读消息
      "REC READ"         已收到已读消息
      "STO UNSENT"     已存储未发送消息
      "STO SENT"         已存储已发送消息
      "ALL"       所有消息
      整型。在 PDU 模式下：
       0        已收到未读消息
       1        已收到已读消息
       2        已存储未发送消息
       3        已存储已发送消息
         4        所有消息
<index>        整型。相关存储器支持的位置编号。
<da>           目标地址。3GPP TS 23.040 TP-Destination-Address 的 Address-Value 字段，以
 字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
 字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <toda> 给出。
<oa>     始发地址。3GPP TS 23.040 TP-Originating-Address 的 Address-Value 字段，以
字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <tooa> 给出。
<alpha>        字符串类型。<da> 或 <oa> 的字母数字表示，对应于 MT 电话簿中找到的条目。此
功能的实现由制造商规定。使用的字符集应为通过 AT+CSCS 命令选择的字符集（参见
3GPP TS 27.007 中对该命令的定义）。
<scts>      短信中心时间戳。3GPP TS 23.040 TP-Service-Centre-Time-Stamp，以
时间字符串格式表示（参见 <dt>）。
<toda>         收件人地址类型。3GPP TS 24.011 TP-Recipient-Address 的 Type-of-Address
 八位组，以整型格式表示。
<tooa>      始发地址类型。3GPP TS 24.011 TP-Originating-Address 的
 Type-of-Address 八位组，以整型格式表示（默认参见 <toda>）。
<length>   消息长度。整型。指示文本模式（AT+CMGF=1）下消息正文 <data>（或
<cdata>）以字符为单位的长度，或 PDU 模式（AT+CMGF=0）下实际 TP 数据单元以
八位组为单位的长度（即 RP 层的 SMSC 地址八位组不计入长度）。
<data>        对于 SMS：文本模式响应中的 3GPP TS 23.040 TP-User-Data；格式：
-  如果 <dcs>（参见第 9.7 章）指示使用 3GPP TS 23.038 GSM 7 位默认字母表，
并且 <fo>（参见第 9.7 章）指示 3GPP TS 23.040 TP-User-Data-Header-Indication
未设置。
-  如果 TE 字符集不是 "HEX"（参见 3GPP TS 27.007 中的 AT+CSCS 命令）：ME/TA
根据 3GPP TS 27.007 附录 A 的规则将 GSM 字母表转换为当前 TE 字符集。
-  如果 TE 字符集为 "HEX"：ME/TA 将 GSM 7 位默认字母表的每个 7 位字符转换为
两个 IRA 字符长的十六进制数（例如 GSM 7 位默认字母表第 23 号字符表示为
17（IRA 49 和 55））。
-  如果 <dcs> 指示使用 8 位或 UCS2 数据编码方案，或 <fo> 指示 3GPP TS 23.040
TP-User-Data-Header-Indication 已设置：ME/TA 将每个 8 位八位组转换为两个
IRA 字符长的十六进制数（例如整数值为 42 的八位组以两个字符 2A（IRA 50 和
65）呈现给 TE）。
                对于 CBS：文本模式响应中的 3GPP TS 23.041 CBM 消息内容；格式：
             -  如果 <dcs> 指示使用 3GPP TS 23.038 GSM 7 位默认字母表：
-  如果 TE 字符集不是 "HEX"（参见 3GPP TS 27.007 中的 AT+CSCS）：ME/TA
根据 3GPP TS 27.007 附录 A 的规则将 GSM 字母表转换为当前 TE 字符集。
     -  如果 TE 字符集为 "HEX"：ME/TA 将 GSM 7 位默认字母表的每个 7 位字符转换为
       两个 IRA 字符长的十六进制数。
-  如果 <dcs> 指示使用 8 位或 UCS2 数据编码方案：ME/TA 将每个 8 位八位组转换为
两个 IRA 字符长的十六进制数。
<pdu>        对于 SMS：3GPP TS 24.011 SC 地址后跟 3GPP TS 23.040 TPDU，以十六进制
 格式表示：ME/TA 将 TP 数据单元的每个八位组转换为两个 IRA 字符长的十六进制数
 （例如整数值为 42 的八位组以两个字符 2A（IRA 50 和 65）呈现给 TE）。
<fo>  取决于命令或结果码：3GPP TS 23.040 的 SMS-DELIVER、SMS-SUBMIT
（默认 17）、SMS-STATUS-REPORT 或 SMS-COMMAND（默认 2）的第一个八位组，
以整型格式表示。
<mr>  3GPP TS 23.040 TP-Message-Reference，以整型格式表示。
<ra>  3GPP TS 23.040 TP-Recipient-Address 的 Address-Value 字段，以字符串格式表示；
 BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的字符
 （参见 3GPP TS 27.007 中的 +CSCS）；地址类型由 <tora> 给出。
<tora>  3GPP TS 24.011 TP-Recipient-Address 的 Type-of-Address 八位组，以整型格式表示
 （默认参见 <toda>）。
<scts>  3GPP TS 23.040 TP-Service-Centre-Time-Stamp，以时间字符串格式表示（参见 <dt>）
<dt>  3GPP TS 23.040 TP-Discharge-Time，以时间字符串格式表示：
 "yy/MM/dd,hh:mm:ss zz"，其中字符表示年（最后两位）、月、日、时、分、秒和时区。
 例如 1994 年 5 月 6 日 22:10:00 GMT+2 小时等于 "94/05/06,22:10:00+08"。
<st>  3GPP TS 23.040 TP-Status，以整型格式表示。
<ct>  3GPP TS 23.040 TP-Command-Type，以整型格式表示（默认 0）。
<sn>  3GPP TS 23.041 CBM 序列号，以整型格式表示。
<mid>  3GPP TS 23.041 CBM 消息标识符，以整型格式表示。
<page>  3GPP TS 23.041 CBM 页面参数位 4-7，以整型格式表示。
<pages>  3GPP TS 23.041 CBM 页面参数位 0-3，以整型格式表示。
<mem1>  从该存储器中读取和删除消息

示例
AT+CMGF=1        //将短信消息格式设置为文本模式。
OK
AT+CMGL="ALL"      //列出消息存储中的所有消息。
+CMGL: 1,"STO UNSENT","",,
<This is a test from Quectel>
+CMGL: 2,"STO UNSENT","",,
<This is a test from Quectel>
OK

<stat> 的操作取决于所列消息的存储位置。

## 9.7. AT+CMGR 读取消息 (Read Message)

该读取命令将消息存储 <mem1> 中位置值为 <index> 的短信消息返回给 TE。如果消息状态为 "REC
UNREAD"，则存储中的状态将变为 "REC READ"。

测试命令
AT+CMGR=?
响应
OK
写入命令
AT+CMGR=<index>
响应
在非 CDMA 模式下：
如果处于文本模式（AT+CMGF=1）且命令执行成功：
对于 SMS-DELIVER：
+CMGR: <stat>,<oa>,[<alpha>],<scts>[,<tooa>,<fo>,<pid>,<dcs>,<sca>,<tosca>,<length>]<CR><LF><data>

OK

注意

对于 SMS-SUBMIT：
+CMGR: <stat>,<da>,[<alpha>][,<toda>,<fo>,<pid>,<dcs>,[<vp>],<sca>,<tosca>,<length>]<CR><LF><data>

OK

对于 SMS-STATUS-REPORT：
+CMGR: <stat>,<fo>,<mr>,[<ra>],[<tora>],<scts>,<dt>,<st>

OK

对于 SMS-COMMAND：
+CMGR: <stat>,<fo>,<ct>[,<pid>,[<mn>],[<da>],[<toda>],<length><CR><LF><cdata>]

OK
对于 CBM 存储：
+CMGR: <stat>,<sn>,<mid>,<dcs>,<page>,<pages><CR><LF><data>

OK

如果处于 PDU 模式（AT+CMGF=0）且命令执行成功：
+CMGR: <stat>,[<alpha>],<length><CR><LF><pdu>

OK

在 CDMA 文本模式下：
+CMGR: <stat>,<oa/da>,<scts>,<alpha>,<tooa/toda>,<lang>,<fmt>,<length>,<prt>,<prv>,<type><CR><LF><data>

OK
如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 取决于消息内容的长度。
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.005

参数
<index>      整型值，范围为相关存储器支持的位置编号。
<stat>    字符串类型。在文本模式下。
    "REC UNREAD"     已收到未读消息
    "REC READ"      已收到已读消息
    "STO UNSENT"     已存储未发送消息
    "STO SENT"      已存储已发送消息
    "ALL"       所有消息
整型。在 PDU 模式下。
    0        已收到未读消息
    1       已收到已读消息
    2         已存储未发送消息
    3       已存储已发送消息
    4         所有消息
<alpha>       字符串类型。<da> 或 <oa> 的字母数字表示，对应于 MT 电话簿中找到的条目。
此功能的实现由制造商规定。使用的字符集应为通过 AT+CSCS 命令选择的字符集
（参见 3GPP TS 27.007 中对该命令的定义）。
<da>    目标地址。3GPP TS 23.040 TP-Destination-Address 的 Address-Value 字段，以
字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <toda> 给出。
<oa>         始发地址。3GPP TS 23.040 TP-Originating-Address 的 Address-Value 字段，以
字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <tooa> 给出。
<scts>     短信中心时间戳。3GPP TS 23.040 TP-Service-Centre-Time-Stamp，以
时间字符串格式表示（参见 <dt>）。
<fo>           第一个八位组。取决于命令或结果码：3GPP TS 23.040 的 SMS-DELIVER、
SMS-SUBMIT（默认 17）、SMS-STATUS-REPORT 或 SMS-COMMAND 的第一个八位组，
以整型格式表示。如果已输入过一次有效值，则该参数可省略。
<pid>         协议标识符。3GPP TS 23.040 TP-Protocol-Identifier，以整型格式表示（默认 0）。
<dcs>         数据编码方案。取决于命令或结果码：3GPP TS 23.038
SMS 数据编码方案（默认 0），或小区广播数据编码方案，以整型格式表示。
<vp>      有效期。取决于 SMS-SUBMIT <fo> 设置：3GPP TS 23.040
TP-Validity-Period，以整型格式或时间字符串格式表示（参见 <dt>）。
<mn>          消息编号。3GPP TS 23.040 TP-Message-Number，以整型格式表示。
<mr>          消息参考。3GPP TS 23.040 TP-Message-Reference，以整型格式表示。
<ra>           收件人地址。3GPP TS 23.040 TP-Recipient-Address 的 Address-Value 字段，以
字符串格式表示。BCD 号码（或 GSM 默认字母表字符）被转换为当前所选 TE 字符集的
字符（参见 AT+CSCS 命令）。地址类型由 <tora> 给出。
<tora>         收件人地址类型。3GPP TS 24.011 TP-Recipient-Address 的 Type-of-Address
八位组，以整型格式表示（默认参见 <toda>）。
<toda>         收件人地址类型。3GPP TS 24.011 TP-Recipient-Address 的 Type-of-Address
八位组，以整型格式表示。
<tooa>         始发地址类型。3GPP TS 24.011 TP-Originating-Address 的 Type-of-Address
八位组，以整型格式表示（默认参见 <toda>）。
<sca>          短信中心地址。3GPP TS 24.011 RP SC 地址的 Address-Value 字段，以字符串
格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <tosca> 给出。
<tosca>        短信中心地址类型。3GPP TS 24.011 RP SC 地址的 Type-of-Address 八位组，
以整型格式表示（默认参见 <toda>）。
<length>    消息长度。整型。指示文本模式（AT+CMGF=1）下消息正文 <data>（或
<cdata>）以字符为单位的长度，或 PDU 模式（AT+CMGF=0）下实际 TP 数据单元以
八位组为单位的长度（即 RP 层的 SMSC 地址八位组不计入长度）。
<data>         短信的文本内容。详情请参见第 14.8 章。
<pdu>        对于 SMS：3GPP TS 24.011 SC 地址后跟 3GPP TS 23.040 TPDU，以十六进制
格式表示：ME/TA 将 TP 数据单元的每个八位组转换为两个 IRA 字符长的十六进制数
（例如整数值为 42 的八位组以两个字符 2A（IRA 50 和 65）呈现给 TE）。
<prt>          优先级。
0   正常
1   交互式
2   紧急
3   紧急情况
<fmt>          格式。
0   GSM 7 位
   1   ASCII
               6   UNICODE
<prv>         隐私。
0   正常
1   受限
                2   机密
                3   秘密
<lang>       语言。
0   未指定
                1   英语
                2   法语
                3   西班牙语
                4   日语
                5   韩语
                6   中文
                7   希伯来语
<type>         0   正常
                1   CPT
                2   语音信箱
                3   短信报告
<mem1>    字符串类型。从该存储器中读取和删除消息。
      "SM"  (U)SIM 消息存储
      "ME"  移动设备消息存储
      "MT"  与 "ME" 存储相同
<err>          错误码。更多详情请参见第 15.5 章。

示例
+CMTI: "SM",3       //指示已收到新消息并保存到 "SM" 的 <index>=3 位置。
AT+CSDH=1
OK
AT+CMGR=3       //读取消息。
+CMGR: "REC UNREAD","+8615021012496",,"13/12/13,15:06:37+32",145,4,0,0,"+8613800210500",145,27
<This is a test from Quectel>

OK

## 9.8. AT+CMGS 发送消息 (Send Message)

本命令将短信从 TE 发送到网络（SMS-SUBMIT）。调用写入命令后，等待提示符 >，然后开始输入
消息。之后，输入 <CTRL-Z> 表示 PDU 输入结束并开始发送消息。可以通过输入 <ESC> 字符取消
发送。取消会以 OK 确认，但消息不会被发送。消息参考值 <mr> 在消息成功投递时返回给 TE。该值
可用于在收到主动上报的投递状态报告结果码时识别消息。

测试命令
AT+CMGS=?
响应
OK
写入命令
1) 如果处于文本模式（AT+CMGF=1）：
AT+CMGS=<da>[,<toda>]<CR>
响应
TA 将消息从 TE 发送到网络（SMS-SUBMIT）。
消息参考值 <mr> 在消息成功投递时返回给 TE。

参数

输入文本
<Ctrl+Z/ESC>
ESC 退出且不发送

2) 如果处于 PDU 模式（AT+CMGF=0）：
AT+CMGS=<length><CR>
给出 PDU <Ctrl+Z/ESC>
可选地（当 AT+CSMS <service> 值为 1 且网络支持时）会返回 <scts>。该值可用于
在收到主动上报的投递状态报告结果码时识别消息。
如果处于文本模式（AT+CMGF=1）且发送成功：
+CMGS: <mr>

OK

如果处于 PDU 模式（AT+CMGF=0）且发送成功：
+CMGS: <mr>

OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 120 s，由网络决定。
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.005

<da>           目标地址。3GPP TS 23.040 TP-Destination-Address 的 Address-Value 字段，以
 字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
 字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <toda> 给出。
<toda>       收件人地址类型。3GPP TS 24.011 TP-Recipient-Address 的 Type-of-Address
八位组，以整型格式表示。
<length>       整型。指示文本模式（AT+CMGF=1）下消息正文 <data>（或 <cdata>）以字符为
单位的长度，或 PDU 模式（AT+CMGF=0）下实际 TP 数据单元以八位组为单位的长度
（即 RP 层的 SMSC 地址八位组不计入长度）。
 文本模式下的最大长度为 160 字节。
 PDU 模式下的最大长度为 140 字节。
<mr>         消息参考。3GPP TS 23.040 TP-Message-Reference，以整型格式表示。
<err>           错误码。更多详情请参见第 15.5 章。

注意
1. 对于长短信，最大长度将减去用户数据头（UDH）的长度。3GPP TS 23.040 定义了两种 UDH
长度：6 字节和 7 字节，因此两种 <uid> 分别为 8 位（6 字节）和 16 位（7 字节）。AT+QCMGS
使用 8 位 <uid>。
⚫ 对于 GSM 7 位默认字母表数据编码方案，长短信每段的最大长度为 (140 个八位组 - 6) × 8/7=153
个字符。
⚫ 对于 16 位 UCS2 数据编码方案，每段的最大长度为 (140-6)/2=67 个字符。
⚫ 对于 8 位数据编码方案，每段的最大长度为 140-6=134 个字符。
2. <mr>  Message-Reference 字段给出 MS 提交给 SC 的 SMS-SUBMIT 或 SMS-COMMAND 的
  参考号的整数表示，用于确认收到的 SMS-DELIVER 是否与来自 SC 的重复。
<uid>  UDH 的字段。它是长短信的消息标识，不同于 <mr>。长短信中的每个段应具有相同的 <uid>，
  但 <mr> 必须对长短信的每个段递增。
3. AT+QCMGS 不支持在 PDU 模式（AT+CMGF=0）下发送消息。

示例
AT+CMGF=1            //将短信消息格式设置为文本模式。
OK
AT+CSCS="GSM"          //设置 TE 使用的字符集为 GSM。
OK
AT+CMGS="15021012496"
> <This is a test from Quectel>             //输入文本。使用 <CTRL+Z> 发送消息，或使用
<ESC> 退出且不发送。
+CMGS: 247

OK

## 9.9. AT+CMMS 更多消息待发送 (More Messages to Send)

本命令用于控制短信中继协议链路的持续性。如果该功能被启用（且当前使用的网络支持），由于链路
保持打开状态，可以更快地发送多条消息。

测试命令
AT+CMMS=?
响应
+CMMS: (range of supported <n>s)

OK
读取命令
AT+CMMS?
响应
+CMMS: <n>

OK
写入命令
AT+CMMS=<n>
响应
OK
或
ERROR

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 120 s，由网络决定。
特性 该命令立即生效。
配置将自动保存。
参考
3GPP TS 27.005

参数
<n>        整型。
     0   禁用该功能
   1  保持启用，直到最近一条消息发送命令（AT+CMGS、AT+CMSS 等）的响应与下一条
     发送命令之间的时间超过 1-5 秒（具体值由 ME 实现决定），然后 ME 应关闭链路并
     自动将 <n> 切换回 0
   2  启用该功能（如果最近一条消息发送命令的响应与下一条发送命令之间的时间超过
     1-5 秒（具体值由 ME 实现决定），ME 应关闭链路，但 TA 不会自动将 <n> 切换回 0）
<err>       错误码。更多详情请参见第 15.5 章。

注意

执行读取命令后，需要等待 5-10 秒才能发出写入命令。否则可能会出现 +CMS ERROR: 500。

## 9.10. AT+CMGW 将消息写入存储器 (Write Message to Memory)

该写入和执行命令将短信从 TE 存储到存储器 <mem2> 中，然后返回所存储消息的存储位置 <index>。
消息状态默认设置为 "已存储未发送"，但参数 <stat> 也允许指定其他状态值。

输入文本的语法与 AT+CMGS 写入命令中指定的语法相同。

测试命令
AT+CMGW=?
响应
OK
写入命令
1) 如果处于文本模式（AT+CMGF=1）：
AT+CMGW=<oa/da>[,<tooa/toda>[,<stat>]]<CR>
输入文本
<Ctrl+Z/ESC>
<ESC> 退出且不发送

2) 如果处于 PDU 模式（AT+CMGF=0）：
AT+CMGW=<length>[,<stat>]<CR>
给出 PDU <Ctrl+Z/ESC>
响应
如果写入成功：
+CMGW: <index>

OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.005

参数
<da>          目标地址。3GPP TS 23.040 TP-Destination-Address 的 Address-Value 字段，以
字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <toda> 给出。
<oa>          始发地址。3GPP TS 23.040 TP-Originating-Address 的 Address-Value 字段，以
字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <tooa> 给出。
<tooa>        始发地址类型。3GPP TS 24.011 TP-Originating-Address 的 Type-of-Address
八位组，以整型格式表示（默认参见 <toda>）。
<stat>    PDU 模式      文本模式      说明
    0     "REC UNREAD"   已收到未读消息
    1     "REC READ"     已收到已读消息
    2     "STO UNSENT"   已存储未发送消息
    3     "STO SENT"     已存储已发送消息
    4        "ALL"       所有消息
<toda>        收件人地址类型。3GPP TS 24.011 TP-Recipient-Address 的 Type-of-Address
八位组，以整型格式表示。
<length>     消息长度。整型，指示文本模式（AT+CMGF=1）下消息正文 <data>（或 <cdata>）
以字符为单位的长度，或 PDU 模式（AT+CMGF=0）下实际 TP 数据单元以八位组为单位的
长度（即 RP 层的 SMSC 地址八位组不计入长度）。
<pdu>         对于 SMS：3GPP TS 24.011 SC 地址后跟 3GPP TS 23.040 TPDU，以十六进制
格式表示：ME/TA 将 TP 数据单元的每个八位组转换为两个 IRA 字符长的十六进制数
（例如整数值为 42 的八位组以两个字符 2A（IRA 50 和 65）呈现给 TE）。
<index>        所选存储器 <mem2> 中消息的索引。
<err>          错误码。更多详情请参见第 15.5 章。

示例
AT+CMGF=1           //将短信消息格式设置为文本模式。
OK
AT+CSCS="GSM"          //设置 TE 使用的字符集为 GSM。
OK
AT+CMGW="15021012496"
> <This is a test from Quectel>      //输入文本。使用 <CTRL+Z> 写入消息，或使用
           <ESC> 退出且不发送。
+CMGW: 4

OK
AT+CMGF=0                               //将短信消息格式设置为 PDU 模式。
OK
AT+CMGW=18
> 0051FF00000008000A0500030002016D4B8BD5
+CMGW: 5

OK

## 9.11. AT+CMSS 从存储器发送消息 (Send Message from Storage)

该写入命令将消息存储 <mem2> 中位置值为 <index> 的消息发送到网络（SMS-SUBMIT）。如果给定
了新的收件人地址 <da>，则使用该地址代替与消息一起存储的地址。参考值 <mr> 在消息成功投递时
返回给 TE。该值可用于在收到主动上报的投递状态报告结果码时识别消息。

测试命令
AT+CMSS=?
响应
OK
写入命令
AT+CMSS=<index>[,<da>[,<toda>]]
响应
如果处于文本模式（AT+CMGF=1）且发送成功：
+CMSS: <mr>[,<scts>]

OK

如果处于 PDU 模式（AT+CMGF=0）且发送成功：
+CMSS: <mr>[,<ackpdu>]

OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 120 s，由网络决定。
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.005

参数
<index>   整型值，范围为相关存储器支持的位置编号。
<da>           目标地址。3GPP TS 23.040 TP-Destination-Address 的 Address-Value 字段，以
 字符串格式表示。BCD 号码（或 GSM 7 位默认字母表字符）被转换为当前所选 TE 字符集的
 字符（参见 3GPP TS 27.007 中的 AT+CSCS 命令）。地址类型由 <toda> 给出。
<toda>       收件人地址类型。3GPP TS 24.011 TP-Recipient-Address 的 Type-of-Address
八位组，以整型格式表示。
<mr>           消息参考。3GPP TS 23.040 TP-Message-Reference，以整型格式表示。
<scts>       短信中心时间戳。3GPP TS 23.040 TP-Service-Centre-Time-Stamp，以
时间字符串格式表示（参见 <dt>）。

示例
AT+CMGF=1                              //将短信消息格式设置为文本模式。
OK
AT+CSCS="GSM"                        //设置 TE 使用的字符集为 GSM。
OK
AT+CMGW="15021012496"
> Hello                               //输入文本。使用 <CTRL+Z> 发送消息，或使用
            <ESC> 退出且不发送。
+CMGW: 4

OK
AT+CMSS=4                             //从存储器中发送索引为 4 的消息。
+CMSS: 54

OK

## 9.12. AT+CNMA 向 UE/TE 发送新消息确认 (New Message Acknowledgement to UE/TE)

该写入和执行命令确认成功接收了直接路由到 TE 的新消息（SMS-DELIVER 或 SMS-STATUS-REPORT）。
如果 UE 在要求的时间内（网络超时）未收到确认，它将向网络发送 RP-ERROR 消息。UE 将通过把
AT+CNMI 的 <mt> 和 <ds> 值都设置为 0 来自动禁用到 TE 的路由。

测试命令
AT+CNMA=?
响应
+CNMA: (range of supported <n>s)

OK
执行命令
AT+CNMA
响应
OK
或
ERROR

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
写入命令
AT+CNMA=<n>
响应
OK
或
ERROR

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性/
参考
3GPP TS 27.005

参数
<n>   整型。仅 PDU 模式下需要此参数。
      0     该命令的操作与文本模式下类似
      1     向网络发送肯定（RP-ACK）确认。仅接受 PDU 模式
         2     向网络发送否定（RP-ERROR）确认。仅接受 PDU 模式
<ackpdu>       格式与 SMS 情况下的 <pdu> 相同，但不包括 3GPP TS 24.011 SC
地址字段，且该参数应与普通字符串类型参数一样用双引号字符括起来。
<err>   错误码。更多详情请参见第 15.5 章。

执行和写入命令仅应在 AT+CSMS 参数 <service> 等于 1（Phase 2+）且模组已发出相应 URC 时使用，
即：
+CMT 用于 <mt>=2 的入站消息类别 0、1、3 和无；
+CMT 用于 <mt>=3 的入站消息类别 0 和 3；
+CDS 用于 <ds>=1。

示例
AT+CSMS=1
+CSMS: 1,1,1

OK
AT+CNMI=1,2,0,0,0
OK

+CMT: "+8615021012496",,"13/03/18,17:07:21+32",145,4,0,0,"+8613800551500",145,28
This is a test from Quectel.  //当短信到达时直接输出短信内容。

AT+CNMA                          //向网络发送 ACK。
OK
AT+CNMA=<n> 响应
OK
或
ERROR

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性/
参考
3GPP TS 27.005

注意

AT+CNMA
+CMS ERROR：340                //第二次返回错误。只需 ACK 一次。

## 9.13. AT+CNMI 短信事件上报配置 (SMS Event Reporting Configuration)

该写入命令选择当 TE 处于激活状态（例如 DTR 处于低电平（ON））时，如何将网络收到的新消息
指示给 TE 的过程。如果 TE 处于非激活状态（例如 DTR 处于高电平（OFF）），则应按 3GPP TS
23.038 中的规定接收消息。

测试命令
AT+CNMI=?
响应
+CNMI: (range of supported <mode>s),(range of supported
<mt>s),(list of supported <bm>s),(range of supported
<ds>s),(list of supported <bfr>s)

OK
读取命令
AT+CNMI?
响应
+CNMI: <mode>,<mt>,<bm>,<ds>,<bfr>

OK
写入命令
AT+CNMI[=<mode>[,<mt>[,<bm>[,<ds>[,<bfr>]]]]]
响应
OK
或
ERROR

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性 该命令立即生效。
配置将自动保存。
参考
3GPP TS 27.005

参数
<mode>     整型。
  0      将主动上报结果码缓冲在 TA 中。如果 TA 结果码缓冲区已满，指示可以缓冲在
其他位置，或丢弃最旧的指示并用新收到的指示替换。
              1      当 TA-TE 链路被占用（例如处于在线数据模式）时，丢弃指示并拒绝新收到的
消息主动上报结果码。否则直接转发给 TE。
              2      当 TA-TE 链路被占用（例如处于数据模式）时，将主动上报结果码缓冲在 TA 中，
并在链路释放后将其发送给 TE。否则直接转发给 TE。
<mt>       整型。接收短信的存储规则取决于其数据编码方案（参见 3GPP TS 23.038）和首选
存储器（AT+CPMS）设置，其值为：
              0  不将 SMS-DELIVER 指示路由到 TE。
 1 如果 SMS-DELIVER 存储到 ME/TA 中，则通过主动上报结果码
 +CMTI: <mem>,<index> 将存储位置指示路由到 TE。
 2 SMS-DELIVER（类别 2 除外）直接通过主动上报结果码路由到 TE：
 +CMT: [<alpha>],<length><CR><LF><pdu>（启用 PDU 模式）
 或 +CMT: <oa>,[<alpha>],<scts>[,<tooa>,<fo>,<pid>,<dcs>,<sca>,<tosca>,
 <length>]<CR><LF><data>（启用文本模式；关于斜体参数，参见 AT+CSDH）或
 ^HCMT: <oa>,<scts>,<lang>,<fmt>,<length>,<prt>,<prv>,<type>,<stat><CR><LF><data>
 （CDMA 短信的文本模式）。类别 2 消息按照 <mt>=1 中定义的指示处理。
 3 类别 3 的 SMS-DELIVER 通过 <mt>=2 中定义的主动上报结果码直接路由到 TE。
 其他类别的消息按照 <mt>=1 中定义的指示处理。
<bm>       整型。接收 CBM 的存储规则取决于其数据编码方案（参见 3GPP TS 23.038）和
选择 CBM 类型（AT+CSCB）的设置，其值为：
             0    不将 CBM 指示路由到 TE。
             2  新 CBM 直接通过主动上报结果码路由到 TE：
  +CBM: <length><CR><LF><pdu>（PDU 模式）；
 或 +CBM: <sn>,<mid>,<dcs>,<page>,<pages><CR><LF><data>（文本模式）
<ds>       整型。
    0       不将 SMS-STATUS-REPORT 路由到 TE。
          1       通过主动上报结果码将 SMS-STATUS-REPORT 路由到 TE：
                    +CDS: <length><CR><LF><pdu>（PDU 模式）
                    +CDS: <fo>,<mr>,[<ra>],[<tora>],<scts>,<dt>,<st>（文本模式）
             2       如果 SMS-STATUS-REPORT 存储到 ME/TA 中，则通过主动上报结果码
               将存储位置指示路由到 TE：
                    +CDSI: <mem>,<index>
<bfr>       整型。
 0      当输入 <mode> 1 或 2 时，将本命令定义的主动上报结果码的 TA 缓冲区发送给 TE
（应在发送这些结果码之前给出 OK 响应）。
             1  当输入 <mode> 1 或 2 时，清除本命令定义的主动上报结果码的 TA 缓冲区。
<err>       错误码。更多详情请参见第 15.5 章。

主动上报结果码：
+CMTI: <mem>,<index>        指示已收到新消息
+CMT: [<alpha>],<length><CR><LF><pdu>  直接输出短信内容
+CBM: <length><CR><LF><pdu>    直接输出小区广播消息内容

示例
AT+CMGF=1                           //将短信消息格式设置为文本模式。
OK
AT+CSCS="GSM"                     //设置 TE 使用的字符集为 GSM。
OK
AT+CNMI=1,2,0,1,0                    //设置 SMS-DELIVER 直接路由到 TE。
OK

+CMT: "+8615021012496",,"13/03/18,17:07:21+32",145,4,0,0,"+8613800551500",145,28
This is a test from Quectel.           //当短信到达时直接输出短信内容。

## 9.14. AT+CSCB 选择小区广播消息类型 (Select Cell Broadcast Message Types)

该写入命令用于选择 ME 接收哪些类型的 CBM。

测试命令
AT+CSCB=?
响应
+CSCB: (list of supported <mode>s)

OK
读取命令
AT+CSCB?
响应
+CSCB: <mode>,<mids>,<dcss>

OK
写入命令
AT+CSCB=<mode>[,mids>[,<dcss>]]
响应
OK

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性 该命令立即生效。
配置将自动保存。
参考
3GPP TS 27.005

注意

配置存储在 NVM 中。
参数

<mode>  整型。
   0  接受 <mids> 和 <dcss> 中指定的消息类型
   1  不接受 <mids> 和 <dcss> 中指定的消息类型
<mids> 字符串类型。CBM 消息标识符的所有不同可能组合（参见 <mid>）（默认为空字符串），
例如 "0,1,5,320-478,922"
<dcss> 字符串类型。CBM 数据编码方案的所有不同可能组合（参见 <dcs>）（默认为空字符串），
例如 "0-3,5"
<err>       错误码。更多详情请参见第 15.5 章。

## 9.15. AT+CSDH 显示短信文本模式参数 (Show SMS Text Mode Parameters)

该写入命令用于控制是否在文本模式结果码中显示详细的报头信息。

测试命令
AT+CSDH=?
响应
+CSDH: (list of supported <show>s)

OK
读取命令
AT+CSDH?
响应
+CSDH: <show>

OK
写入命令
AT+CSDH[=<show>]
响应
OK
或
ERROR
最大响应时间 300 ms
特性/
参考
3GPP TS 27.005

注意

参数
<show>     整型。
   0  不在文本模式下 SMS-DELIVER 和 SMS-SUBMIT 的 +CMT、+CMGL、+CMGR 结果码中
    显示 +CSCA、+CSMP（<sca>、<tosca>、<fo>、<vp>、<pid>、<dcs>）命令中定义的
    报头值以及 <length>、<toda> 或 <tooa> 值
  1  在结果码中显示这些值

示例
AT+CSDH=0
OK
AT+CMGR=2
+CMGR: "STO UNSENT","",
<This is a test from Quectel>
OK
AT+CSDH=1
OK
AT+CMGR=2
+CMGR: "STO UNSENT","",,128,17,0,0,143,"+8613800551500",145,18
<This is a test from Quectel>
OK

## 9.16. AT+CSMP 设置短信文本模式参数 (Set SMS Text Mode Parameters)

本命令用于设置在文本模式下将短信发送到网络或存入存储器时所需的附加参数值。

测试命令
AT+CSMP=?
响应
OK
读取命令
AT+CSMP?
响应
+CSMP: <fo>,<vp>,<pid>,<dcs>

OK
写入命令
AT+CSMP=<fo>[,<vp>[,<pid>[,<dcs>]]]
响应
TA 为在文本模式（AT+CMGF=1）下将短信发送到网络或存入存储器时所需的附加参数
选择值。可以设置从 SMSC 收到短信时开始计算的有效期（<vp> 范围为 0 到 255），
或定义有效期终止的绝对时间（<vp> 为字符串）。
OK
最大响应时间 300 ms
特性/
参考
3GPP TS 27.005

参数
<fo>          第一个八位组。取决于命令或结果码：3GPP TS 23.040 的
SMS-DELIVER、SMS-SUBMIT（默认 17）、SMS-STATUS-REPORT、SMS-COMMAND
的第一个八位组，以整型格式表示。如果已输入过一次有效值，则可省略该参数。
<vp>        有效期。取决于 SMS-SUBMIT <fo> 设置：3GPP TS 23.040
TP-Validity-Period，以整型格式或时间字符串格式表示（参见 <dt>）。
<pid>          协议标识符。3GPP TS 23.040 TP-Protocol-Identifier，以整型格式表示（默认 0）。
<dcs>         数据编码方案。取决于命令或结果码：3GPP TS 23.038
SMS 数据编码方案（默认 0），或小区广播数据编码方案，以整型格式表示。

## 9.17. AT+QCMGS 发送长短信（合并短信） (Send Concatenated Messages)

本命令用于发送长短信。与 AT+CMGS 不同，通过本命令发送长短信时，长短信的每个段都必须通过
附加参数 <uid>、<msg_seg> 和 <msg_total> 标识。当逐个发送消息的所有段时，必须为每个段执行
多次 AT+QCMGS（次数等于 <msg_total>）。此命令仅在文本模式（AT+CMGF=1）下使用。

测试命令
AT+QCMGS=?
响应
OK
写入命令
如果处于文本模式（+CMGF=1）：
AT+QCMGS=<da>[,<toda>],<uid>,<msg_seg>,<msg_total><CR>
输入文本
<Ctrl+Z/ESC>
响应
如果处于文本模式（AT+CMGF=1）且发送成功：
+QCMGS: <mr>

OK
或
ERROR

如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 120 s，由网络决定。
特性/
注意

参数
<uid>              整型。用户数据头（UDH）中的消息标识。范围：0–255。该参数由用户
定义和输入。同一条长短信的所有段必须具有相同的 <uid>。不同的长短信应具有
不同的 <uid>。
<msg_seg>          整型。长短信的序列号。范围：0–7。
 <msg_seg>=0 表示：忽略该值，将其视为非合并消息。
<msg_total>         整型。一条长短信的段总数。范围：0–7。<msg_total>=0 或 1 表示：
忽略该值，将其视为非合并消息。
<da>                请参见 AT+CMGS。
<toda>              请参见 AT+CMGS。
<mr>                请参见 AT+CMGS。
<err>                整型。有关错误码的详细信息，请参见第 15.5 章。

注意
1. 对于长短信，最大长度将减去用户数据头（UDH）的长度。3GPP TS 23.040 定义了两种 UDH
长度：6 字节和 7 字节，因此两种 <uid> 分别为 8 位（6 字节）和 16 位（7 字节）。AT+QCMGS
使用 8 位 <uid>。
⚫ 对于 GSM 7 位默认字母表数据编码方案，长短信每段的最大长度为 (140 个八位组 - 6) × 8/7=153
个字符。
⚫ 对于 16 位 UCS2 数据编码方案，每段的最大长度为 (140-6)/2=67 个字符。
⚫ 对于 8 位数据编码方案，每段的最大长度为 140-6=134 个字符。
2. <mr>  Message-Reference 字段给出 MS 提交给 SC 的 SMS-SUBMIT 或 SMS-COMMAND 的
  参考号的整数表示，用于确认收到的 SMS-DELIVER 是否与来自 SC 的重复。
<uid>  UDH 的字段。它是长短信的消息标识，不同于 <mr>。长短信中的每个段应具有相同的 <uid>，
  但 <mr> 必须对长短信的每个段递增。
3. AT+QCMGS 不支持在 PDU 模式（AT+CMGF=0）下发送消息。

示例
AT+CMGF=1                                 //将短信消息格式设置为文本模式。
OK
AT+CSCS="GSM"                            //设置 TE 使用的字符集为 GSM。
OK
AT+QCMGS="15056913384",120,1,2 <CR>     //输入 <uid> 为 120，并发送长短信的第一段。
>ABCD<Ctrl-Z>
+QCMGS: 190

OK
AT+QCMGS="15056913384",120,2,2 <CR>    //发送长短信的第二段。
>EFGH<Ctrl-Z>
+QCMGS: 191

OK

## 9.18. AT+QCMGR 读取长短信（合并短信） (Read Concatenated Messages)

本命令的功能与 AT+CMGR 类似，不同之处在于要读取的消息是长短信的一个段，且结果中将显示
参数 <uid>、<msg_seg> 和 <msg_total>。根据这三个参数，多个段应拼接成一条完整的长短信。
与 AT+QCMGS 类似，AT+QCMGR 仅在文本模式（AT+CMGF=1）下使用。

测试命令
AT+QCMGR=?
响应
OK
写入命令
AT+QCMGR=<index>
响应
在文本模式（AT+CMGF=1）且命令执行成功时：
对于 SMS-DELIVER：
+QCMGR:
<stat>,<oa>,[<alpha>],<scts>[,<tooa>,<fo>,<pid>,<dcs>,<sca>,<tosca>,<length>][,<uid>,<msg_seg>,<msg_total>]
<CR><LF><data>

OK
对于 SMS-SUBMIT：
+QCMGR:
<stat>,<da>,[<alpha>][,<toda>,<fo>,<pid>,<dcs>,[<vp>],<sca>,<tosca>,<length>][,<uid>,<msg_seg>,<msg_total>]
<CR><LF><data>

OK
对于 SMS-STATUS-REPORT：
+QCMGR:
<stat>,<fo>,<mr>,[<ra>],[<tora>],<scts>,<dt>,<st>

OK
对于 SMS-COMMAND：
+QCMGR:
<stat>,<fo>,<ct>[,<pid>,[<mn>],[<da>],[<toda>],<length><CR><LF><cdata>]

OK

否则，如果出现与 ME 功能相关的错误：
+CMS ERROR: <err>
最大响应时间 取决于消息内容的长度。
特性/
注意

参数
<uid>           整型。用户数据头（UDH）中的消息标识。范围：0–65535（参见注意）。
 同一条长短信的所有段具有相同的 <uid>。不同的长短信应具有不同的 <uid>。
<msg_seg>      整型。长短信的序列号。范围：1–7。
<msg_total>      整型。一条长短信的段总数。范围：2–7。
    其他参数请参见 AT+CMGR
<err>           整型。有关错误码的详细信息，请参见第 15.5 章。

注意
1. AT+QCMGR 中的 <uid> 不同于 AT+QCMGS 中的 <uid>。UE 可能接收到带有 8 位或 16 位 <uid>
的长短信。因此其最大值为 8 位时的 255 和 16 位时的 65535。
2. 如果要读取的消息不是长短信，则结果中不会显示 <uid>、<msg_seg> 和 <msg_total>。

示例
+CMTI: "SM",3           //长短信的第一条消息到达。

+CMTI: "SM",4           //长短信的第二条消息到达。
AT+QCMGR=3          //读取长短信的第一个段。
+QCMGR: "REC UNREAD","+8615056913384",,"13/07/30,14:44:37+32",120,1,2
ABCD

OK
AT+QCMGR=4          //读取长短信的第二个段。
+QCMGR: "REC UNREAD","+8615056913384",,"13/07/30,14:44:37+32",120,2,2
EFGH

OK

