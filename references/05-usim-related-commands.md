# 5 (U)SIM 卡相关指令 ((U)SIM Related Commands)

5 (U)SIM 卡相关指令

5.1. AT+CIMI  请求国际移动用户识别码（IMSI）

本指令用于请求国际移动用户识别码（IMSI），以便 TE 识别连接到 MT 的 UICC（GSM 或 USIM）中特定的 SIM 卡或活动应用。
参数
示例
AT+CIMI
460023210226023      //Query IMSI number of (U)SIM which is attached to ME

AT+CIMI  请求国际移动用户识别码（IMSI）
测试命令
AT+CIMI=?
响应
OK
执行命令
AT+CIMI
响应
TA 返回 <IMSI>，用于识别连接到 ME 的特定 (U)SIM 卡。
<IMSI>

OK

如果存在与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性  /
参考
3GPP TS 27.007

<IMSI>  国际移动用户识别码（不带双引号的字符串）
<err>       错误码。更多详情请参阅第 15.4 章。

OK

5.2. AT+CLCK  功能锁

本指令用于锁定、解锁或查询 MT 或网络功能 <fac>。当正在设置或查询网络功能时，本指令可被中止。PF、PN、PU、PP 和 PC 锁的出厂默认密码为 "12341234"。对于写入命令，执行此类操作通常需要 <passwd>。当查询网络业务状态（<mode>=2）时，只有在任何 <class> 下业务均未激活的情况下，才应返回“未激活”情况（<status>=0）的响应行。
参数
AT+CLCK  功能锁
测试命令
AT+CLCK=?
响应
+CLCK: (list of supported <fac>s)

OK
写入命令
AT+CLCK=<fac>,<mode>[,<passwd>[
,<class>]]
响应
如果 <mode> 不等于 2 且命令设置成功：
OK

如果 <mode>=2 且命令设置成功：
+CLCK: <status>[,<class>]
[+CLCK: <status>[,<class>]]
[…]

OK
最大响应时间 5 s
特性  本指令立即生效。
配置将自动保存。
参考
3GPP TS 27.007

<fac>    字符串类型。
   "SC"    (U)SIM 卡（锁定当前选定的卡槽中安装的 SIM/UICC 卡）
     （在 MT 上电及发出此锁定命令时，SIM/UICC 会要求输入密码）。
 "AO"  BAOC（禁止所有去话）（参见 3GPP TS 22.088 第 1 条）。
 "OI"      BOIC（禁止国际去话）（参见 3GPP TS 22.088 第 1 条）。
"OX" BOIC-exHC（除本国以外的国际去话禁止）（参见 3GPP TS 22.088 第 1 条）。

示例
AT+CLCK="SC",2                      //Query the status of (U)SIM card.
+CLCK: 0          //The (U)SIM card is unlocked (OFF).

OK
AT+CLCK="SC",1,"1234"       //Lock (U)SIM card, and the password is 1234.
OK
参见 3GPP TS 22.088 第 1 条）。
"AI" BAIC（禁止所有来话）（参见 3GPP TS 22.088 第 2 条）。
"IR" BIC-Roam（在归属国以外漫游时禁止来话）（参见 3GPP TS 22.088 第 2 条）。
"AB" 所有禁止业务（参见 3GPP TS 22.030）（仅适用于 <mode>=0）。
"AG" 所有去话禁止业务（参见 3GPP TS 22.030）（仅适用于 <mode>=0）。
"AC" 所有来话禁止业务（参见 3GPP TS 22.030）（仅适用于 <mode>=0）。
"FD" UICC（GSM 或 USIM）中 SIM 卡或活动应用的固定拨号存储器功能（如果当前会话中尚未进行 PIN2 认证，则需要将 PIN2 作为 <passwd>）。
"PF" 将手机锁定到首次插入的 SIM/UICC 卡（本文档中亦称为 PH-FSIM）（当插入其他 SIM/UICC 卡时，MT 会要求输入密码）。
"PN" 网络个性化（参见 3GPP TS 22.022）
"PU" 网络子集个性化（参见 3GPP TS 22.022）
"PP" 服务提供商个性化（参见 3GPP TS 22.022）
"PC" 企业个性化（参见 3GPP TS 22.022）
<mode>   整型。网络业务的状态。
   0  解锁
    1  锁定
   2  查询状态
