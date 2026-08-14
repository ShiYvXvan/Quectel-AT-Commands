# 4 状态控制指令 (Status Control Commands)

4 状态控制指令

4.1. AT+CPAS  移动设备活动状态

本指令用于查询模组的活动状态。
参数
AT+CPAS  移动设备活动状态
测试命令
AT+CPAS=?
响应
+CPAS: (list of supported <pas>s)

OK
执行命令
AT+CPAS
响应
TA 返回 ME 的活动状态：
+CPAS: <pas>

OK
或者
ERROR

如果存在与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

<pas>  整型。ME 活动状态。
   0  就绪
   3  振铃
   4    通话进行中或通话保持
<err>       错误码。更多详情请参阅第 15.4 章。

示例
AT+CPAS
+CPAS: 0        //The module is idle

OK
RING
AT+CLCC
+CLCC: 1,1,4,0,0,"15695519173",161

OK
AT+CPAS
+CPAS: 3        //The module is ringing

OK
AT+CLCC
+CLCC: 1,0,0,0,0,"10010",129

OK
AT+CPAS
+CPAS: 4                 //Call in progress

OK

4.2. AT+CEER  扩展错误报告

本指令用于查询扩展错误，并报告最近一次失败操作的原因，例如：

⚫ 呼叫释放失败
⚫ 呼叫建立失败（包括主叫或被叫）
⚫ 使用补充业务修改呼叫失败
⚫ 激活、注册、查询、去激活或注销补充业务失败
⚫ GPRS 附着失败或 PDP 上下文激活失败
⚫ GPRS 去附着失败或 PDP 上下文去激活失败

释放原因 <text> 是用于描述网络给出的原因信息的文本。
AT+CEER  扩展错误报告
测试命令
AT+CEER=?
响应
OK
执行命令
AT+CEER
响应
+CEER: <text>

参数
<text>            释放原因文本。最近一次呼叫建立或释放失败的原因（列于第 15.8 章）。CS 和 PS 域的呼叫类型均会被报告。原因数据从呼叫管理器事件中获取，并在本地缓存以供本指令稍后使用。
<err>       错误码。更多详情请参阅第 15.4 章。

4.3. AT+QINDCFG  URC 指示配置

本指令用于控制 URC 指示。

OK
或者
ERROR

如果存在与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
AT+QINDCFG  URC 指示配置
测试命令
AT+QINDCFG=?
响应
+QINDCFG: "all",(list of supported <enable>s),(list of
supported <save_to_nvram>s)
+QINDCFG: "csq",(list of supported <enable>s),(list of
supported <save_to_nvram>s)
+QINDCFG: "smsfull",(list of supported <enable>s),(list of
supported <save_to_nvram>s)
+QINDCFG: "ring",(list of supported <enable>s),(list of
supported <save_to_nvram>s)
+QINDCFG: "smsincoming",(list of supported
<enable>s),(list of supported <save_to_nvram>s)
+QINDCFG: "act",(list of supported <enable>s),(list of
supported <save_to_nvram>s)
+QINDCFG: "ccinfo",(list of supported <enable>s),(list of
supported <save_to_nvram>s)

OK

参数
<urctype>             字符串类型。URC 类型。
                       "all"          所有 URC 的总开关。默认值：ON。
 "csq"         信号强度及信道误码率变化的指示（类似于 AT+CSQ）。默认值：OFF。如果
此配置为 ON，则上报：
            +QIND: "csq",<rssi>,<ber>
"smsfull"            SMS 存储已满指示。默认值：OFF。如果此配置为 ON，则上报：
                                             +QIND: "smsfull",<storage>
                       "ring"                 "RING" 指示。默认值：ON。
                       "smsincoming"         来电消息指示。默认值：ON。
相关 URC 列表：
 +CMTI, +CMT, +CDS
"act"                网络接入技术变化的指示。默认值：OFF。如果此配置为 ON，则上报：
                       +QIND: "act",<actvalue>
                       <actvalue> 为字符串格式。其取值如下：
                       "GSM"
                       "EGPRS"
                       "WCDMA"
                       "HSDPA"
                       "HSUPA"
                       "HSDPA&HSUPA"
