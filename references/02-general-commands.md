# 2 通用指令 (General Commands)

2 通用指令

2.1. ATI  显示 MT 标识信息

该执行命令输出 MT 信息文本。
参数
示例
ATI
Quectel
EC25
Revision: EC25EFAR02A09M4G

OK

ATI  显示产品标识信息
执行命令
ATI
响应
Quectel
<objectID>
Revision: <revision>

OK
最大响应时间 300 ms
特性 /
参考
V.25ter

<objectID>  字符串类型。设备类型的标识符。
<revision>  字符串类型。产品软件版本的标识文本。

2.2. AT+GMI  请求制造商标识

该命令返回制造商标识文本。它与 AT+CGMI 相同。

2.3. AT+GMM  请求型号标识

该命令返回 MT 型号标识文本。它与第 2.6 章中的 AT+CGMM 相同。
参数

AT+GMI  请求制造商标识
测试命令
AT+GMI=?
响应
OK
执行命令
AT+GMI
响应
Quectel

OK
最大响应时间 300 ms
特性 /
参考
V.25ter

AT+GMM  请求 TA 型号标识
测试命令
AT+GMM=?
响应
OK
执行命令
AT+GMM
响应
<objectID>

OK
最大响应时间 300 ms
特性 /
参考
V.25ter

<objectID>  字符串类型。设备类型的标识符。

2.4. AT+GMR  请求 TA 固件版本标识

该命令输出产品固件版本标识文本。它与 AT+CGMR 相同。
参数
示例
AT+GMR
EC25EFAR02A09M4G

OK

2.5. AT+CGMI  请求制造商标识

该命令返回制造商标识文本。它与 AT+GMI 相同。
AT+GMR  请求 TA 固件版本标识
测试命令
AT+GMR=?
响应
OK
执行命令
AT+GMR
响应
<revision>

OK
最大响应时间 300 ms
特性 /
参考
V.25ter

<revision>  字符串类型。产品软件版本的标识文本。
AT+CGMI  请求制造商标识
测试命令
AT+CGMI=?
响应
OK
执行命令
AT+CGMI
响应
Quectel

OK

2.6. AT+CGMM  请求 MT 型号标识

该命令返回产品的型号信息。它与上述 AT+GMM 相同。
参数

2.7. AT+CGMR  请求 MT 固件版本标识

该执行命令输出 MT 固件版本的标识文本。它与上述 AT+GMR 相同。
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

AT+CGMM  请求型号标识
测试命令
AT+CGMM=?
响应
OK
执行命令
AT+CGMM
响应
<objectID>

OK
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

<objectID>  字符串类型。设备类型的标识符。
AT+CGMR  请求 MT 固件版本标识
测试命令
AT+CGMR=?
响应
OK
执行命令
AT+CGMR
响应
<revision>

参数

2.8. AT+GSN  请求国际移动设备识别码（IMEI）和 SN

该命令请求国际移动设备识别码（IMEI）号码，该号码允许用户识别单个 ME 设备，以及 ME 的序列号（SN）。它与第 2.9 章中的 AT+CGSN 命令相同。

OK
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

<revision>  字符串类型。MT 固件版本的标识文本。
AT+GSN  请求国际移动设备识别码（IMEI）和 SN
测试命令
AT+GSN=?
响应
+GSN: (list of supported <snt>s)

OK
写入命令
AT+GSN=<snt>
响应
如果 <snt>=0，查询 ME 的 SN：
+GSN: <SN>

OK
如果 <snt>=1，查询 ME 的 IMEI：
+GSN: <IMEI>

OK
执行命令
AT+GSN
响应
<IMEI>

OK
或
ERROR

参数

2.9. AT+CGSN  请求国际移动设备识别码（IMEI）

该执行命令请求国际移动设备识别码（IMEI）号码，该号码允许用户识别单个 ME 设备，以及 ME 的序列号（SN）。它与上述 AT+GSN 相同。

如果存在与 ME 功能相关的任何错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

<snt>  整型。控制查询 ME 的 SN 或 IMEI。
   0  查询 ME 的 SN
   1  查询 ME 的 IMEI
