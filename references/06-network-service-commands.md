# 6 网络服务指令 (Network Service Commands)

6 网络服务指令 (Network Service Commands)

6.1. AT+COPS  运营商选择 (Operator Selection)

本命令返回当前运营商及其状态，并允许设置自动或手动网络选择。

该测试命令返回一组五个参数，每个参数表示网络中出现的运营商。任一格式可能不可用，此时应为空字段。运营商列表应按以下顺序排列：归属网络、(U)SIM 中引用的网络以及其他网络。

该读取命令返回当前模式和当前选择的运营商。如果未选择运营商，则省略 <format>、<oper> 和 <Act>。

该写入命令强制尝试选择并注册 GSM/UMTS 网络运营商。如果所选的运营商不可用，则不应选择其他运营商（<mode>=4 除外）。所选运营商名称的格式将应用于后续的读取命令（AT+COPS?）。
AT+COPS  运营商选择 (Operator Selection)
测试命令
AT+COPS=?
响应
+COPS: (list of supported  <stat>,long alphanume ric <op
er>,short alphanumeric <oper>,numeric <oper>s)[,<Act>])
s][,,(list of  supported <mode>s),(list of supported <forma
t>s)]

OK

如果发生任何与 ME 功能相关的错误：
+CME ERROR: <err>
读取命令
AT+COPS?
响应
+COPS: <mode>[,<format>[,<oper>][,<Act>]]

OK

如果发生任何与 ME 功能相关的错误：
+CME ERROR: <err>

参数
写入命令
AT+COPS=<mode>[,<format>[,<oper
>[,<Act>]]]

响应
OK

如果发生任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 180 s，由网络决定。
特性 该命令立即生效。
参考
3GPP TS 27.007

<stat>  整型。
   0  未知
   1  运营商可用
   2  当前运营商
   3  运营商被禁止
<oper>  运营商，格式由 <format> 决定。<mode> 决定是否显示 <oper>。
<mode>  整型。
   0  自动模式。<oper> 字段省略
   1  手动选择运营商。<oper> 字段必须存在，<Act> 可选
   2  手动从网络注销
 3 仅设置 <format>（用于 AT+COPS? 读取命令），并且不尝试
注册/注销（忽略 <oper> 和 <Act> 字段）。该值
在读取命令的响应中无效。
4 手动/自动选择。<oper> 字段必须存在。如果手动选择
失败，则进入自动模式（<mode>=0）
<format>  整型。指示 <oper> 的格式。
   0  长格式字母数字 <oper>，最长可达 16 个字符
   1  短格式字母数字 <oper>
   2  数字 <oper>。GSM 位置区识别号
<Act>       整型。选择的接入技术。值 3、4、5 和 6 仅出现在 MS 处于数据服务状态时的读取命令
响应中，不用于 AT+COPS 写入命令。
             0       GSM
             2       UTRAN
   3       GSM W/EGPRS
             4       UTRAN W/HSDPA
             5       UTRAN W/HSUPA
             6       UTRAN W/HSDPA 和 HSUPA
7       E-UTRAN
             100  CDMA