"LTE"
"TD-SCDMA"
写入命令
AT+QINDCFG=<urctype>[,<enable>[,<
save_to_nvram>]]
响应
如果省略可选参数，则查询当前配置：
+QINDCFG: <urctype>,<enable>

OK

如果指定了可选参数，则设置 URC 指示配置：
OK
或者
ERROR

如果存在与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms

"CDMA"
                                             "HDR"
"EVDO"
                       "UNKNOWN"
                       URC 示例如下：
                       +QIND: "act","HSDPA&HSUPA"
                       +QIND: "act","UNKNOWN"
                       关于 "act" 的说明如下：
1. 如果模组未注册到网络，则 <actvalue> 为 "UNKNOWN"。
2. 如果此配置为 ON，则立即上报 "act" 的 URC。仅当网络接入技术发生变化时，才会上报新的 URC。
                       "ccinfo"                 语音通话状态变化指示。默认值：0。默认禁用，设置为 1 以启用，并上报 +QIND:
"ccinfo",<id>,<dir>,<state>,<mode>,<mpty>,<nu
mber>,<type>[,<alpha>]。
<enable>            整型。URC 指示为 ON 或 OFF。
0   OFF
1   ON
<save_to_nvram>      整型。是否将配置保存到 NVM。
                       0    不保存
1 保存
<err>                  整型。错误码的详细信息请参阅第 15.4 章。

4.4. AT+QMBNCFG  MBN 文件配置设置

AT+QMBNCFG   MBN 文件配置设置
测试命令
AT+QMBNCFG=?
响应
+QMBNCFG: "List"
+QMBNCFG: "Select"[,<MBN name>]
+QMBNCFG: "Deactivate"
+QMBNCFG: "AutoSel"[,(0,1)]
+QMBNCFG: "Delete","<MBN name>"
+QMBNCFG: "Add","<filename>"
+QMBNCFG: "List_all"

OK

4.4.1. AT+QMBNCFG="List"  查询已导入的 MBN 文件列表
本指令用于查询已导入的 MBN 文件列表。
参数
示例
AT+QMBNCFG="list"
+QMBNCFG: "List",0,0,1,"ROW_Generic_3GPP",0x06010821,201706061
+QMBNCFG: "List",1,0,0,"Volte_OpenMkt-Commercial-CMCC",0x06012064,201706061
+QMBNCFG: "List",2,0,0,"OpenMkt-Commercial-CU",0x06011510,201706062
+QMBNCFG: "List",3,0,0,"Telstra-Commercial_VoLTE",0x0680010F,201710261
+QMBNCFG: "List",4,1,0,"hVoLTE-Verizon",0x060101A0,201801081

OK

AT+QMBNCFG="List"  查询已导入的 MBN 文件列表
写入命令
AT+QMBNCFG="List"
响应
+QMBNCFG:"List",<index>,<selected>,<activate>,<MBN na
me>,<MBN_version>,<MBN_release_date>
…

OK
最大响应时间 300 ms
特性 本指令立即生效。
配置不会自动保存。
<index>  整型。MBN 索引，表示当前列出的是哪一个已导入的 MBN 文件。
<selected>    整型。指示该 MBN 文件是否被选中。
       0  未选中
       1  已选中
<activate>   整型。指示该 MBN 文件是否已激活。
       0  未激活
    1  已激活
<MBN name>   字符串类型。已导入的 MBN 文件的名称。
<MBN_version>   字符串类型。已导入的 MBN 文件的版本。
<MBN_release_date> 字符串类型。已导入的 MBN 文件的发布日期。

4.4.2. AT+QMBNCFG="Select"  选择已导入的 MBN 文件
本指令用于选择一个已加载的 MBN 文件，当模组重新启动后，所选中的 MBN 文件将被激活。
参数

4.4.3. AT+QMBNCFG="Deactivate"  去激活 MBN 文件
MBN 文件去激活后，当前激活的 MBN 文件将变为非激活状态。

AT+QMBNCFG="Select"  选择已导入的 MBN 文件
写入命令
AT+QMBNCFG="Select"[,<MB
Nname>]
响应
如果省略可选参数，则查询当前配置：
+QMBNCFG: "Select",<MBN name>

OK