<SN>  字符串类型。ME 的 SN。
<IMEI>  字符串类型。ME 的 IMEI。
<err>  错误代码。更多详细信息，请参阅第 15.5 章。
AT+CGSN  请求国际移动设备识别码（IMEI）
测试命令
AT+CGSN=?
响应
+CGSN: (list of supported <snt>s)

OK
写入命令
AT+CGSN=<snt>
响应
如果 <snt>=0，查询 ME 的 SN：
+CGSN: <SN>

OK
如果 <snt>=1，查询 ME 的 IMEI：
+CGSN: <IMEI>

OK
执行命令
AT+CGSN
响应
<IMEI>

参数

2.10. AT&F  将 AT 指令设置重置为出厂默认值

该命令将 AT 指令设置重置为制造商指定的默认值。（参见表 17）。
参数

OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CMS ERROR: <err>
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

<snt>  整型。控制查询 ME 的 SN 或 IMEI。
   0  查询 ME 的 SN
   1  查询 ME 的 IMEI
<SN>  字符串类型。ME 的 SN。
<IMEI>  字符串类型。ME 的 IMEI。
<err>  错误代码。更多详细信息，请参阅第 15.5 章。
AT&F  将所有当前参数设置为制造商默认值
执行命令
AT&F[<value>]
响应
OK
最大响应时间 300 ms
特性 /
参考
V.25ter

<value>  整型。
   0  将所有 AT 指令设置重置为出厂设置

2.11. AT&V  显示当前配置

该命令显示若干 AT 指令参数的当前设置（参见表 2），包括不可读取的单字母 AT 指令参数。

表 4：AT&V 响应

AT&V  显示当前配置
执行命令
AT&V
响应
OK
最大响应时间 300 ms
特性 /
参考
V.25ter

AT&V
&C: 1
&D: 2
&F: 0
&W: 0
E: 1
Q: 0
V: 1
X: 4
Z: 0
S0: 0
S3: 13
S4: 10
S5: 8
S6: 2
S7: 0
S8: 2
S10: 15
S12: 50

OK

2.12. AT&W  将当前设置保存到用户自定义配置文件

该命令将当前 AT 指令设置保存到非易失性存储器中的用户自定义配置文件。（参见表 18）。
参数

2.13. ATZ  将所有当前参数设置为用户自定义配置文件中的值

该命令首先将 AT 指令设置重置为制造商默认值。之后，如果之前已通过 AT&W 保存，则从非易失性存储器中的用户自定义配置文件恢复 AT 指令设置（参见表 20）。

同一命令行上的任何其他 AT 指令可能会被忽略。
参数
AT&W  将当前设置保存到用户自定义配置文件
执行命令
AT&W[<n>]
响应
OK
最大响应时间 300 ms
特性 /
参考
V.25ter

<n>  整型。
   0  用于保存当前 AT 指令设置的配置文件编号。
ATZ  将所有当前参数设置为用户自定义配置文件中的值
执行命令
ATZ[<value>]
响应
OK
最大响应时间 300 ms
特性 /
参考
V.25ter

<value>  整型。

2.14. ATQ  设置结果码显示模式

该命令控制结果码是否传输到 TE。作为响应传输的其他信息文本不受影响。
参数

2.15. ATV  MT 响应格式

该命令决定与 AT 指令结果码和信息响应一起传输的报头（header）和报尾（trailer）的内容。

结果码的数字等效值和简要描述列于下表 4 中。
   0  重置为配置文件 0。
ATQ  设置结果码显示模式
执行命令
ATQ<n>
响应
如果 <n>=0：
OK

如果 <n>=1：
（无）
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。
参考
V.25ter

<n>  整型。
   0  TA 传输结果码
         1  结果码被抑制且不传输
ATV  MT 响应格式
执行命令
ATV<value>
响应
当 <value>=0 时：
0

参数
示例
ATV1           //设置 <value>=1
OK
AT+CSQ
+CSQ: 30,99

OK
            //当 <value>=1 时，结果码为 OK。
ATV0           //设置 <value>=0
0
AT+CSQ
+CSQ: 30,99
0            //当 <value>=0 时，结果码为 0。

表 5：ATV0 和 ATV1 结果码的数字等效值与简要描述