<passwd>  字符串类型。密码。
<class>   整型。
   1     语音
    2   数据
       4     传真
   7  除 SMS 外的所有电话业务
    8     短消息业务
    16    数据电路同步
    32   数据电路异步
<status> 整型。
   0     关闭
       1  开启

AT+CLCK="SC",2                      //Query the status of (U)SIM card.
+CLCK: 1          //The (U)SIM card is locked (ON).

OK
AT+CLCK="SC",0,"1234"       //Unlock (U)SIM card.
OK

5.3. AT+CPIN  输入 PIN 码

本指令用于输入密码，或查询模组在操作前是否需要输入密码。该密码可以是 (U)SIM PIN、(U)SIM PUK、PH-SIM PIN 等。

读取命令返回一个字母数字字符串，指示是否需要输入某种密码。

TA 存储一个密码，如 (U)SIM PIN、(U)SIM PUK 等，该密码是 TA 操作前所必需的。如果 PIN 需要输入两次，TA 会自动重复该 PIN。如果没有待处理的 PIN 请求，则不执行任何操作，并向 TE 返回错误消息 +CME ERROR。

如果所需 PIN 为 (U)SIM PUK 或 (U)SIM PUK2，则需要输入第二个 PIN。该第二个 PIN <new_pin> 用于替换 (U)SIM 中的旧 PIN。
参数
AT+CPIN  输入 PIN 码
测试命令
AT+CPIN=?
响应
OK
读取命令
AT+CPIN?
响应
+CPIN: <code>

OK
写入命令
AT+CPIN=<pin>[,<new_pin>]
响应
OK
最大响应时间 5 s
特性  本指令立即生效。
配置将自动保存。
参考
3GPP TS 27.007

<code>    不带双引号的字符串。模组所需的密码。
     READY              MT 不等待任何密码

示例
//Enter PIN.
AT+CPIN?
+CPIN: SIM PIN       //Queried PIN code is locked.

OK
AT+CPIN=1234       //Enter PIN.
OK

+CPIN: READY
AT+CPIN?        //PIN has already been entered.
+CPIN: READY

OK
//Enter PUK and PIN.
AT+CPIN?
+CPIN: SIM PUK       //Queried PUK code is locked.

K
AT+CPIN="26601934","1234"    //Enter PUK and new PIN password.
  SIM PIN        MT 正在等待输入 SIM PIN
SIM PUK        MT 正在等待输入 SIM PUK
SIM PIN2     MT 正在等待输入 SIM PIN2
SIM PUK2      MT 正在等待输入 SIM PUK2
PH-NET PIN      MT 正在等待输入网络个性化密码
PH-NET PUK       MT 正在等待输入网络个性化解锁密码
PH-NETSUB PIN     MT 正在等待输入网络子集个性化密码
PH-NETSUB PUK    MT 正在等待输入网络子集个性化解锁密码
PH-SP PIN MT 正在等待输入服务提供商个性化密码
PH-SP PUK MT 正在等待输入服务提供商个性化解锁密码
PH-CORP PIN  MT 正在等待输入企业个性化密码
PH-CORP PUK  MT 正在等待输入企业个性化解锁密码
<pin> 字符串类型。密码。如果请求的密码是 PUK，如 (U)SIM PUK1、PH-FSIM PUK 或其他密码，则 <pin> 后面必须跟 <new_pin>。
<new_pin>   字符串类型。如果请求的代码是 PUK，则需要的新密码。

OK

CPIN: READY
AT+CPIN?
+CPIN: READY       //PUK has already been entered.

OK

5.4. AT+CPWD  修改密码

本指令用于为 AT+CLCK 定义的功能锁功能设置新密码。