如果指定了可选参数，则选择指定的 MBN 文件：
OK
或者
ERROR
最大响应时间 300 ms
特性 本指令在重启后生效。
<MBN name>          整型。要选择的 MBN 文件名称。
AT+QMBNCFG="Deactivate"  去激活 MBN 文件
写入命令
AT+QMBNCFG="Deactivate"
响应
OK
或者
ERROR
最大响应时间 300 ms
特性 本指令立即生效。

4.4.4. AT+QMBNCFG="AutoSel"  自动选择是否激活 MBN 文件
本指令用于配置是否可通过 (U)SIM 卡自动选择 MBN 文件。
参数

4.4.5. AT+QMBNCFG="Add"  添加 MBN 文件
本指令用于添加 MBN 文件。
AT+QMBNCFG="AutoSel"  自动选择是否激活 MBN 文件
写入命令
AT+QMBNCFG="AutoSel"
响应
+QMBNCFG: "AutoSel",<enable>

OK
或者
ERROR
执行命令
AT+QMBNCFG="AutoSel"[,<en
able>]
响应：
如果省略可选参数，则查询当前配置：
+QMBNCFG: "AutoSel",<enable>

OK
或者
ERROR

如果指定了可选参数，则配置是否可通过 (U)SIM 卡自动选择 MBN 文件：
OK
或者
ERROR
最大响应时间 300 ms
特性 本指令在模组重新启动后生效。
配置将自动保存。
<enable>       整型。启用/禁用自动激活 MBN 文件。
    0 禁用
    1 启用
AT+QMBNCFG="Add"  添加 MBN 文件
写入命令
AT+QMBNCFG="Add",<filename>
响应
OK
或者

参数

4.4.6. AT+QMBNCFG="Delete"  删除 MBN 文件
本指令用于从 EFS 中删除 MBN 文件。
参数

4.4.7. AT+QMBNCFG="List_all"  查询所有已导入的 MBN 文件列表中包含的 PLMN
本指令用于查询所有已导入的 MBN 文件列表中包含的 PLMN。
ERROR
最大响应时间 300 ms
特性 本指令立即生效。
配置将自动保存。
<filename>       字符串类型。要添加的 MBN 文件的名称。
AT+QMBNCFG="Delete"  删除 MBN 文件
写入命令：
AT+QMBNCFG="Delete",<MBN
name>
响应
OK
或者
ERROR
特性 本指令在模组重新启动后生效。
<MBN_name>       字符串类型。要删除的 MBN 文件的名称。
AT+QMBNCFG="List_all"  查询所有已导入的 MBN 文件列表中包含的 PLMN
写入命令
AT+ QMBNCFG="List_all"
响应
+QMBNCFG: "List_all",<index>,<selected>,<activated>,"<MBN
name>",<MBN_version>,<MBN_release_date>,<PLMN_list>
…

OK

参数
示例
AT+QMBNCFG="List_all"       //Query PLMN contained in all imported lists of MBN files.
+QMBNCFG: "List_all",0,0,0,"ROW_Generic_3GPP",0x05010814,201704141, ''''
+QMBNCFG: "List_all",1,0,0,"OpenMkt-Commercial-CU",0x05011510,201704141,''460-01 460-09
460-06''
+QMBNCFG: "List_all",2,1,1,"OpenMkt-Commercial-CT",0x0501131C,201704141,''455-07 460-11
460-03''
+QMBNCFG: "List_all",3,0,0,"Volte_OpenMkt-Commercial-CMCC",0x05012011,201706021,''460-00
460-02 460-07 460-08 454-12 454-13 460-04''

OK

<index>           整型。MBN 文件标签，表示当前列出的是哪一个已导入的 MBN 文件。
<selected>    整型。指示该 MBN 文件是否被选中。
   0  未选中
   1  已选中
<activate>    整型。指示该 MBN 文件列表是否已激活。
   0  未激活
   1  已激活
<MBN name>   字符串类型。已导入的 MBN 文件的名称。
<MBN_version>   字符串类型。已导入的 MBN 文件的版本。
<MBN_release_date> 字符串类型。已导入的 MBN 文件的发布日期。
<PLMN_list>   字符串类型。所有已导入的 MBN 文件列表中包含的支持的 PLMN
      列表。