示例
AT+COPS=?        //列出所有当前网络运营商。
+COPS: (1,"CHN -UNICOM","UNICOM","46001",2),(1,"CHN-UNICOM","UNICOM","46001",0),(2,"CH
N-UNICOM","UNICOM","46001",7),(1,"46011","46011","46011",7),(3,"CHINA MOBILE","CMCC","46
000",0),,(0,1,2,3,4),(0,1,2)

OK
AT+COPS?        //查询当前选择的网络运营商。
+COPS: 0,0,"CHN-UNICOM",7

OK

6.2. AT+CREG  网络注册状态 (Network Registration Status)

该读取命令返回结果码呈现状态以及一个整型 <stat>，该整型指示网络当前是否已指示 ME 的注册。仅当 <n>=2 且 ME 已注册到网络时，才返回位置信息元素 <LAC> 和 <ci>。

该写入命令控制当 <n>=1 且 ME 网络注册状态发生变化时主动上报结果码 +CREG: <stat> 的呈现。
<err>       错误码。更多详情，请参阅第 15.4 章。
AT+CREG  网络注册状态 (Network Registration Status)
测试命令
AT+CREG=?
响应
+CREG: (list of supported <n>s)

OK
读取命令
AT+CREG?
响应
+CREG: <n>,<stat>[,<LAC>,<ci>[,<Act>]]

OK

如果发生任何与 ME 功能相关的错误：
+CME ERROR: <err>
写入命令
AT+CREG[=<n>]
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
该配置不会被保存。

参数
示例
AT+CREG=1
OK

+CREG: 1        //URC 上报 ME 已注册到网络。
AT+CREG=2        //激活扩展 URC 模式。
OK

+CREG: 1,"D509","80D413D",7        //URC 上报运营商已找到位置区码和小区 ID。

参考
3GPP TS 27.007

<n>       整型。是否启用相关注册网络。
    0  禁用网络注册 URC
  1  启用网络注册 URC +CREG: <stat>
 2  启用带位置信息的网络注册 URC：
 +CREG: <stat>[,<LAC>,<ci>[,<Act>]]
<stat>    整型。注册网络状态。
    0  未注册。ME 当前未在搜索新的运营商进行注册
    1  已注册，归属网络
    2  未注册，但 ME 当前正在搜索新的运营商进行注册
    3  注册被拒绝
    4  未知
  5  已注册，漫游
<LAC>       字符串类型。十六进制格式的两字节位置区码。
<ci>        字符串类型。十六进制格式的 16 位（GSM）或 28 位（UMTS/LTE）小区 ID。
<Act>        整型。选择的接入技术。
 0       GSM
    2       UTRAN
 3       GSM W/EGPRS
    4       UTRAN W/HSDPA
    5       UTRAN W/HSUPA
    6       UTRAN W/HSDPA 和 HSUPA
    7       E-UTRAN
<err>           错误码。更多详情，请参阅第 15.4 章。

6.3. AT+CSQ  信号质量报告 (Signal Quality Report)

本命令指示接收信号强度 <rssi> 和信道误码率 <ber>。

该测试命令返回 MT 支持的值。

该执行命令返回来自 MT 的接收信号强度指示 <rssi> 和信道误码率 <ber>。
参数
AT+CSQ  信号质量报告 (Signal Quality Report)
测试命令
AT+CSQ=?
响应
+CSQ: (list of supported <rssi>s),(list of supported <ber>s)

OK
执行命令
AT+CSQ
响应
+CSQ: <rssi>,<ber>

OK

如果发生与 MT 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

<rssi>   整型。接收信号强度指示。
    0   -113 dBm 或以下
    1   -111 dBm
    2–30  -109 dBm 至 -53 dBm
    31   -51 dBm 或以上
    99          未知或不可检测
                100         -116 dBm 或以下
                101         -115 dBm
                102...190    -114 dBm 至 -26 dBm
                191         -25 dBm 或以上
                199         未知或不可检测
                100–199  扩展用于 TD-SCDMA 中指示接收信号码功率 (RSCP)

示例
AT+CSQ=?
+CSQ: (0-31,99),(0-7,99)

OK
AT+CSQ
+CSQ: 28,99     //当前信号强度指示为 28 dBm，信道误码率为 99 dBm。

OK

在使用 AT+CCWA 和 AT+CCFC 等网络相关命令后，建议等待 3 秒再输入 AT+CSQ，以确保前一条命令所需的任何网络接入已完成。

6.4. AT+CPOL  首选运营商列表 (Preferred Operator List)

本命令编辑并查询首选运营商列表。
<ber>   整型。信道误码率（百分比）。
    0–7      与 3GPP TS 45.008 第 8.2.4 小节表格中的 RxQual 值一致
    99   未知或不可检测
AT+CPOL  首选运营商列表 (Preferred Operator List)
测试命令
AT+CPOL=?
响应
+CPOL: (list o f supported  <index>s),(list o f supported
<format>s)

OK
读取命令
AT+CPOL?
响应
查询首选运营商列表：
+CPOL: <index>,<format>,<oper >[,<GSM>,<GSM_comp
act>,<UTRAN>,<E-UTRAN>]
[+CPOL: <index>,<format>,<ope r>[,<GSM>,<GSM_comp
act>,<UTRAN>,<E-UTRAN>
…]

OK
写入命令响应
注意

参数

对于包含带接入技术的 PLMN 选择器的 (U)SIM 卡或 UICC，需要接入技术选择参数 <GSM>、<GSM_compact>、<UTRAN> 和 <E-UTRAN>。

AT+CPOL=<index>[,<format>[,<oper
>[<GSM>,<GSM_compact>,<UTRAN>
,<E-UTRAN>]]]
编辑首选运营商列表：
OK
或
ERROR

如果给定了 <index> 但省略了 <oper>，则删除该条目。
最大响应时间 300 ms
特性 该命令立即生效。
参考
3GPP TS 27.007

<index>             整型。(U)SIM 首选运营商列表中的运营商序号。
<format>         整型。<oper> 的格式。
     0 长格式字母数字 <oper>
           1 短格式字母数字 <oper>
           2 数字 <oper>
<oper>           字符串类型。<format> 指示格式为字母数字或数字（参见
AT+COPS）。
<GSM>             整型。GSM 接入技术。
0 未选择接入技术
1 已选择接入技术
<GSM_compact>   整型。GSM 紧凑型接入技术。
0 未选择接入技术
1 已选择接入技术
<UTRAN>           整型。UTRAN 接入技术。
0 未选择接入技术
1 已选择接入技术
<E-UTRAN>         整型。E-UTRAN 接入技术。
0 未选择接入技术
1 已选择接入技术
注意

6.5. AT+COPN  读取运营商名称 (Read Operator Names)

本命令返回 MT 中支持的运营商名称列表。返回 MT 内存中具有字母数字等效名称 <alphan> 的每个运营商代码 <numericn>。
参数

6.6. AT+CTZU  自动时区更新 (Automatic Time Zone Update)

本命令启用/禁用通过 NITZ 自动进行时区更新。
AT+COPN  读取运营商名称 (Read Operator Names)
测试命令
AT+COPN=?
响应
OK
执行命令
AT+COPN
响应
+COPN: <numeric1>,<alpha1>
[+COPN: <numeric2>,<alpha2>
…]

OK

如果发生与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 取决于运营商名称的数量。
特性 /
参考
3GPP TS 27.007
<numericn>  字符串类型。数字格式的运营商（参见 AT+COPS）。
<alphan>  字符串类型。长字母数字格式的运营商（参见 AT+COPS）。
<err>           错误码。更多详情，请参阅第 15.4 章。
AT+CTZU  自动时区更新 (Automatic Time Zone Update)
测试命令
AT+CTZU=?
响应
+CTZU: (list of supported <enable>s)

OK
写入命令
AT+CTZU=<enable>
响应
OK

参数
<enable>  整型。自动时区更新的模式。
                0 禁用通过 NITZ 自动进行时区更新。
1 启用通过 NITZ 自动进行时区更新
3 启用通过 NITZ 自动进行时区更新，并将 LOCAL 时间更新到 RTC
示例
AT+CTZU?       //读取命令。
+CTZU: 0

OK
AT+CTZU=?     //测试命令。
+CTZU: (0,1,3)

OK
AT+CTZU=1     //启用自动时区更新。
OK
AT+CTZU?
+CTZU: 1

OK

或
ERROR
读取命令
AT+CTZU?
响应
+CTZU: <enable>

OK
最大响应时间 300 ms
特性 该命令立即生效。
该配置将自动保存。
参考
3GPP TS 27.007

6.7. AT+CTZR  时区上报 (Time Zone Reporting)

本命令控制时区变化事件的上报。如果启用了上报，则每当时区发生变化时，MT 都会返回主动上报结果码 +CTZV: <tz> 或 +CTZE: <tz>,<dst>,<time>。
参数
AT+CTZR  时区上报 (Time Zone Reporting)
测试命令
AT+CTZR=?
响应
+CTZR: (range of supported <reporting>s)

OK
写入命令
AT+CTZR=<reporting>
响应
OK
或
ERROR
读取命令
AT+CTZR?
响应
+CTZR: <reporting>

OK
最大响应时间 300 ms
特性 该命令在模组重启后生效。
该配置将自动保存。
参考
3GPP TS 27.007

<reporting>  整型。时区上报的模式。
0 禁用时区变化事件的上报
1 通过 URC +CTZV: <tz> 启用时区变化事件的上报
2 通过 URC +CTZE: <tz>,<dst>,<time> 启用扩展时区上报
<tz> 字符串类型。本地时区（本地时间与 GMT 之间的差值，以刻钟为单位表示）加上夏令时时间的总和。格式为 "± zz"，表示为固定宽度、两位整数的形式，范围为 -48 至 +56。为保持固定宽度，-9 至 +9 范围内的数字用前导零表示，例如 "-09"、"+00" 和 "+09"。
<dst>       整型。指示 <tz> 是否包含夏令时调整。
0 <tz> 不包含夏令时调整
1 <tz> 包含 +1 小时（在 <tz> 中等于 4 刻钟）的夏令时调整
2   <tz> 包含 +2 小时（在 <tz> 中等于 8 刻钟）的夏令时调整

示例
AT+CTZR=2
OK
AT+CTZR?
+CTZR: 2

OK

+CTZE: "+32",0,"2017/11/04,06:51:13"   //URC 上报扩展时区和本地时间。

6.8. AT+QLTS  获取通过网络同步的最新时间 (Obtain the Latest Time Synchronized Through Network)

本命令获取通过网络同步的最新时间。

该执行命令返回通过网络同步的最新时间。
<time> 字符串类型。本地时间。格式为 "YYYY/MM/DD,hh:mm:ss"，以整数表示年 (YYYY)、月 (MM)、日 (DD)、时 (hh)、分 (mm) 和秒 (ss)。当网络发送时区信息时可提供此参数，并且如果网络提供了该参数，它将出现在扩展时区上报的主动上报结果码中。
AT+QLTS  获取通过网络同步的最新时间 (Obtain the Latest Time Synchronized Through Network)
测试命令
AT+QLTS=?
响应
+QLTS: (range of supported <mode>s)

OK
执行命令
AT+QLTS
响应
+QLTS: <time>,<dst>

OK
写入命令
AT+QLTS=<mode>
响应
+QLTS: <time>,<dst>

OK
或
ERROR

如果发生与 ME 功能相关的错误：
+CME ERROR: <err>

参数

如果时间尚未通过网络同步，则命令将返回空时间字符串，即 +QLTS: ""。
示例
AT+QLTS=?    //查询支持的网络时间模式。
+QLTS: (0-2)

OK
AT+QLTS    //查询通过网络同步的最新时间。
+QLTS: "2017/10/13,03:40:48+32,0"

OK
AT+QLTS=0            //查询通过网络同步的最新时间。其功能与执行命令 AT+QLTS 相同。
+QLTS: "2017/10/13,03:40:48+32,0"

OK
AT+QLTS=1    //查询由通过网络同步的最新时间计算出的当前 GMT 时间。
+QLTS: "2017/10/13,03:41:22+32,0"

OK
最大响应时间 300 ms
特性 该命令立即生效。
<mode>  整型。网络时间获取模式。
   0 查询通过网络同步的最新时间
   1 查询由通过网络同步的最新时间计算出的当前 GMT 时间
   2 查询由通过网络同步的最新时间计算出的当前 LOCAL 时间
<time> 字符串类型值。格式为 "YYYY/MM/dd,hh:mm:ss±zz"，其中各字符指示年（最后两位数字）、月、日、时、分、秒和时区（表示本地时间与 GMT 之间的差值，以刻钟为单位；范围：-48 至 +48）。例如：2004 年 5 月 6 日 22:10:00 GMT+2 小时等于 "04/05/06,22:10:00+08"。
<dst>  整型。夏令时。范围：0–2。
<err>       错误码。更多详情，请参阅第 15.4 章。
注意

AT+QLTS=2    //查询由通过网络同步的最新时间计算出的当前 LOCAL 时间。
+QLTS: "2017/01/13,11:41:23+32,0"

OK

6.9. AT+QNWINFO  查询网络信息 (Query Network Information)

本命令查询网络信息，例如所选择的接入技术、运营商和频段。
参数
AT+QNWINFO  查询网络信息 (Query Network Information)
测试命令
AT+QNWINFO=?
响应
OK
执行命令
AT+QNWINFO
响应
+QNWINFO: <Act>,<oper>,<band>,<channel>

OK
最大响应时间 300 ms
特性 /
<Act>   字符串类型。选择的接入技术。
                "NONE"
                "CDMA1X"
                "CDMA1X AND HDR"
                "CDMA1X AND EHRPD"
                "HDR"
                "HDR-EHRPD"
                "GSM"
                "GPRS"
                "EDGE"
                "WCDMA"
                "HSDPA"
                "HSUPA"
                "HSPA+"
                "TDSCDMA"
                "TDD LTE"
                "FDD LTE"
<oper>   字符串类型。数字格式的运营商。

示例
AT+QNWINFO=?
OK
AT+QNWINFO
+QNWINFO: "FDD LTE",46011,"LTE BAND 3",1650

OK

<band>      字符串类型。选择的频段。
                "CDMA BC0" – "CDMA BC19"
                "GSM 450"
                "GSM 480"
                "GSM 750"
                "GSM 850"
                "GSM 900"
                "GSM 1800"
                "GSM 1900"
                "WCDMA 2100"
                "WCDMA 1900"
                "WCDMA 1800"
                "WCDMA 1700 US"
                "WCDMA 850"
                "WCDMA 800"
                "WCDMA 2600"
                "WCDMA 900"
                "WCDMA 1700 JAPAN"
                "WCDMA 1500"
                "WCDMA 850 JAPAN"
                "LTE BAND 1" 至 "LTE BAND 43"
                "LTE BAND 66"
                "LTE BAND 71"
                "TDSCDMA BAND A"
                "TDSCDMA BAND B"
                "TDSCDMA BAND C"
                "TDSCDMA BAND D"
                "TDSCDMA BAND E"
                "TDSCDMA BAND F"
<channel>      整型。信道 ID。

6.10. AT+QSPN  显示注册网络名称 (Display the Name of Registered Network)

参数

示例
AT+QSPN           //查询 RPLMN 的 EONS 信息。
+QSPN: "CHN-UNICOM","UNICOM","",0,"46001"

OK

AT+QSPN  显示注册网络名称 (Display the Name of Registered Network)
测试命令
AT+QSPN=?
响应
OK
执行命令
AT+QSPN
响应
+QSPN: <FNN>,<SNN>,<SPN>,<alphabet>,<RPLMN>

OK
最大响应时间 300 ms
特性 /
<FNN>                字符串类型。完整网络名称。
<SNN>               字符串类型。短网络名称。
<SPN>                 字符串类型。服务提供商名称。
<alphabet>             整型。完整网络名称和短网络名称的字母表。
                     0 GSM 7 位默认字母表
                      1 UCS2
<RPLMN>           字符串类型。注册的 PLMN。
1. 如果 <alphabet> 为 0，则 <FNN> 和 <SNN> 将以 GSM 7 位默认字母表字符串显示。
2. 如果 <alphabet> 为 1，则 <FNN> 和 <SNN> 将以 UCS2 十六进制字符串显示。
注意

6.11. AT+QNETINFO  查询 RAT 网络信息 (Query Network Information of RATs)

本命令查询指定 RAT 的指定参数。
参数
AT+QNETINFO  查询 RAT 网络信息 (Query Network Information of RATs)
测试命令
AT+QNETINFO=?
响应
+QNETINFO: <rat>,<bit_msk>

OK
写入命令
AT+QNETINFO=<rat>,<bit_msk>

响应
+QNETINFO: <mode>,<rslt_cnt>
<func>,<value>
……
<func>,<value>

OK
或
ERROR
最大响应时间 300 ms
特性 该命令在模组重启后生效。
<rat> 整型。选择的接入技术。
 0    GSM
 1    WCDMA
 2    LTE
 3    TD-SCDMA

4    UMTS
5    CDMA
6    HDR
<bit_msk> 数字格式（HEX）。功能掩码。范围：00xFFFFFFFF，每个位表示一项功能。

rat 位 功能 <func>,<value>
GSM
0 drx "drx",value
... -
31 -
WCDMA 0 drx "drx",value

... -
31 -
LTE
0 rsssnr "rsssnr",value
1 timing advance "timingadvance",value
2 drx "drx",value1,value2,value3
… -
31 -
TD-SCDMA*
0 -
… -
31 -
UMTS*
0 -
… -
31 -
CDMA*
0 -
… - /
31 - /
HDR*
0 - /
… - /
31 - /
在上表中，"-" 表示该位尚未定义。
查询 LTE 的 drx 时，会返回三个参数 value1、value2 和 value3，分别指示空闲 DRX 周期、短 CDRX 周期和长 CDRX 周期。
<mode> 字符串类型。选择的接入技术。

"GSM"
"WCDMA"
"LTE"
"TD-SCDMA"
"UMTS"
"CDMA"
"HDR"

1. 每种网络模式下 <bit_msk> 的每个位代表一项功能。例如，LTE 中 <bit_msk> 的第 0 位指示查询 rsssnr，第一位指示查询 timing advance。
2. 返回响应时，如果 AT 命令的 <bit_msk> 中所设置的位集中存在未定义的位，则 <rslt_cnt> 将小于 AT 命令 <bit_msk> 中所设置的位数。
示例
AT+QNETINFO=2,1                  //查询 LTE 网络的 rsssnr。
+QNETINFO: "LTE",1
"rsssnr",10

OK
AT+QNETINFO=2,1
+QNETINFO: "LTE",1
"rsssnr",-

OK

AT+QNETINFO=2,7     //查询 LTE 网络的 rsssnr、timingadvance、drx。
+QNETINFO: "LTE",1
"rsssnr",10
"timingadvance",39
"drx",320,0,0

OK

AT+QNETINFO=0,1                  //查询 GSM 网络的 drx。
+QNETINFO: "GSM", 1
"drx",471

OK

AT+QNETINFO=1,1                  //查询 WCDMA 网络的 drx。
+QNETINFO: "WCDMA", 1
"drx",1280

<rslt_cnt> 数字格式（DEC）。响应功能的数量。
<func> 字符串类型。功能。
<value> 格式与 <func> 相关。不同 <func> 的值格式不同。如果返回值为空，则返回 "-"。
注意

OK

6.12. AT+QNWLOCK="common/lte"  网络锁定配置 (Network Locking Configuration)

本命令将模组锁定到指定的 FREQ 或小区。
参数

AT+QNWLOCK="common/lte"  网络锁定配置 (Network Locking Configuration)
测试命令
AT+QNWLOCK=?
响应
…
+QNWLOCK: "common/lte"[,<action>[,<EARFCN>,<PCI>[,<s
tatus>]]]

OK
写入命令
AT+QNWLOCK="common/lte"[,<
action>[,<EARFCN>,<PCI>]]
响应
如果省略可选参数，则查询当前设置：
+QNWLOCK: " common/lte",<action>,<EARFCN>,<PCI>,<sta
tus>

OK

如果指定了可选参数，则将模组锁定到
指定的 FREQ 或小区：
OK
或
ERROR
最大响应时间 300 ms
特性 该命令立即生效。
这些配置不会被保存。
<action>

整型。
0   禁用锁定小区
1 通过指定的 EARFCN 启用锁定 LTE 小区
2 通过指定的 EARFCN 和 PCI 启用锁定 LTE 小区
<EARFCN> 整型。要锁定小区的指定 EARFCN。默认值：0。
<PCI> 整型。要锁定小区的指定 PCI。默认值：0。
<status> 整型。完成/未完成锁定或解锁小区。默认值：0。
0 完成锁定或解锁小区
1 未完成锁定或解锁小区

1. 设置 <action> 为 0 并重启模组后，模组即可解锁小区。
2. 使用本命令锁定 LTE 小区前，需要先使用 AT+QCFG="NWSCANMODE",3 将模组固定为仅 LTE 模式。更多详情，请参阅文档 [12]。
示例
AT+QCFG="NWSCANMODE",3
OK

AT+QNWLOCK="common/lte"           //查询锁定小区状态。
+QNWLOCK: "common/lte",0,0,0,0

OK

AT+QNWLOCK="common/lte",1,38400,0  //在 EARFCN 38400 上锁定小区。
OK
AT+QNWLOCK="common/lte"
+QNWLOCK: "common/lte",1,38400,0,0

OK

AT+QNWLOCK="common/lte",2,38400,87  //在 EARFCN 38400 的 PCI 87 上锁定小区。
OK
AT+QNWLOCK="common/lte"
+QNWLOCK: "common/lte",2,38400,87,0

OK
AT+QENG="SERVINGCELL"
+QENG: "servingcell","NOCONN","LTE","TDD",460,00,82E8C80,87,38400,39,5,5,550A,-93,-13,-59,-
4,46

OK
AT+QNWLOCK="common/lte",0      //禁用锁定小区功能。
OK
AT+QNWLOCK="common/lte"
+QNWLOCK: "common/lte",0,38400,87,1

OK

注意

6.13. AT+QOPSCFG="scancontrol"  配置 2G/3G/4G 中待扫描的频段 (Configure Bands to be Scanned in 2G/3G/4G)
参数
AT+QOPSCFG="scancontrol"  配置 2G/3G/4G 中待扫描的频段 (Configure Bands to be Scanned in 2G/3G/4G)
测试命令
AT+QOPSCFG=?
响应
+QOPSCFG: "scancon trol",(range of supported  <RAT>
s),(range of su pported <GW_band>s),(range o f supported
 <LTE_band>s),(range of supported  <TDS_band>s)

OK
写入命令
AT+QOPSCFG="scancontrol"[,<RAT>
[,<GW_band>,<LTE_band>,<TDS_ban
d>]]
响应
如果省略 <RAT>、<GW_band>、<LTE_band> 和 <TDS_band>，则查询当前配置：
+QOPSCFG: "scancontrol",<rat>,<GW_band>,<LTE_ban
d>,<TDS_band>

OK

如果省略 <GW_band>、<LTE_band> 和 <TDS_band>，则配置 2G/3G/4G 中待扫描的全部频段：
OK
或
ERROR

如果指定了 <RAT>、<GW_band>、<LTE_band> 和 <TDS_band>，则配置 2G/3G/4G 中待扫描的频段：
OK
或
ERROR
最大响应时间 300 ms
特性 该命令立即生效；
这些配置不会被保存。
<RAT> 十进制数字格式。网络模式。
0 2G
1 3G
2 4G
3 2G、3G 和 4G
<GW_band> 指定 GSM 和 WCDMA 频率频段的十六进制值。如果设置为 0，则表示不更改 GSM 和 WCDMA 频率频段。范围：0-FFFF。
（例如：00000013 = 00000001 (EGSM900) + 00000002 (DCS1800) + 00000010 (WCDMA2100)）。
00000000  不更改
00000001  EGSM900
00000002  DCS1800
00000004  GSM850
00000008  PCS1900
00000010  WCDMA2100
00000020  WCDMA1900
00000040  WCDMA850
00000080  WCDMA900
00000100  WCDMA800
00000200  WCDMA1700
0000FFFF   任意频率频段
<LTE_band> 指定 LTE 频率频段的十六进制值。如果设置为 0 或 0x40000000，则表示不更改 LTE 频率频段。范围：0-7FFFFDF3FFF
（例如：0x15 = 0x1 (LTE B1) + 0x4 (LTE B3) + 0x10 (LTE B5)）。
0x1 (CM_BAND_PREF_LTE_EUTRAN_BAND1)   LTE B1
0x4 (CM_BAND_PREF_LTE_EUTRAN_BAND3)    LTE B3
0x10 (CM_BAND_PREF_LTE_EUTRAN_BAND5)    LTE B5
0x40 (CM_BAND_PREF_LTE_EUTRAN_BAND7)    LTE B7
0x80 (CM_BAND_PREF_LTE_EUTRAN_BAND8)    LTE B8
0x80000 (CM_BAND_PREF_LTE_EUTRAN_BAND20)   LTE B20
0x7FFFFFFFFFFFFFFF (CM_BAND_PREF_ANY)   任意频率频段
<TDS_band> 指定 TD-SCDMA 频率频段的十六进制值。如果设置为 0 或 0x40000000，则表示不更改 TD-SCDMA 频率频段。范围：0-3F
（例如：0x21 = 0x1 (TDS BCA) + 0x20 (TDS BCF)）。
0x1 (CM_BAND_PREF_TDS_BANDA)   TDS BCA
0x2 (CM_BAND_PREF_TDS_BANDB)   TDS BCB
0x4 (CM_BAND_PREF_TDS_BANDC)   TDS BCC
0x8 (CM_BAND_PREF_TDS_BANDD)   TDS BCD
0x10 (CM_BAND_PREF_TDS_BANDE)   TDS BCE
0x20 (CM_BAND_PREF_TDS_BANDF)  TDS BCF
注意

1. <GW_band> 表示 GSM 和 WCDMA 中的所有频段，范围为 0 至 FFFFFFFFBFFFFFFF。将 <GW_band> 设置为 0-FFFF 范围内的值时，它对应 GSM/WCDMA 中 0-FFFFFFFFBFFFFFFF 范围内的频段值。
2. 建议扫描 GSM/WCDMA 中的全频段（即配置扫描 GSM 和 WCDMA 频段时，将 <GW_band> 的值设置为 FFFF），因为 GSM/WCDMA 中的频段数量较少。

6.14. AT+QOPSCFG="displayrssi"  启用/禁用 LTE 中显示 RSSI (Enable/Disable to Display RSSI in LTE)
参数

配置 <enable>=1 后，当通过 AT+QOPS 扫描 LTE 中的频段或 GSM/WCDMA/LTE 中的全部频段时，将返回 LTE 中的 RSSI 值。

6.15. AT+QOPS  频段扫描 (Band Scan)

本命令触发频段扫描。执行命令列出所有相邻小区的可用运营商网络信息。
AT+QOPSCFG="displayrssi"  启用/禁用 LTE 中显示 RSSI (Enable/Disable to Display RSSI in LTE)
写入命令
AT+QOPSCFG="displayrssi",<enabl
e>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该命令立即生效；
该配置不会被保存。
<enable> 十进制数字格式。启用/禁用 LTE 中显示 RSSI。
1 启用
0 禁用
AT+QOPS  频段扫描 (Band Scan)
执行命令
AT+QOPS

响应
对于 2G：
+QOPS: <oper_in_string> ,<oper_in_short_string>,<oper_in_n umbe
r>
<index>,<RAT,<freq>,<lac>,<ci>,<bsic>,<rxlev>,<c1>,<cba>,<is_gprs
_support>
[…]

注意

参数
对于 3G：
+QOPS:
<oper_in_string>,<oper_in_short_string>,<oper_in_number>
<index>,<RAT>,<freq>,<psc>,<lac>,<ci>,<rscp>,<ecno>,<cba>
[…]

OK

对于 4G：
+QOPS:
<oper_in_string>,<oper_in_short_string>,<oper_in_number>
<index>,<RAT>,<freq>,<pci>,<tac>,<ci>,<rsrp>,<rsrq>,<cba>
[…]

OK

如果发生任何错误：
ERROR
<oper_in_string> 长字符串形式的运营商名称。
<oper_in_short_string> 短字符串形式的运营商名称。
<per_in_number> 整型形式的运营商名称。
<index> 整型。结果中的条目 ID。
<RAT> 字符串类型。
"2G"    2G 网络
"3G"    3G 网络
"4G"    4G 网络
<freq> 十进制数字格式。小区的 ARFCN 或 UARFCN。
<lac> 十六进制数字格式。位置区码。
<ci> 十六进制数字格式。小区 ID。
<bsic> 十进制数字格式。基站识别码。
<rxlev> 十进制数字格式。RX 电平。
<c1> 十进制数字格式。小区选择准则。
<cba> 十进制数字格式。小区接入限制 (Cell bar access)。
0 未限制小区
1 受限小区
<is_gprs_support> 十进制数字格式。指示当前小区是否支持 GPRS。
0 不支持 GPRS
1 支持 GPRS
<psc> 十进制数字格式。主扰码。

1. 本命令与固定为某一网络类型的网络选择模式冲突。必须通过 AT+QCFG="NWSCANMODE",0 将网络选择模式设置为 AUTO 模式。
2. 在空闲状态下执行此命令。如果已建立 CS 或 PS 连接，空中信令将中断 AT+QOPS，然后模组将返回 ERROR。
3. 使用本命令扫描频段前，请先配置网络模式和特定频段。

示例
AT+QOPSCFG="scancontrol",0              //配置扫描 2G 网络中的所有频段。
OK
AT+QOPS            //扫描 2G 网络中的所有频段。
+QOPS: "CHINA MOBILE","CMCC","46000"
1,"2G",16,550B,D89,16,35,27,0,1
2,"2G",124,550B,3A40,20,80,1,0,1
...
+QOPS: "CHN-UNICOM","UNICOM","46001"
1,"2G",234,5504,56E3,27,44,12,0,1
2,"2G",536,6254,7F62,13,70,1,0,1
....

OK
AT+QOPSCFG="scancontrol",1              //配置扫描 3G 网络中的所有频段。
OK
AT+QOPS            //扫描 3G 网络中的所有频段。
+QOPS: "CHN-UNICOM","UNICOM","46001"
1,"3G",10688,5,D5D5,8055189,-109,27,0

OK
AT+QOPSCFG="scancontrol",2              //配置扫描 4G 网络中的所有频段。
OK
AT+QOPS            //扫描 4G 网络中的所有频段。
+QOPS: "CHINA MOBILE","CMCC","46000"
1,"4G",38950,206,550B,F2D4A42,-72,-11,0
2,"4G",39148,206,550B,F2D4A44,-73,-12,0
<rscp> 十进制数字格式。接收信号码功率电平。
<ecno> 十进制数字格式。网络质量指示。
<pci> 十进制数字格式。物理小区 ID。
<tac> 十进制数字格式。跟踪区码。
<rsrp> 参考信号接收功率。
<rsrq> 参考信号接收质量。
注意

3,"4G",1300,121,550B,5C4EF2D,-99,-17,0
4,"4G",38400,121,550B,5C4EF01,-99,-16,0
5,"4G",3683,121,550B,5C4EF29,-99,-11,0
6,"4G",38098,428,550B,F48330E,-112,-20,0
7,"4G",1425,116,550B,80A61AA,-118,-25,0
+QOPS: "CHN-CT","CT","46011"
1,"4G",100,466,691D,DD8A30B,-75,-11,0
2,"4G",1850,314,691D,690843E,-88,-12,0
3,"4G",2452,9,691D,690271D,-97,-12,0
+QOPS: "CHN-UNICOM","UNICOM","46001"
1,"4G",1650,465,550C,5A29C0B,-78,-10,0
2,"4G",3770,312,550C,5F1EA65,-98,-13,0
3,"4G",1506,330,550C,5A7980D,-107,-15,0

OK
AT+QOPSCFG="scancontrol",3           //配置扫描 2G、3G 和 4G 网络中的所有频段。
OK
AT+QOPS         //扫描 2G、3G 和 4G 网络中的所有频段。
+QOPS: "CHINA MOBILE","CMCC","46000"
1,"2G",32,550B,34B8,63,26,18,0,1
2,"2G",16,550B,D89,34,26,18,0,1
3,"4G",39148,206,550B,F2D4A44,-71,-4,0
4,"4G",38950,206,550B,F2D4A42,-80,-4,0
5,"4G",1300,121,550B,5C4EF2D,-100,-4,0
6,"4G",38400,121,550B,5C4EF01,-101,-11,0
7,"4G",3683,471,550B,84958A8,-103,-4,0
8,"4G",38544,168,550B,104FD44,-111,-11,0
9,"4G",36275,169,550B,104FD77,-116,-13,0
10,"4G",40738,428,550B,F48330E,-119,-11,0
+QOPS: "CHN-UNICOM","UNICOM","46001"
1,"3G",10688,387,D5D6,8066479,-106,23,0
2,"4G",1650,465,550C,5A29C0B,-74,0,0
3,"4G",3770,312,550C,5F1EA65,-96,-4,0
4,"4G",1506,330,550C,5A7980D,-108,-4,0
+QOPS: "CHN-CT","CT","46011"
1,"4G",100,466,691D,DD8A30B,-71,-4,0
2,"4G",2452,9,691D,690271D,-92,-10,0
3,"4G",1850,314,691D,690843E,-99,-4,0
+QOPS: "AT&T","AT&T","310410"
1,"4G",2525,3,1,1A2D003,-106,-15,0

OK
AT+QOPSCFG="scancontrol",2,0,1,0         //配置在 4G 中扫描 LTE Band1。
OK

AT+QOPS            //在 4G 中扫描 LTE Band1。
+QOPS: "CHN-CT","CT","46011"
1,"4G",100,466,691D,DD8A30B,-74,-12,0

OK
AT+QOPSCFG="displayrssi",1               //启用显示 RSSI。
OK
AT+QOPSCFG="scancontrol",2,0,1,0         //配置在 4G 中扫描 LTE Band1。
OK
AT+QOPS            //在 4G 中扫描 LTE Band1。
+QOPS: "CHN-CT","CT","46011"
1,"4G",100,466,691D,DD8A30B,-71,-11,-40,0    //RSSI 的值为 -40。

OK

6.16. AT+QFPLMNCFG  FPLMN 配置 (FPLMN Configuration)

本命令配置 FPLMN（禁止公共陆地移动网络），包括将 PLMN 添加到 FPLMN、从 FPLMN 列表中删除 PLMN。
AT+QFPLMNCFG  FPLMN 配置 (FPLMN Configuration)
测试命令
AT+QFPLMNCFG=?
响应
+QFPLMNCFG: "List"
+QFPLMNCFG: "Add",<PLMN>
+QFPLMNCFG: "Delete",(<PLMN>,"all")

OK
写入命令
AT+QFPLMNCFG=<cmd>[,<PLMN>][,
(<PLMN>,"all")]
响应
如果 <cmd> 等于 "List"，则返回当前 FPLMN 列表：
+QFPLMNCFG: "List",<index>,<PLMN>
[+QFPLMNCFG: "List",<index>,<PLMN>
[…]]

OK

如果 <cmd> 等于 "Add" 或 "Delete"：
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>

参数
示例
AT+QFPLMNCFG=?
+QFPLMNCFG: "List"
+QFPLMNCFG: "Add",<PLMN>
+QFPLMNCFG: "Delete",(<PLMN>,"all")

OK
AT+QFPLMNCFG="List"
+QFPLMNCFG: "List",1,"46000"
+QFPLMNCFG: "List",2,"46002"
+QFPLMNCFG: "List",3,"46004"
+QFPLMNCFG: "List",4,"46007"
+QFPLMNCFG: "List",5,"46008"
+QFPLMNCFG: "List",6,"46003"
+QFPLMNCFG: "List",7,"46011"
+QFPLMNCFG: "List",8,"46008"

OK
AT+QFPLMNCFG="Add","46001"   //将 PLMN "46001" 添加到 FPLMN 列表。
OK
AT+QFPLMNCFG="List"
+QFPLMNCFG: "List",1,"46000"
+QFPLMNCFG: "List",2,"46002"
+QFPLMNCFG: "List",3,"46004"
+QFPLMNCFG: "List",4,"46007"
+QFPLMNCFG: "List",5,"46008"
+QFPLMNCFG: "List",6,"46003"
+QFPLMNCFG: "List",7,"46011"
+QFPLMNCFG: "List",8,"46008"
最大响应时间 300 ms
特性 该命令立即生效。
该配置将自动保存。
<cmd>      字符串类型。FPLMN 的操作命令。
                "List"  禁止 PLMN 列表
                "Add"  将指定的 PLMN 添加到 FPLMN
                "Delete"  从 FPLMN 中删除指定的 PLMN 或所有 PLMN
<index>   整型。FPLMN 的索引。
<PLMN>  整型。PLMN。
<err>           错误码。更多详情，请参阅第 15.4 章。

+QFPLMNCFG: "List",9,"46001"

OK
AT+QFPLMNCFG="Delete","46001"  //从 FPLMN 列表中删除 PLMN "46001"。
OK
AT+QFPLMNCFG="List"
+QFPLMNCFG: "List",1,"46000"
+QFPLMNCFG: "List",2,"46002"
+QFPLMNCFG: "List",3,"46004"
+QFPLMNCFG: "List",4,"46007"
+QFPLMNCFG: "List",5,"46008"
+QFPLMNCFG: "List",6,"46003"
+QFPLMNCFG: "List",7,"46011"
+QFPLMNCFG: "List",8,"46008"

OK
AT+QFPLMNCFG="Delete","all"          //从 FPLMN 列表中删除所有 PLMN。
OK

AT+QFPLMNCFG="List"
OK

6.17. AT+QENG  开启/关闭工程模式 (Switching on/off Engineering Mode)

工程模式旨在上报服务小区、相邻小区和分组交换参数的信息。该命令开启/关闭该模式。
AT+QENG  开启/关闭工程模式 (Switching on/off Engineering Mode)
测试命令
AT+QENG=?
响应
+QENG: (list of supported <cell_type>s)

OK
AT+QENG="servingcell"
查询服务小区的信息

响应
在 GSM 模式下：
+QENG: "servin gscell",<state>,"GSM",<mcc>,<mnc>,<L
AC>,<cellID> ,<BSIC>,<arfcn>,<band>,<rxlev>,<txp>,<rl
a>,<drx>,<c1>,<c2>,<gprs>,<tch>,<ts> ,<ta>,<maio>,<hs
n>,<rxlevsub>,<rxlevfull>,<rxqualsub>,< rxqualfull>,<voi
cecodec>

OK

在 WCDMA 模式下：
+QENG: "servingc ell",<state>,"WCDMA",<mcc>,<mnc>,
<LAC>,<cellID>,<uarfcn>,<psc>,<rac>,<rscp>,<ecio>,<ph
ych>,<SF>,<slot>,<speech_code>,<ComMod>

OK

在 LTE 模式下：
+QENG: "servingcell ",<state>,"LTE",<is_tdd>,<mcc>,<m
nc>,<cellID>,<pcid>,<earfcn>,<freq_band_ind>,<ul_band
width>,<dl_bandwidth>,<tac>,< rsrp>,<rsrq>,<rssi>,<si n
r>,<srxlev>

OK

在 TD-SCDMA 模式下：
+QENG: "serv ingscell",<state>,"TDSCDMA",<mcc>,<mn
c>,<LAC>,<cellID>,<pfreq>,<rssi>,<rscp>,<ecio>

OK

在 CDMA 模式或 CDMA+HDR 模式下：
+QENG: "servingscell",<state>,"CDMA",<mcc>,<mnc>,<
LAC>,<cellID>,<bcch>,<rxpwr>,<ecio>,<txpwr>
[+QENG: "servingscell",<state >,"HDR",<mcc>,<mnc>,<L
AC>,<cellID>,<bcch>,<rxpwr>,<ecio>,<txpwr>]

OK

在 SRLTE 模式下：
+QENG: "servingscell",<state>,"CDMA",<mcc>,<mnc>,<
LAC>,<cellID>,<bcch>,<rxpwr>,<ecio>,<txpwr>
+QENG: "servingcell",<state>,"LTE",<is_tdd>,<mcc>,<m
nc>,<cellID>,<pcid>,<earfcn>,<freq_band_ind>,<ul_band
width>,<dl_ba ndwidth>,<tac>,<rsrp>,<rsrq>,<rs si>,<sin
r>,<srxlev>

OK
AT+QENG="neighbourcell"
查询相邻小区的信息

响应
在 GSM 模式下：
[+QENG: "neighbourcell","GSM",<mcc>,<mnc>,<LAC>,<
cellID>,<BSIC>,<arfcn>,<rxlev>,<c1>,<c2>,<c31>,<c32>
[…]]
[+QENG: "neighbourcell","WCDMA",<uarfcn>,<psc>,<rs

cp>,<ecno>
[…]]
[+QENG: "neighbourcell","LTE",<earfcn>,<pcid>,<rsrp>,
<rsrq>
[…]]

OK

在 WCDMA 模式下：
[+QENG: "neighbourcell"," WCDMA",<uarfcn>,<srxqua
l>,<psc>,<rscp>,<ecno>,<set>,<rank>,<srxlev>
[…]]
[+QENG: "neighbourcell","GSM",<BSIC>,<rssi>,<rxlev>,
<rank>
[…]]
[+QENG: "neighbourcell","LTE",<earfcn>,<pcid>,<rsrp>,
<rsrq>,<s_rxlev>
[…]]

OK

在 LTE 模式下：
[+QENG:
"neighbourcell intra","LTE",<earfcn>,<pcid>,<rsrq>,<rsr
p>,<rssi>,<sinr>,<srxlev>,<cell_resel_priority>,<s_non_i
ntra_search>,<thresh_serving_low>,<s_intra_search>
[…]]
[+QENG:
"neighbourcell inter","LTE",<earfcn>,<pcid>,<rsrq>,<rsr
p>,<rssi>,< sinr>,<srxlev>,<thres hX_low>,<threshX_hig
h>,<cell_resel_priority>
[…]]
[+QENG:
"neighbourcell","GSM",<arfcn>,<cell_resel_priority>,<th
resh_gsm_high>,<thres h_gsm_low>,<ncc_permitted>,<
band>,<bsic_id>,<rssi>,<srxlev>
[…]]
[+QENG:
"neighbourcell ","WCDMA",<uarfcn>,<cell_resel_prio rit
y>,<thresh_Xhigh>,<thresh_Xlow>,<psc>,<cpich_rsc p>,
<cpich_ecno>,<srxlev>
[…]]

OK

参数
AT+QENG="3gcomm"
获取 3G 小区公共信息

响应
仅在 WCDMA 模式下，获取 3G 小区公共项，其中包括
3G 相邻小区、2G 相邻小区和 3G 服务小区的信息。

对于 WCDMA 服务小区信息：
[+QENG: "3gcomm",<cell_type> ,<rat>,<state>,<mcc>,<
mnc>,<LAC>,<cellID>,<uarfcn>,<psc>,<rssi>,<rscp>,<ec
n0>,<srxqual>,<srxlev>
[…]]

对于 WCDMA 服务小区的 3G 相邻小区信息：
[+QENG: "3gcomm",<cell_type>,<rat>,<mcc>,<mnc>,<L
AC>,<cellID>,<uarfcn>,<psc>,<rssi>,<rscp>,<ecn0>,<srx
qual>,<srxlev>
[…]]

对于 WCDMA 服务小区的 2G 相邻小区信息：
[+QENG: "3gcomm ",<cell_type>,<rat>,<arfcn>,<BSIC>,<
rssi>,<rxlev>,<rank>
[…]]

OK

如果模组工作在 2G 网络中，则响应：
OK
最大响应时间 300 ms
特性 /
<cell_type>      字符串格式。不同小区的信息。
    "servingcell"     2G/3G/4G 服务小区的信息
                "neighbourcell"   2G/3G/4G 相邻小区的信息
<state>         字符串格式。UE 状态。
 "SEARCH"     UE 正在搜索，但（尚）未找到合适的 2G/3G/4G 小区。
    "LIMSRV"     UE 已驻留在一个小区上，但尚未注册到网络。
                "NOCONN" UE 已驻留在一个小区上并已注册到网络，且处于空闲模式。
"CONNECT" UE 已驻留在一个小区上并已注册到网络，且通话正在进行中。
<rat>           字符串格式。接入技术，包括：

                "GSM"
    "WCDMA"
    "LTE"
    "CDMA"
    "HDR"
    "TDSCDMA"
<mcc>          整型。移动国家码（PLMN 码的第一部分）。
"-"          无效
<mnc>          整型。移动网络码（PLMN 码的第二部分）。
    "-"        无效
<LAC>         十六进制格式。位置区码。确定所扫描小区的两字节十六进制位置区码（例如 00C1 等于十进制 193）。
范围：0-0xFFFFFFF。
 "-"    无效
<cellID>        十六进制格式。小区 ID。确定 16 位（GSM）或 28 位（UMTS）小区 ID。
范围：0-0xFFFFFFF。
 "-"    无效
<BSIC>         整型。基站识别码。范围：0–63。
<arfcn>         整型。确定所扫描小区的 ARFCN。范围：0-1023。
<band>         整型。当前频段。
    0           DCS_1800
1    PCS_1900
    "-"     其他频段
<rac>           整型。路由区码。范围：0–255。
<pfreq>   主频率。
<rxlev>          整型。用于基站选择的 RX 电平值，单位为 dB（参见 3GPP 25.304）。
范围：0-63。将 RX 电平值减去 111 即可得到 dBm 值。
<txp>           整型。CCH 上的 MS 最大发射功率。
<rla>            整型。最小接入 RX 电平。
<drx>           整型。不连续接收周期长度。
<c1>            整型。小区选择准则。
<c2>            整型。小区重选准则。
<gprs>          整型。当前小区是否支持 GPRS。
    0 不支持 GPRS
1 支持 GPRS
<tch>           整型。在跳频时显示 'h'，否则显示语音通话中的当前 ARFCN。
<ts>            整型。时隙号。
<ta>            整型。到基站的时间提前量。范围：0–63。
<maio>         整型。移动分配索引偏移量。
<hsn>          整型。跳频序列号。
<rxqualsub>    整型。RX 质量（子）。范围：0–7。
<rxqualfull>     整型。RX 质量（全）。范围：0–7。
<rxlevsub>      整型。RX 电平（子）。范围：0–63。

<rxlevfull>      整型。RX 电平（全）。范围：0–63。
<voicecodec>  字符串格式。语音通话期间的信道模式。
    "HR"          半速率
    "FR"          全速率
    "EFR"        增强全速率
    "AMR"        自适应多速率
    "AMRHR"      AMR 半速率
    "AMRFR"      AMR 全速率
                "AMRWB"     AMR 宽带
    "-"           无效
<uarfcn>         整型。所扫描小区的 UTRA-ARFCN。
<earfcn>         整型。所扫描小区的 E-UTRA-ARFCN。
<psc>           整型。该参数确定所扫描小区的主扰码。
<rssi>  整型。接收信号强度指示。
<sinr>  整型。SINR 的对数值。范围：-20–+30。单位：dB。
<rscp>          整型。所扫描小区的接收信号码功率电平。
<srxlev>       整型。用于基站选择的 RX 电平值，单位为 dB（参见 3GPP 25.304）。
<SF>           整型。扩频因子。值为 4、8、16、32、64、128、256 和 512。
0  SF_4
1  SF_8
2  SF_16
3  SF_32
4  SF_64
5  SF_128
6  SF_256
7  SF_512
8  未知
<slot>           整型。DPCH 的时隙格式（0–16）。FDPCH 的时隙格式（0–9）。
<ComMod>  整型。是否支持压缩模式。
    0    不支持压缩模式
    1    支持压缩模式
<c31>           整型。GPRS 小区选择准则。
<c32>           整型。GPRS 小区重选准则。
<set>           整型。3G 相邻小区集。
                1         激活集
                2         同步相邻集
                3         异步相邻集
<rank>          用于异 RAT 小区重选时该小区作为相邻小区的排名。
<txpwr>         整型。UE 的 TX 功率电平。
<is_tdd>         TDD 或 FDD 模式。
<pcid>          物理小区 ID
<freq_band_ind>  E-UTRA 频率频段（参见 3GPP 36.101）。
<ul_bandwidth>  整型。UL 带宽。

0     1.4 MHz
1     3 MHz
2     5 MHz
3     10 MHz
4     15 MHz
5     20 MHz
<dl_bandwidth>   整型。DL 带宽。
0     1.4 MHz
1     3 MHz
2     5 MHz
3     10 MHz
4     15 MHz
5     20 MHz
<tac>            跟踪区码（参见 3GPP 23.003 第 19.4.2.3 章）。
<rsrp>           参考信号接收功率（参见 3GPP 36.214 第 5.1.1 章）。
<rsrq>           参考信号接收质量（参见 3GPP 36.214 第 5.1.2 章）。
<thresh_serving_low>  在向较低优先级 RAT/频率重选时，UE 在服务小区上使用的 <srxlev> 阈值（单位为 dB）。
<ecio>                整型。载干比，单位为 dB = 实测的 Ec/Io 值，单位为 dB。
<phych>               0     DPCH
      1     FDPCH
<speech_code>   呼叫将被转移到的目标号码。
<rxpwr>                 RX 功率值，分辨率为 1/10 dBm。
<ecno>                 整型。载干比，单位为 dB = 实测的 Ec/Io 值，单位为 dB。
<srxqual>              驻留频率上的接收机自动增益控制。
<s_rxlev>              异频小区合适的接收电平。
<cell_resel_priority>    整型。小区重选优先级。范围：0–7。
<s_non_intra_search>   用于控制非频率内搜索的阈值。
<s_intra_search>      频率内小区的小区选择参数。
<serving_cell_id>       整型。LTE 服务小区 ID。这是服务小区的小区 ID，可以在小区列表中找到。范围：0–503。
<threshX_low>           重选时需要参考。被评估的低优先级小区的合适接收电平值必须大于此值。
<threshX_high>          重选时需要参考。被评估的高优先级小区的合适接收电平值必须大于此值。
<thresh_gsm_high>  高优先级层的重选阈值。
<thresh_gsm_low>  低优先级层的重选阈值。
<ncc_permitted>        位掩码，指定是否上报具有特定网络色码的相邻小区。第 n 位设置为 1 表示具有 NCC n 的相邻小区应包含在上报中。
<bsic_id>               基站识别码 ID。
<thresh_Xhigh>         高优先级层的重选阈值。
<thresh_Xlow>          低优先级层的重选阈值。
<cpich_rscp>       UE 接收到的公共导频信道的绝对功率电平，单位为

        dBm × 10。
<cpich_ecno>      在 UE 天线连接器处，公共导频信道的每 PN 码片接收能量与总接收功率谱密度之比，单位为 dB×10。
<bcch>             EARFCN。当前系统的激活信道。

1. 如果返回 "-" 或 -，则表示该参数在当前条件下无效。
2. 2G 相邻小区仅在空闲模式下可见。
示例
AT+QENG="servingcell"
+QENG: "servingcell","SEARCH"

OK
AT+QENG="servingcell"
+QENG:"servingcell","LIMSRV","GSM",460,01,5504,2B55,52,123,0,-67,5,14,64,30,28,0,-,-,-,-,-,-,-,-,-,"
-"

OK
AT+QENG="servingcell" //获取空闲状态下 GSM 模式的服务小区信息。
+QENG:"servingcell","NOCONN","GSM",460,01,5504,2B55,52,123,0,-111,5,14,64,0,0,0,-,-,-,-,-,-,-,-,-,
"-"

OK
AT+QENG="servingcell" //获取连接状态下 GSM 模式的服务小区信息。
+QENG:"servingcell","CONNECT","GSM",460,00,550A,2BB9,23,94,0,-61,5,14,4,0,0,0,h,1,0,0,33,50,
52,0,0,"EFR"

OK
AT +QENG="neighbourcell" //获取 LTE 模式的相邻小区信息。
+QENG: "neighbourcell intra","LTE",38950,276,-3,-88,-65,0,37,7,16,6,44
+QENG: "neighbourcell inter","LTE",39148,-,-,-,-,-,37,0,30,7,-,-,-,-
+QENG: "neighbourcell inter","LTE",37900,-,-,-,-,-,0,0,30,6,-,-,-,-
+QENG: "neighbourcell","GSM",0,3,14,50,255,0,0,-1920,0
+QENG: "neighbourcell","GSM",94,3,14,50,255,0,0,-1920,0
+QENG: "neighbourcell","GSM",93,3,14,50,255,0,0,-1920,0
+QENG: "neighbourcell","GSM",91,3,14,50,255,0,0,-1920,0
+QENG: "neighbourcell","GSM",90,3,14,50,255,0,0,-1920,0
+QENG: "neighbourcell","GSM",89,3,14,50,255,0,0,-1920,0
+QENG: "neighbourcell","GSM",87,3,14,50,255,0,0,-1920,0
+QENG: "neighbourcell","GSM",85,3,14,50,255,0,0,-1920,0

注意

OK
AT+QENG="neighbourcell" //获取 WCDMA 模式的相邻小区信息。
+QENG: "neighbourcell","WCDMA",10713,-723,398,-880,-155,6,-32768,-
+QENG: "neighbourcell","WCDMA",10713,-723,331,-870,-155,2,-32768,-
+QENG: "neighbourcell","WCDMA",10713,-723,290,-880,-165,2,-32768,-
+QENG: "neighbourcell","WCDMA",10713,-723,397,-910,-190,2,-32768,-
+QENG: "neighbourcell","WCDMA",10713,-723,114,-910,-195,2,-32768,-
+QENG: "neighbourcell","WCDMA",10713,-723,332,-940,-220,2,-32768,-
+QENG: "neighbourcell","WCDMA",10713,-723,379,-950,-230,2,-32768,-
+QENG: "neighbourcell","WCDMA",10713,-723,115,-1210,-250,6,-32768,-

OK
AT+QENG="3gcomm"      //获取 WCDMA 模式下的公共信息。
+QENG:"3gcomm","servingcell","3G","NOCONN",460,01,D5D6,8062AF1,10713,38,-72,-74,11,25,32
+QENG: "3gcomm","neighbourcell","3G",460,01,D5D6,8062AEF,10713,36,-87,-87,36,0,27
+QENG: "3gcomm","neighbourcell","2G",123,52,-98,12,-5

OK

6.18. AT+CIND  控制指示命令 (Command of Control Instructions)
参数
AT+CIND  控制指示命令 (Command of Control Instructions)
测试命令
AT+CIND=?
响应
+CIND:(<descr>,(list of supported <ind>s))[,(<descr>,(list of
supported <ind>s))[,...]]
OK
读取命令
AT+CIND?
响应
+CIND: <ind>[,<ind>[,...]]

OK
如果错误与 ME 功能相关：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
<descr>  字符串类型。指示状态。详见以下注意事项。
<ind>   整型。指示事件。与 <descr> 的值相关。详见以下注意事项。

<descr> 和 <ind> 的值描述如下：

<descr> <ind>
"battchg" 电池电量级别。范围：0-5。
"signal"
信号强度指示。
0–5：信号分为五个级别。值越大，
信号越好。
"service"
网络服务状态指示。
0 未注册到网络
1 已注册到已知网络
"call"
呼叫状态指示。
0 无呼叫
1 有呼叫
"roam"
漫游指示。
0 已注册到归属网络或未注册的网络
1 已注册到漫游网络
"smsfull" MT 中的短消息存储器已满（'0'），或存储位置可用（'1'）。
"GPRS coverage"
PS 域注册指示。
0 未在 PS 域注册
1 已在 PS 域注册
"callsetup"
呼叫建立呼叫类型：
0 无
1 MTRING
2 MOINIT
3 MORING
示例
AT+CIND=?
+CIND: (" battchg",(0-5)),("signal",(0-5)),("service",(0-1)),("call",(0-1)),("roam",(0-1)),("smsfull",(0-
1)),("GPRS coverage" ,(0-1)),("callsetup",(0-3))

OK
AT+CIND?
+CIND: 0,3,1,0,0,0,1,0

OK

<err>       错误码。更多详情，请参阅第 15.4 章。
注意