当 <value>=1 时：
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。
参考
V.25ter

<value>  整型。
   0  信息响应：<text><CR><LF>
      短结果码格式：<numeric code><CR>
   1  信息响应：<CR><LF><text><CR><LF>
      长结果码格式：<CR><LF><verbose code><CR><LF>
ATV1 ATV0 描述
OK 0 确认命令执行
CONNECT 1 已建立连接；DCE 正在从命令模式切换到数据模式
RING 2 DCE 检测到来自网络的来电信号

2.16. ATE  设置命令回显模式

该命令控制 TA 在 AT 指令模式下是否回显从 TE 接收的字符。
参数

NO CARRIER 3 连接已终止或建立连接的尝试失败
ERROR 4
命令未被识别、命令行超过最大长度、参数值无效，或处理命令行时出现其他问题
NO DIALTONE 6 未检测到拨号音
BUSY 7 检测到占线（忙）信号
NO ANSWER 8
使用了"@"（等待静音应答）拨号修饰符，但在连接定时器（S7）到期前，未检测到远端振铃后接五秒静音
ATE  设置命令回显模式
执行命令
ATE<value>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。
参考
V.25ter

<value>  整型。
   0  回显模式关闭
   1  回显模式开启

2.17. A/  重复上一条命令行

该命令重复上一条 AT 命令行，"/" 作为行终止字符。
示例
ATI
Quectel
EC25
Revision: EC25EFAR02A09M4G

OK
A/          //重复上一条命令。
Quectel
EC25
Revision: EC25EFAR02A09M4G

OK

2.18. ATS3  设置命令行终止字符

该命令决定 TA 识别为终止传入命令行的字符。它还用于生成结果码和信息文本，与通过 ATS4 设置的字符值一起使用。
A/  重复上一条命令行
执行命令
A/
响应
重复上一条命令
参考
V.25ter

ATS3  设置命令行终止字符
读取命令
ATS3?
响应
<n>

OK
写入命令
ATS3=<n>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。

参数

2.19. ATS4  设置响应格式化字符

该命令决定 TA 为结果码和信息文本生成的字符，与通过 ATS3 设置的行终止字符一起使用。
参数

参考
V.25ter

<n>  整型。命令行终止字符。范围：0–127。默认值：13。
ATS4  设置响应格式化字符
读取命令
ATS4?
响应
<n>

OK
写入命令
ATS4=<n>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。
参考
V.25ter

<n>  整型。响应格式化字符。范围：0–127。默认值：10。

2.20. ATS5  设置命令行编辑字符

该命令决定模组用于从 AT 命令行删除紧邻的前一个字符的字符值（即等同于退格键）。
参数

2.21. ATX  设置 CONNECT 结果码格式并监视呼叫进程

该命令决定 TA 是否向 TE 传输特定结果码。它还控制 TA 在开始拨号时是否检测拨号音，以及是否检测占线音（忙信号）。
ATS5  设置命令行编辑字符
读取命令
ATS5?
响应
<n>

OK
写入命令
ATS5=<n>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。
参考
V.25ter

<n>  整型。响应编辑字符。范围：0–127。默认值：8。
ATX  设置 CONNECT 结果码格式并监视呼叫进程
执行命令
ATX<value>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置可以通过 AT&W 保存。
参考
V.25ter

参数

2.22. AT+CFUN  设置 UE 功能

该命令控制功能级别。它还可以用于重置 UE。

<value>  整型。
   0  仅返回 CONNECT 结果码，拨号音和忙音检测均被禁用。
   1  仅返回 CONNECT<text> 结果码，拨号音和忙音检测均被禁用。
   2  返回 CONNECT<text> 结果码，启用拨号音检测，禁用忙音检测。
   3  返回 CONNECT<text> 结果码，禁用拨号音检测，启用忙音检测。
   4  返回 CONNECT<text> 结果码，拨号音和忙音检测均被启用。
AT+CFUN  设置 UE 功能
测试命令
AT+CFUN=?
响应
+CFUN: (list of supported <fun>s),(list of supported <rst>s)

OK
读取命令
AT+CFUN?
响应
+CFUN: <fun>