本测试命令返回一个列表，其中的成对数据表示可用的功能及其密码的最大长度。
参数
AT+CPWD  修改密码
测试命令
AT+CPWD=?
响应
+CPWD: ("AB",4),("AC",4),("AG",4),("AI",4),("AO",4),("IR
",4),("OI",4),("OX",4),("SC",8),("P2",8)

OK
写入命令
AT+CPWD=<fac>,<oldpwd>,<newpw
d>
响应
OK
最大响应时间 5 s
特性  本指令立即生效。
配置将自动保存。
参考
3GPP TS 27.007

<fac>         字符串类型。功能锁
     "SC"    (U)SIM 卡（锁定 SIM/UICC 卡）（在 MT 上电及发出此锁定命令时，SIM/UICC 会要求输入密码）
"AO"   BAOC（禁止所有去话，参见 3GPP TS 22.088 第 1 条）
   "OI"   BOIC（禁止国际去话，参见 3GPP TS 22.088 第 1 条）
"OX" BOIC-exHC（除本国以外的国际去话禁止，参见 3GPP TS 22.088 第 1 条）
"AI"  BAIC（禁止所有来话，参见 3GPP TS 22.088 第 2 条）
"IR" BIC-Roam（在归属国以外漫游时禁止来话，参见 3GPP TS 22.088 第 2 条）

示例
AT+CPIN?
+CPIN: READY

OK
AT+CPWD="SC","1234","4321"   //Change (U)SIM card password to "4321".
OK
//Restart the module or re-activate the SIM card.
AT+CPIN?        //Query PIN code is locked.
+CPIN: SIM PIN

OK
AT+CPIN="4321"      //PIN must be entered to define a new password "4321".
OK

+CPIN: READY

5.5. AT+CSIM  通用 (U)SIM 访问

本指令允许 TE 上的远端应用直接控制当前选定的卡槽中安装的 (U)SIM 卡。TE 应在 GSM/UMTS 规定的框架内处理 (U)SIM 信息。
参见 3GPP TS 22.088 第 2 条）
"AB"  所有禁止业务（参见 3GPP TS 22.030，仅适用于 <mode>=0）
"AG" 所有去话禁止业务（参见 3GPP TS 22.030，仅适用于 <mode>=0）
"AC"  所有来话禁止业务（参见 3GPP TS 22.030，仅适用于 <mode>=0）
              "P2"   (U)SIM PIN2
<pwdlength> 整型。密码的最大长度。
<oldpwd>  字符串类型。通过用户界面或命令为功能指定的密码。
<newpwd>  字符串类型。新密码
AT+CSIM  通用 (U)SIM 访问
测试命令
AT+CSIM=?
响应
OK
写入命令
AT+CSIM=<length>,<command>
响应
+CSIM: <length>,<response>

参数

5.6. AT+CRSM  受限 (U)SIM 访问

本指令提供对 (U)SIM 数据库简单且有限的访问。它将 (U)SIM 命令编号 <command> 及其所需参数传输给 MT。
OK
或者
ERROR

如果存在与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性  本指令立即生效。
配置将自动保存。
参考
3GPP TS 27.007

<length>  整型。<command> 或 <response> 字符串的长度。
<command>  MT 按照 3GPP TS 51.011 所述的格式传输给 (U)SIM 的命令。
<response> (U)SIM 按照 3GPP TS 51.011 所述的格式传输给 MT 的命令响应。
<err>      错误码。更多详情请参阅第 15.4 章。
AT+CRSM  受限 (U)SIM 访问
测试命令
AT+CRSM=?
响应
OK
写入命令
AT+CRSM=<command>[,<fileld>[,<P1
>,<P2>,<P3>[,<data>][,<pathld>]]]
响应
+CRSM: <sw1>,<sw2>[,<response>]

OK
或者
ERROR

如果存在与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms

参数

特性  本指令立即生效。
配置将自动保存。
参考
3GPP TS 27.007

<command>          整型。(U)SIM 命令编号。
            176       READ BINARY
 178       READ RECORD
 192       GET RESPONSE
 214       UPDATE BINARY
 220       UPDATE REC ORD
 242       STATUS
<fileId>               整型。(U)SIM 上基本数据文件的标识符，如果 <command> 使用的话。
<P1>, <P2>, <P3>    整型。由 MT 传输给 (U)SIM 的参数。除 GET RESPONSE 和 STATUS 外，这些参数对每个命令都是必需的。其值在 3GPP TS 51.011 中描述。
<data>              应写入 (U)SIM 的信息（十六进制字符格式；
参见 AT+CSCS）。
<pathId>                以十六进制格式表示的 SIM/UICC 上基本文件的目录路径。
<sw1>, <sw2>       整型。来自 (U)SIM 的关于实际命令执行情况的信息。无论命令执行成功还是失败，这些参数都会传递给 TE。
<response>            先前发出的命令成功完成的响应（十六进制字符格式；参见 AT+CSCS）。STATUS 和 GET
RESPONSE 返回的数据给出了当前基本数据文件的信息。该信息包括文件类型及其大小
（参见 3GPP TS 51.011）。在 READ BINARY、READ RECORD 或
RETRIEVE DATA 命令之后，将返回所请求的数据。
在执行成功的 UPDATE BINARY、UPDATE RECORD 或 SET DATA 命令后，不返回 <response>。
<err>    错误码。更多详情请参阅第 15.4 章。

5.7. AT+QCCID  显示 ICCID

本指令返回 (U)SIM 卡的 ICCID（集成电路卡识别码）号码。
参数
示例
AT+QCCID        //Query ICCID of the (U)SIM card.
+QCCID: 89860025128306012474

OK

5.8. AT+QPINC  显示 PIN 剩余次数计数器

本指令用于查询 (U)SIM PIN/PUK 密码剩余的可输入次数。
AT+QCCID  显示 ICCID
测试命令
AT+QCCID=?
响应
OK
执行命令
AT+QCCID
响应
+QCCID: <ICCID>

OK
或者
ERROR
最大响应时间 300 ms
特性 /
<ICCID>  不带双引号的字符串。(U)SIM 卡的 ICCID（集成电路卡识别码）号码。
AT+QPINC  显示 PIN 剩余次数计数器
测试命令
AT+QPINC=?
响应
+QPINC: (list of supported <facility>s)

OK
读取命令
AT+QPINC?
响应
+QPINC: "SC",<PIN_counter>,<PUK_counter>

参数

5.9. AT+QINISTAT  查询 (U)SIM 卡初始化状态

本指令用于查询 (U)SIM 卡的初始化状态。
+QPINC: "P2",<PIN_counter>,<PUK_counter>

OK
写入命令
AT+QPINC=<facility>
响应
+QPINC: <facility>,<PIN_counter>,<PUK_counter>

OK
或者
ERROR

如果存在与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
<facility>      字符串类型。
     "SC"    (U)SIM PIN
                  "P2"    (U)SIM PIN2
<PIN_counter>   整型。PIN 密码剩余的可输入次数。最大值为 3。
<PUK_counter>   整型。PUK 密码剩余的可输入次数。最大值为 10。
<err>              错误码。更多详情请参阅第 15.4 章。
AT+QINISTAT  查询 (U)SIM 卡初始化状态
测试命令
AT+QINISTAT=?
响应
+QINISTAT: (range of supported <status>s)

OK
执行命令
AT+QINISTAT
响应
+QINISTAT: <status>

OK
最大响应时间 300 ms

参数

5.10. AT+QSIMDET  (U)SIM 卡检测

本指令用于启用 (U)SIM 卡热插拔功能。(U)SIM 卡通过 GPIO 中断进行检测。同时还应设置插入 (U)SIM 卡时的 (U)SIM 卡检测引脚电平。
参数
特性 /
<status> 整型。(U)SIM 卡的初始化状态。实际值是以下四种类型中若干项之和（例如 7 = 1 + 2 + 4 表示 CPIN READY 和 SMS DONE 和 PB DONE）。
默认值：7。
            0    初始状态
1    CPIN READY。允许进行锁定/解锁 PIN 等操作
2    SMS 初始化完成
4    电话簿初始化完成
AT+QSIMDET  (U)SIM 卡检测
测试命令
AT+QSIMDET=?
响应
+QSIMDET: (list of supported <enable>s),(list of supported
<insert_level>s)

OK
读取命令
AT+QSIMDET?
响应
+QSIMDET: <enable>,<insert_level>

OK
写入命令
AT+QSIMDET=<enable>,<insert_level
>
响应
OK
或者
ERROR
最大响应时间 300 ms
特性 本指令在模组重新启动后生效。
配置将自动保存。
<enable>         整型。启用或禁用 (U)SIM 卡检测。
0   禁用

1. 如果 <insert_level> 的配置值与硬件设计中的不一致，则热插拔功能无效。
2. 热插拔功能在模组重新启动后生效。
示例
AT+QSIMDET=1,0           //Set (U)SIM card detection pin level as low when (U)SIM card is inserted.
OK
<Remove (U)SIM card>
+CPIN: NOT READY
<Insert (U)SIM card>
+CPIN: READY              //If PIN1 of (U)SIM card is unlocked.

5.11. AT+QSIMSTAT  (U)SIM 卡插入状态上报

本指令用于查询 (U)SIM 卡插入状态，或决定是否上报 (U)SIM 卡插入状态。
1   启用
<insert_level>  整型。插入 (U)SIM 卡时 (U)SIM 检测引脚的电平。
0   低电平
1   高电平
AT+QSIMSTAT  (U)SIM 卡插入状态上报
测试命令
AT+QSIMSTAT=?
响应
+QSIMSTAT: (list of supported <enable>s)

OK
读取命令
AT+QSIMSTAT?
响应
+QSIMSTAT: <enable>,<inserted_status>

OK
写入命令
AT+QSIMSTAT=<enable>
响应
OK
或者
ERROR
最大响应时间 300 ms
特性 本指令立即生效。
配置将自动保存。
注意事项

参数
示例
AT+QSIMSTAT?               //Query (U)SIM card insertion status.
+QSIMSTAT: 0,1

K
AT+QSIMDET=1,0
K
AT+QSIMSTAT=1              //Enable (U)SIM card insertion status report.
K
AT+QSIMSTAT?
+QSIMSTAT: 1,1

OK
<Remove (U)SIM card>
+QSIMSTAT : 1,0              //Report of (U)SIM card insertion status: removed.

CPIN: NOT READY
AT+QSIMSTAT?
+QSIMSTAT: 1,0

OK
<Insert (U)SIM card>
+QSIMSTAT: 1,1              //Report of (U)SIM card insertion status: inserted.

+CPIN: READY

<enable> 整型。启用或禁用 (U)SIM 卡插入状态上报。如果启用，则当 (U)SIM 卡被拔出或插入时，将上报 URC +QSIMSTAT:
<enable>,<inserted_status>。
0   禁用
1   启用
<inserted_status> 整型。(U)SIM 卡是否被插入或拔出。此参数不允许设置。
 0  已拔出
 1  已插入
 2  未知，(U)SIM 初始化之前

5.12. AT+QSIMVOL  固定 (U)SIM 卡供电电压

本指令用于固定 (U)SIM 卡的供电电压。对于常见的 UICC，(U)SIM 卡的供电电压通常为 1.8V 或 3.0V。
参数
示例
AT+QSIMVOL=?
+QSIMVOL: (0-2)

OK
AT+QSIMVOL?
+QSIMVOL: 0

OK
AT+QSIMVOL=1
OK
AT+QSIMVOL?
AT+QSIMVOL  固定 (U)SIM 卡供电电压
测试命令
AT+QSIMVOL=?
响应
+QSIMVOL: (range of supported <mode>s)

OK
读取命令
AT+QSIMVOL?
响应
+QSIMVOL: <mode>

OK
写入命令
AT+QSIMVOL=<mode>
响应
OK
或者
ERROR
最大响应时间 300 ms
特性 本指令在模组重新启动后生效。
配置将自动保存。
<mode>      整型。(U)SIM 卡供电电压的模式。
0    不固定 (U)SIM 卡的供电电压
1    固定 (U)SIM 卡的供电电压为 1.8 V
2    固定 (U)SIM 卡的供电电压为 3.0 V

+QSIMVOL: 1

OK
AT+QSIMVOL=2
OK
AT+QSIMVOL?
+QSIMVOL: 2

OK

5.13. AT+CCHO  打开逻辑通道

本指令用于打开 (U)SIM 卡的逻辑通道。
参数

逻辑通道号包含在 APDU 命令的 CLASS 字节中，因此隐式包含在发送到 UICC 的所有 APDU 命令中。在这种情况下，将由 MT 管理 APDU CLASS 字节中的逻辑通道部分，并确保所选择的逻辑通道与 AT 命令中指示的 <sessionID> 相关。有关逻辑通道的更多信息，请参见 3GPP TS 31.101 [65]。
AT+CCHO  打开逻辑通道
测试命令
AT+CCHO=?
响应
OK
写入命令
AT+CCHO=<dfname>
响应
<sessionID>

OK
或者
ERROR
最大响应时间 300 ms
特性 本指令立即生效。
配置不会被保存。
<dfname> 字符串类型。UICC 中的所有选定应用通过以 1 至 16 个字节编码的 DF 名称引用。
<sessionID> 整型。会话 ID，用于通过逻辑通道机制定位智能卡上的特定应用。
注意

APDU 命令协议中的逻辑通道。
示例
AT+CCHO=?                   //Test command.
OK
AT+CCHO="A0000000871002FF86FFFF89FFFFFFFF" //<dfname> is made up of AID strings.
+CCHO: 1                //The session ID is 1.

OK

5.14. AT+CGLA  UICC 逻辑通道访问

本指令用于访问 UICC 逻辑通道。
参数
AT+CGLA  UICC 逻辑通道访问
测试命令
AT+CGLA=?
响应
OK
写入命令
AT+CGLA=<sessionID>,<length>,
<command>
响应
+CGLA: <length>,<response>

OK
或者
ERROR
最大响应时间 300 ms
特性 本指令立即生效。
配置不会被保存。
<sessionID>        整型。这是用于向 UICC 发送 APDU 命令的会话标识符。当使用除默认通道（通道 "0"）以外的逻辑通道来定位智能卡上的应用时，必须向 UICC 发送命令。
<length>           整型。在 <command> 或 <response> 中发送给 TE 的字符长度（为命令或响应实际长度的两倍）。
<command>        MT 按照 3GPP TS 31.101 [65] 所述的格式传递给 UICC 的命令（十六进制字符格式；参见 +cscs）
<response>         UICC 按照 3GPP TS 31.101 [65] 所述的格式传递给 MT 的命令响应（十六进制字符格式；参见 +cscs）。

示例
AT+CGLA=?             //Test command.
OK
AT+CGLA=1,14,"00A40804022F00"   //The command is 00A40804022F00.
+CGLA: 4,"6121"           //The length is 4, the response is 6121.

OK

5.15. AT+CCHC  关闭逻辑通道

本指令用于关闭具有给定 <sessionID> 的 (U)SIM 卡逻辑通道。
参数
示例
AT+CCHC=?         //Test command.
OK
AT+CCHC=1         //Close logical channel: 1.
OK
AT+CCHC  关闭逻辑通道
测试命令
AT+CCHC=?
响应
OK
写入命令
AT+CCHC=<sessionID>
响应
OK
或者
ERROR
最大响应时间 300 ms
特性 本指令立即生效。
配置不会被保存。
<sessionID>      整型。会话 ID，用于通过逻辑通道机制定位智能卡上的特定应用。