OK
写入命令
AT+CFUN=<fun>[,<rst>]
响应
OK

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
最大响应时间 15 s，由网络决定。
特性 该指令立即生效。
该配置不会被保存。
参考
3GPP TS 27.007

参数
示例
AT+CFUN=0          //将 UE 切换到最小功能。
OK
AT+COPS?
+COPS: 0          //未注册任何运营商。

OK
AT+CPIN?
+CME ERROR: 13  //(U)SIM 卡故障。

AT+CFUN=1          //将 UE 切换到全功能。
OK

+CPIN: SIM PIN
AT+CPIN=1234
OK

+CPIN: READY

+QUSIM: 1

+QIND: PB DONE

+QIND: SMS DONE
AT+CPIN?
+CPIN: READY

OK
AT+COPS?
+COPS: 0,0,"CHINA MOBILE",7                   //已注册运营商。

<fun>  整型。
   0  最小功能
1  全功能
4  禁止 ME 发射和接收射频信号
<rst>  整型。
   0  在将 ME 设置为 <fun> 功能级别之前，不重置 ME。
1  重置 ME。重置后设备全功能可用。该值仅适用于 <fun>=1
<err>  错误代码。更多详细信息，请参阅第 15.4 章。

OK

2.23. AT+CMEE  错误消息格式

该命令控制错误结果码的格式：ERROR、错误编号，或如 +CME ERROR: <err> 和 +CMS ERROR: <err> 的详细消息。该命令禁用或启用使用最终结果码 +CME ERROR: <err> 作为错误指示。
参数
<n>  整型。
   0  禁用结果码
   1  启用结果码并使用数字值
2  启用结果码并使用详细值
示例
AT+CMEE=0         //禁用结果码。
OK
AT+CPIN?
ERROR          //仅显示 ERROR

AT+CMEE=1        //启用带有数字值的错误结果码。
OK
AT+CMEE  错误消息格式
测试命令
AT+CMEE=?
响应
+CMEE: (range of supported <n>s)

OK
读取命令
AT+CMEE?
响应
+CMEE: <n>

OK
写入命令
AT+CMEE=<n>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。
参考
3GPP TS 27.007

AT+CPIN?
+CME ERROR: 10
AT+CMEE=2        //启用带有详细（字符串）值的错误结果码。
OK
AT+CPIN?
+CME ERROR: SIM not inserted

2.24. AT+CSCS  选择 TE 字符集

该命令告知 MT 使用的是哪种字符集。之后，TA 便能够在 TE 和 MT 字符集之间正确转换字符串。
参数
示例
AT+CSCS?           //查询当前字符集。
+CSCS: "GSM"                                 //字符集为 GSM。

AT+CSCS  选择 TE 字符集
测试命令
AT+CSCS=?
响应
+CSCS: (list of supported <chset>s)

OK
读取命令
AT+CSCS?
响应
+CSCS: <chset>

OK
写入命令
AT+CSCS=<chset>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被保存。
参考
3GPP TS 27.007

<chset>  字符串类型。
    "GSM"   GSM 默认字母表
             "IRA"   国际参考字母表
             "UCS2"  UCS2 字母表

OK
AT+CSCS="UCS2"        //将字符集设置为 "UCS2"。
OK
AT+CSCS?
+CSCS: "UCS2"                                //配置后字符集为 UCS2。

OK

2.25. AT+QURCCFG  配置 URC 指示选项

该命令配置 URC 的输出端口。
参数
AT+QURCCFG  配置 URC 指示选项
测试命令
AT+QURCCFG=?
响应
+QURCCFG: "urcport",(list of supported
<urc_port_value>s)

OK
写入命令
AT+QURCCFG="urcport"[,<urc_port
_value>]

响应
如果省略可选参数，查询当前配置：
+QURCCFG: "urcport",<urc_port_value>

OK

如果指定了可选参数，则配置 URC 的输出端口：
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
该配置会被自动保存。
<urc_port_value>  字符串类型。设置 URC 输出端口。
       "usbat"           USB AT 端口
          "usbmodem"          USB modem 端口
"uart1"      主 UART
"uart2"      调试 UART

示例
AT+QURCCFG=?
+QURCCFG: "urcport",("usbat","usbmodem","uart1","uart2","all")

OK
AT+QURCCFG="urcport"
+QURCCFG: "urcport","usbat"

OK
AT+QURCCFG="urcport","usbmodem"
OK
AT+QURCCFG="urcport"
+QURCCFG: "urcport","usbmodem"

OK

2.26. AT+QAPRDYIND  配置上报指定的 URC

该命令配置在 AP 侧进程成功启动后，是否启用指定的 URC。

"all"      所有端口
AT+QAPRDYIND  配置上报指定的 URC
读取命令
AT+QAPRDYIND?
响应
+QAPRDYIND: (range of supported <cfg_val>s)

OK
写入命令
AT+QAPRDYIND=<cfg_val>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令在模组重启后生效。
该配置会被自动保存。

参数

1. 如果 URC 已启用，上电后将通过指定端口上报该 URC。该端口可以通过 AT+QURCCFG="urcport" 配置，默认端口为 USB AT。
2. 模组 UART2 的 AT 功能被禁用；如果需要 DDP URC，则需要通过 AT+QDIAGPORT=1 启用 AT 功能。
<cfg_val>  整型。范围：0–15。默认值：0。
     该值与对应的 URC 可参考下表。下表中的 Y 表示该 URC 将被上报，N 表示该 URC 将不会被上报。

<cfg_val> +APIND: UART
DDP READY
+APIND: QUEC
DAEMON READY
+APIND: ATFWD
READY
+APIND: QMI
READY
0 N N N N
1 Y N N N
2 N Y N N
3 Y Y N N
4 N N Y N
5 Y N Y N
6 N Y Y N
7 Y Y Y N
8 N N N Y
9 Y N N Y
10 N Y N Y
11 Y Y N Y
12 N N Y Y
13 Y N Y Y
14 N Y Y Y
15 Y Y Y Y

注释（NOTES）

示例
AT+QAPRDYIND?
+QAPRDYIND=0

OK
AT+QURCCFG="urcport"    //该命令可用于设置 URC 输出的端口。
+QURCCFG: "urcport","usbat"

OK
AT+QAPRDYIND=2
OK        //端口设置成功，模组重启后将上报 URC +APIND: QUEC DAEMON READY。
AT+QAPRDYIND=4
OK        //端口设置成功，模组重启后将上报 URC +APIND: ATFWD READY。

AT+QAPRDYIND=6
OK        //端口设置成功，模组重启后将上报 URC +APIND: QUEC DAEMON READY
         和 +APIND: ATFWD READY。

//如果需要上报 URC +APIND: UART DDP READY，则需要在配置前通过 AT+QDIAGPORT=1 启用 UART2 的 AT 功能。
AT+QDIAGPORT=1

OK
AT+QAPRDYIND=1
OK        //端口设置成功，模组重启后将上报 URC +APIND: UART DDP READY。
AT+QAPRDYIND=3
OK        //端口设置成功，模组重启后将上报 URC +APIND: UART DDP READY 和
        +APIND: QUEC DAEMON READY。
AT+QAPRDYIND=5
OK        //端口设置成功，模组重启后将上报 URC +APIND: UART DDP READY 和
+APIND:        ATFWD READY。
AT+QAPRDYIND=7
OK        //端口设置成功，模组重启后将上报 URC +APIND: UART DDP READY、
+APIND:        QUEC DAEMON READY 和 +APIND: ATFWD READY。

2.27. AT+QDIAGPORT  调试 UART 配置

该命令将调试 UART 配置为 AT 端口。
参数

1. 当调试 UART 配置为 AT 端口时，波特率固定为 115200 bps。
2. 当调试 UART 配置为 AT 端口时，仍然会输出模组启动消息。
3. 由于波特率有限，建议不要在调试 UART 上建立数据连接。
AT+QDIAGPORT  调试 UART 配置
读取命令
AT+QDIAGPORT=?
响应
+QDIAGPORT: (list of supported <num>s)

OK
写入命令
AT+QDIAGPORT=<num>
响应
OK
或
ERROR
最大响应时间 12 s
特性 该指令在模组重启后生效。
该配置会被自动保存。
<num>  整型。
   0  调试 UART 端口
   1  AT 端口
注释（NOTES）
