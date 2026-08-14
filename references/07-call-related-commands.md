# 7 通话相关指令 (Call Related Commands)

7 通话相关指令

7.1. ATA  接听来电

该命令用于使模组接通由 RING URC 指示的语音或数据来电。

1. 同一命令行上的任何其他指令均被忽略。
2. 在执行过程中收到一个字符通常可中止该命令。但在某些连接建立状态（如握手）期间无法中止。
3. 另请参阅第 2.21 章中的 ATX。

ATA  接听来电
执行命令
ATA
响应
TA 向远端站点发送摘机信号。
数据呼叫成功连接时的响应：
CONNECT <text>
TA 随之切换到数据模式。
注：仅当 ATX <value> 参数设置中的 <value> 大于 0 时，<text> 才会输出。
呼叫释放后 TA 返回命令模式时：
OK

语音呼叫成功连接时的响应：
OK

未连接时的响应：
NO CARRIER
最大响应时间 90 s，由网络决定。
特性 /
参考
V.25ter

注释

示例
RING  //语音呼叫正在响铃
AT+CLCC
+CLCC: 1,0,0,1,0,"",128                  //LTE 模式下的 PS 呼叫
+CLCC: 2,1,4,0,0,"02154450290",129      //来电

OK
ATA          //使用 ATA 接听语音呼叫
OK

7.2. ATD  主叫拨号 (Mobile Originated Call to Dial a Number)

该命令用于建立语音和数据呼出。也可以通过该命令控制补充业务。
ATD  主叫拨号 (Mobile Originated Call to Dial a Number)
执行命令
ATD<n>[<mgsm>][;]
响应
若没有拨号音且参数设置为 ATX2 或 ATX4：
NO DIALTONE

若占线（且参数设置为 ATX3 或 ATX4）：
BUSY

若无法建立连接：
NO CARRIER

若连接成功且为非语音呼叫：
CONNECT <text>
TA 随之切换到数据模式。
注：仅当 ATX<value> 参数设置中的 <value> 大于 0 时，<text> 才会输出。
呼叫释放后 TA 返回命令模式时：
OK

若连接成功且为语音呼叫：
OK
最大响应时间 5 s，由网络决定（AT+COLP=0）。
特性 /
参考
V.25ter

参数

1. 在执行过程中收到 ATH 命令或一个字符通常可中止该命令。但在某些连接建立状态（如握手）期间无法中止。
2. 仅当拨号字符串中没有 "*" 或 "#" 代码时，参数 "I" 和 "i" 才可以省略。
3. 有关结果码和呼叫监测参数的设置，请参阅 ATX 命令。
4. 使用 ATD 拨号后返回的响应
   对于语音呼叫，可以确定两种不同的响应模式。TA 在拨号完成后或呼叫建立后立即返回 OK。该设置由 AT+COLP 控制。出厂默认为 AT+COLP=0，即 TA 在拨号完成后立即返回 OK。否则 TA 将返回 OK、BUSY、NO DIAL TONE 或 NO CARRIER。
5. 在激活的语音通话期间使用 ATD：
   ⚫ 当用户在当前已有激活语音通话时发起第二个语音呼叫，第一个呼叫将自动被置于保持状态。
   ⚫ 任何时刻都可以使用 AT+CLCC 命令轻松查看所有呼叫的当前状态。
示例
ATD10086;        //拨打对方号码。
OK

<n>   拨号数字串及可选的 V.25ter 修饰符
   拨号数字：0-9, * , #, +, A, B, C
      以下 V.25ter 修饰符被忽略：,(逗号), T, P, !, W, @
<mgsm>  GSM 修饰符字符串：
     I  激活 CLIR（禁止向被叫方显示本机号码）
            i     停用 CLIR（允许向被叫方显示本机号码）
    G   仅对本呼叫激活闭合用户群呼叫
           g     仅对本呼叫停用闭合用户群呼叫
<;>     仅用于建立语音呼叫时，返回命令模式
注释

7.3. ATH  断开现有连接

该命令用于断开电路交换数据呼叫或语音呼叫。AT+CHUP 也用于断开语音呼叫。
参数

7.4. AT+CVHU  语音挂断控制 (Voice Hang up Control)

该命令控制是否可以使用 ATH 断开语音呼叫。
ATH  断开现有连接
执行命令
ATH[n]
响应
从命令行本地断开现有呼叫并终止该呼叫。
OK
最大响应时间 90 s，由网络决定。
特性 /
参考
V.25ter

<n>   整型。
0  从命令行断开现有呼叫并终止该呼叫
AT+CVHU  语音挂断控制 (Voice Hang up Control)
测试命令
AT+CVHU=?
响应
+CVHU: (list of supported <mode>s)

OK
读取命令
AT+CVHU?
响应
+CVHU: <mode>

OK
写入命令
AT+CVHU=<mode>

响应
OK
或
ERROR
最大响应时间 300 ms

参数

7.5. AT+CHUP  挂断语音呼叫 (Hang up Voice Call)

该命令用于取消处于 Active（激活）、Waiting（等待）和 Held（保持）状态的所有语音呼叫。对于数据连接，请使用 ATH。
示例
RING                                 //来电。

AT+CHUP                            //挂断该呼叫。
OK

特性 /
参考
3GPP TS 27.007

<mode>        整型。
0  可以使用 ATH 断开语音呼叫。
                1  ATH 被忽略，但返回 OK 响应。
AT+CHUP  挂断语音呼叫 (Hang up Voice Call)
测试命令
AT+CHUP=?
响应
OK
执行命令
AT+CHUP

响应
OK
或
ERROR
最大响应时间 90 s，由网络决定。
特性 /
参考
3GPP 27.007

7.6. +++  从数据模式切换到命令模式

该命令仅在 TA 处于数据模式时可用。"+++" 字符序列使 TA 取消 AT 接口上的数据流并切换到命令模式。这允许在保持与远端服务器（或相应的 GPRS 连接）的数据连接的同时输入 AT 命令。

1. 为防止 +++ 转义序列被误认为数据，应遵循以下顺序：
   ⚫ 在输入 +++ 之前的 1 秒内不要输入任何字符。
   ⚫ 在 1 秒内输入 +++，且在此期间不能输入任何其他字符。
   ⚫ 在输入 +++ 之后的 1 秒内不要输入任何字符。
   ⚫ 成功切换到命令模式；否则返回到步骤 1。
2. 要从命令模式返回数据模式，请输入 ATO。
3. 另一种切换到命令模式的方法是通过 DTR 电平变化，详情请参阅 AT&D 命令。

7.7. ATO  从命令模式切换到数据模式

该命令恢复连接并从命令模式切换回数据模式。
+++  从数据模式切换到命令模式
执行命令
+++
响应
OK
最大响应时间 300 ms
特性 /
参考
V.25ter

ATO  从命令模式切换到数据模式
执行命令
ATO[n]
响应
如果连接未能成功恢复：
NO CARRIER

如果连接成功恢复，TA 从命令模式返回数据模式：
CONNECT <text>
注释

参数

当 TA 从命令模式成功返回数据模式时，会返回 CONNECT <text>。请注意，仅当 ATX<value> 参数设置中的 <value> 大于 0 时，<text> 才会输出。

7.8. ATS0  设置自动应答前的振铃次数

该命令控制来电的自动应答模式。
参数

最大响应时间 300 ms
特性 /
参考
V.25ter

<n>   整型。
0  从命令模式切换到数据模式
ATS0  设置自动应答前的振铃次数
读取命令
ATS0?
响应
<n>

OK
写入命令
ATS0=<n>
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置可通过 AT&W 保存。
参考
V.25ter

<n>   整型。该参数设置决定自动应答前的振铃次数。
0  禁用自动应答
   1–255  在指定的振铃次数后启用自动应答
注

如果 <n> 设置过高，来电方可能在呼叫被自动应答之前挂断。
示例
ATS0=3         //设置振铃三次后自动应答呼叫。
OK

RING         //有来电。

RING

RING            //振铃三次后自动应答呼叫。

7.9. ATS6  设置盲拨前的等待时间

该命令仅为兼容性原因而实现，无实际效果。
参数

ATS6  设置盲拨前的等待时间
读取命令
ATS6?
响应
<n>

OK
写入命令
ATS6=<n>
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置可通过 AT&W 保存。
参考
V.25ter

<n>   整型。
0–2–10  盲拨前等待的秒数
注

7.10. ATS7  设置等待连接完成的等待时间

该命令指定在接听或发起呼叫时等待连接完成的时长（单位：秒）。若在该时间内未建立连接，模组将断开线路连接。
参数

7.11. ATS8  设置逗号拨号修饰符的等待时间

该命令仅为兼容性原因而实现，无实际效果。
ATS7  设置等待连接完成的等待时间
读取命令
ATS7?
响应
<n>

OK
写入命令
ATS7=<n>
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置可通过 AT&W 保存。
参考
V.25ter

<n>  整型。
0       已禁用
1–255  等待连接完成的秒数。单位：秒。
ATS8  设置逗号拨号修饰符的等待时间
读取命令
ATS8?
响应
<n>

OK
写入命令
ATS8=<n>
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置可通过 AT&W 保存。

参数

7.12. ATS10  设置指示数据载波缺失后的断开延迟

该命令决定在数据载波缺失时 UE 保持连接的时长（单位：十分之一秒）。如果在断开前再次检测到数据载波，TA 将保持连接。
参数

参考
V.25ter

<n>  整型。
0  拨号字符串中遇到逗号时无暂停
  1–2–255  逗号拨号修饰符的等待秒数
ATS10  设置指示数据载波缺失后的断开延迟
读取命令
ATS10?
响应
<n>

OK
写入命令
ATS10=<n>
响应
OK
最大响应时间 300 ms
特性 /
参考
V.25ter

<n>    整型。UE 指示接收线路信号缺失后到断开前等待的十分之一秒数。范围：1–15–255。

7.13. ATS12  设置使用 +++ 退出透明接入模式的时间间隔
参数
示例
ATS12
050

OK
ATS12=25
OK

7.14. AT+CBST  选择承载业务类型

该写入命令用于选择发起数据呼叫时要使用的承载业务 <name>、数据速率 <speed> 和连接元素 <ce>。

ATS12  设置使用 +++ 退出透明接入模式的时间间隔
读取命令
ATS12?
响应
<value>

OK
写入命令
ATS12=<value>
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置可通过 AT&W 保存。
参考
V.25ter

<value>  整型。使用 +++ 退出透明接入模式的时间间隔。范围：
   10–250。默认值：50。若设置为 25，表示时间间隔为 0.5 s；若设置为
   50，表示时间间隔为 1 s；若设置为 100，表示时间间隔为 2 s，
   以此类推。

参数
AT+CBST  选择承载业务类型
测试命令
AT+CBST=?
响应
+CBST: (list of supported <speed>s),(list of supported
<name>s),(list of supported <ce>s)

OK
读取命令
AT+CBST?
响应
+CBST: <speed>,<name>,<ce>

OK
写入命令
AT+CBST=[<speed>[,<name>[,<ce>]]
]
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.007

<speed> 整型。
0       自动速率选择
7       9600 bps (V.32)
12      9600 bps (V.34)
14      14400 bps (V.34)
16      28800 bps (V.34)
17      32000 bps (V.34)
39      9600 bps (V.120)
43      14400 bps (V.120)
48      28800 bps (V.120)
51      56000 bps (V.120)
71      9600 bps (V.110)
75      14400 bps (V.110)
80      28800 bps (V.110 或 X.31 标志填充)
81      38400 bps (V.110 或 X.31 标志填充)
83      56000 bps (V.110 或 X.31 标志填充；此设置可配合
异步非透明 UDI 或 RDI 业务使用以获得 FTM)
84      64000 bps (X.31 标志填充；此设置可配合
异步非透明 UDI 业务使用以获得 FTM)
116     64000 bps（比特透明）
134     64000 bps（多媒体）

表 6：AT+CBST 支持的参数配置
<name>  整型。
0  异步调制解调器
         1  同步调制解调器
            4       异步调制解调器 (RDI)
<ce>  整型。
0  透明
   1  非透明
<speed> GSM WCDMA
同步
调制解调器
异步
调制解调器
异步
调制解调器 (RDI)
透明 非透明
0 Y Y N Y N N Y
7 Y N N Y N N Y
12 Y N N Y N N Y
14 Y Y N Y N N Y
16 N Y N Y N N Y
17 N Y N Y N N Y
39 Y N N Y N N Y
43 Y Y N Y N N Y
48 N Y N Y N N Y
51 N Y N Y N N Y
71 Y N N Y N N Y
75 Y Y N Y N N Y
80 Y Y N Y N N Y
81 Y Y N Y N N Y
83 Y Y N Y Y N Y
84 N Y N Y N N Y
116 N Y Y N N Y N
134 N Y Y N N Y N

3GPP TS 22.002 列出了子参数的允许组合。

7.15. AT+CSTA  选择地址类型

该写入命令根据 3GPP 规范为后续拨号命令 ATD 选择号码类型。测试命令返回支持的复合值。
参数

7.16. AT+CLCC  列出 ME 当前呼叫

该执行命令返回所有当前呼叫的列表。如果命令执行成功但不存在呼叫，则不发送信息响应，仅向 TE 发送 OK。
AT+CSTA  选择地址类型
测试命令
AT+CSTA=?
响应
+CSTA: (list of supported <type>s)

OK
读取命令
AT+CSTA?
响应
+CSTA: <type>

OK
写入命令
AT+CSTA=<type>
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.007

<type>  整型。当前地址类型设置。
129      未知类型
   145   国际类型（包含字符 "+"）
注

参数
AT+CLCC  列出 ME 当前呼叫
测试命令
AT+CLCC=?
响应
OK
执行命令
AT+CLCC
响应
[+CLCC :
<id1>,<dir>,<stat>,<mode>,<mpty>[,<number>,<type>[,<
alpha>]]
[+CLCC:
<id2>,<dir>,<stat>,<mode>,<mpty>[,<number>,<type>[,<
alpha>]]
[...]

OK

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
<idx>  整型。呼叫识别号，如 3GPP TS 22.030 子条款 4.5.5.1 所述。
该号码可用于 AT+CHLD 命令操作。
<dir>  整型。
0  移动台主叫（MO）呼叫
   1  移动台被叫（MT）呼叫
<stat>  整型。呼叫状态。
   0  激活（Active）
   1  保持（Held）
   2  拨号中（MO 呼叫）
   3  振铃中（MO 呼叫）
   4  来电（MT 呼叫）
   5  等待中（MT 呼叫）
<mode>  整型。承载/电信业务。
   0  语音
   1  数据
   2  传真
<mpty>  整型。
0  该呼叫不是多方（会议）呼叫的成员
   1  该呼叫是多方（会议）呼叫的成员
<number>   字符串类型的电话号码，格式由 <type> 指定。

示例
ATD10086;        //建立呼叫。
OK
AT+CLCC
+CLCC: 1,0,0,1,0,"",128                     //LTE 模式下的 PS 呼叫。
+CLCC: 2,0,0,0,0,"10086",129       //建立呼叫，且该呼叫已被接听。

OK

7.17. AT+CR  业务报告控制

该命令控制模组在呼叫建立时是否向 TE 发送中间结果码 +CR: <serv>。

若启用，中间结果码将在连接协商中 TA 已确定将使用的业务速率和质量的那个时刻发送，且在任何差错控制或数据压缩报告发送之前，以及在任何最终结果码（如 CONNECT）发送之前。
<type> 整型格式的地址类型八位组（详情请参阅 3GPP TS 24.008 子条款 10.5.4.7）。通常有以下三种取值：
129     未知类型
   145  国际类型（包含字符 "+"）
           161    国内类型
<alpha>    与 <number> 对应的字母数字表示，对应电话簿中找到的条目。
<err>       错误码。更多详情请参阅第 15.4 章。
AT+CR  业务报告控制
测试命令
AT+CR=?
响应
+CR: (list of supported <mode>s)

OK
读取命令
AT+CR?
响应
+CR: <mode>

OK
写入命令
AT+CR=[<mode>]
响应
TA 控制呼叫建立时是否从 TA 向 TE 返回中间结果码
+CR: <serv>。
OK

参数

7.18. AT+CRC  设置来电指示的蜂窝结果码

该命令控制是否使用来电指示的扩展格式。启用后，来电将以非请求结果码 +CRING: <type> 而非正常的 RING 指示给 TE。
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.007

<mode>  整型。
0    禁用
 1    启用
<serv>  ASYNC   异步透明
   SYNC   同步透明
   REL ASYNC  异步非透明
      REL SYNC  同步非透明
            GPRS        GPRS
AT+CRC  设置来电指示的蜂窝结果码
测试命令
AT+CRC=?
响应
+CRC: (list of supported <mode>s)

OK
读取命令
AT+CRC?
响应
+CRC: <mode>

OK
写入命令
AT+CRC=[<mode>]
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.007

参数
示例
AT+CRC=1        //启用扩展格式。
OK

+CRING: VOICE  //向来电向 TE 指示。
ATH
OK
AT+CRC=0        //禁用扩展格式。
OK

RING //向来电向 TE 指示。
ATH
OK

7.19. AT+CRLP  选择无线链路协议参数

该命令用于设置发起非透明数据呼叫时使用的无线链路协议（RLP）参数。
<mode>  整型。
0           禁用扩展格式
 1             启用扩展格式
<type>  ASYNC   异步透明
   SYNC   同步透明
   REL ASYNC  异步非透明
   REL SYNC  同步非透明
   FAX    传真
      VOICE   语音
AT+CRLP  选择无线链路协议参数
测试命令
AT+CRLP=?
响应
+CRLP: (range of supported <iws>s),(range of supported
 <mws>s),(range of supported <T1>s),(range of supported
<N2>s),<ver>
+CRLP: (range of supported <iws>s),(range of supported
<mws>s),(range of supported <T1>s),(range of supported
<N2>s),<ver>
+CRLP: (range of supported <iws>s),(range of supported
<mws>s),(range of supported <T1>s),(range of supported

参数

7.20. AT+QECCNUM  配置紧急呼叫号码

该命令用于查询、添加和删除 ECC（紧急呼叫码）号码。ECC 号码有两种：(U)SIM 之外的 ECC 号码和 (U)SIM 内的 ECC 号码。(U)SIM 之外的默认 ECC 号码为 911, 112, 00, 08, 110, 999, 118 和 119。(U)SIM 内的默认 ECC 号码为 911 和 112。911 和 112 始终作为 ECC 号码受到支持，且无法删除。ECC 号码可自动保存到 NVM。如果 (U)SIM 卡包含 ECC 文件，则该文件中的号码也可以
<N2>s),<ver>

OK
读取命令
AT+CRLP?
响应
+CRLP: <iws>,<mws>,<T1>,<N2>,<ver>
+CRLP: <iws>,<mws>,<T1>,<N2>,<ver>
+CRLP: <iws>,<mws>,<T1>,<N2>,<ver>

OK
写入命令
AT+CRLP=[<iws>[,<mws>[,<T1>[,<N2
>[,<ver>]]]]]
响应
OK
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS27.007

<iws>  整型。互通窗口大小（IWF 到 MS 的窗口大小）。
0–61   互通窗口大小
           0–240–488    适用于 <ver>=2
<mws>  整型。移动台窗口大小（MS 到 IWF 的窗口大小）。
0–61   移动台窗口大小
           0–240–488    适用于 <ver>=2
<T1>  整型。
38–48–255  确认定时器 T1，单位为 10 ms
           42–52–255    适用于 <ver>=2
<N2>  整型。
1–6–255  重传尝试次数 N2
<ver>    整型。RLP 版本号。
0–2     RLP 版本号

被视为 ECC 号码。

每种类型的最大支持 ECC 号码数量为 20。
参数
<mode>             整型。ECC 号码操作。
0 查询 ECC 号码
1 添加 ECC 号码
2 删除 ECC 号码
<type>          整型。ECC 号码类型。
0 (U)SIM 之外的 ECC 号码
1 (U)SIM 内的 ECC 号码
<eccnum>      字符串类型。ECC 号码（例如 110, 119）。
AT+QECCNUM  配置紧急呼叫号码
测试命令
AT+QECCNUM=?
响应
+QECCNUM: (range of supported <mode>s)

OK
写入命令
AT+QECCNUM=<mode>,<type>[,<ec
cnum1>[,<eccnum2>,…[,<eccnumN>
]]]
响应
若 <mode> 等于 0，则查询 ECC 号码。此时
应省略 <eccnumN>：
+QECCNUM: <type>,<eccnum1>,<eccnum2>[…]

OK

若 <mode> 不等于 0：<mode>=1 用于添加
ECC 号码；<mode>=2 用于删除 ECC 号码。
此时，至少应输入一个 ECC 号码 <eccnumN>，响应为：
OK
或
ERROR
读取命令
AT+QECCNUM?
响应
+QECCNUM: 0,<eccnum1>,<eccnum2>[…]
+QECCNUM: 1,<eccnum1>,<eccnum2>[…]

OK
最大响应时间 300 ms
特性 该命令立即生效。
配置会自动保存。

示例
AT+QECCNUM=?              //查询支持的 ECC 号码操作模式。
+QECCNUM: (0-2)

OK
AT+QECCNUM?                 //查询有或没有 (U)SIM 的 ECC 号码。
+QECCNUM: 0,"911","112","00","08","110","999","118","119"
+QECCNUM: 1,"911","112"

OK
AT+QECCNUM=0,1              //查询 (U)SIM 内的 ECC 号码。
+QECCNUM: 1,"911","112"

OK
AT+QECCNUM=1,1,"110", "234"  //将 "110" 和 "234" 添加到 (U)SIM 内的 ECC 号码类型中。
OK
AT+QECCNUM=0,1              //查询 (U)SIM 内的 ECC 号码。
+QECCNUM: 1, "911","112","110","234"

OK
AT+QECCNUM=2,1,"110"         //从 (U)SIM 内的 ECC 号码类型中删除 "110"。
OK
AT+QECCNUM=0,1              //查询 (U)SIM 内的 ECC 号码。
+QECCNUM: 1, "911","112","234"

OK

7.21. AT+QHUP  以特定释放原因挂断呼叫

该命令可以以主机指定的特定 3GPP TS 24.008 释放原因终止一个或多个呼叫（包括语音呼叫和数据呼叫）。
AT+QHUP  以特定释放原因挂断呼叫
测试命令
AT+QHUP=?
响应
OK
写入命令
AT+QHUP=<cause>[,<idx>]
响应
OK
或
ERROR

如果存在与 ME 功能相关的任何错误：

参数
示例
AT+QHUP=?         //测试命令。
OK
ATD10010;             //拨打 10010。
OK
ATD10086;             //拨打 10086。
OK
AT+CLCC              //查询呼叫状态。
+CLCC: 1,0,1,0,0,"10010",129
+CLCC: 2,0,0,0,0,"10086",129

OK
AT+QHUP=17,1         //终止 ID 为 1 的呼叫。释放原因为 "user busy"（用户忙）。
OK
AT+CLCC              //查询呼叫状态。
+CLCC: 1,0,0,0,0,"10086",129
+CME ERROR: <err>
最大响应时间 90 s，由网络决定。
特性 /
<cause> 整型。释放原因。要向网络指示的 3GPP TS 24.008 释放原因。
1            释放原因 "unassigned (unallocated) number"（未分配（未分配）号码）
                16           释放原因 "normal call clearing"（正常呼叫清除）
                17           释放原因 "user busy"（用户忙）
                18           释放原因 "no user responding"（无用户应答）
                21           释放原因 "call rejected"（呼叫被拒绝）
                27           释放原因 "destination out of order"（目的地故障）
                31           释放原因 "normal, unspecified"（正常，未指明）
                88           释放原因 "incompatible destination"（目的地不兼容）
<idx>  整型。呼叫识别号是 AT+CLCC 指示的当前呼叫列表中的一个可选索引。AT+QHUP 将终止由给定呼叫号识别的呼叫。默认呼叫号 0 不分配给任何呼叫，但表示所有呼叫。
                0            终止所有已知呼叫。但是，如果同时存在电路交换数据呼叫和
语音呼叫，该命令仅终止 CSD 呼叫。
                1…7         终止具有指定识别号的特定呼叫。
<err>           错误码。更多详情请参阅第 15.4 章。

OK
AT+QHUP=16           //终止所有已存在的呼叫。释放原因为 "normal call clearing"（正常呼叫清除）。
OK
AT+CLCC
OK

7.22. AT+QCHLDIPMPTY  挂断 VoLTE 会议中的呼叫

该命令用于挂断 VoLTE 会议中的呼叫。
参数
示例
AT+QCHLDIPMPTY=?            //测试命令。
+QCHLDIPMPTY: <number>

OK
ATD13866783782;                //建立呼叫。
OK
AT+CLCC
+CLCC: 2,1,0,1,0,"",128
+CLCC: 1,0,0,0,0,"13866783782",129   //第二个呼叫为激活状态。

AT+QCHLDIPMPTY  挂断 VoLTE 会议中的呼叫
测试命令
AT+QCHLDIPMPTY=?
响应
+QCHLDIPMPTY: <number>

OK
写入命令
AT+QCHLDIPMPTY=<number>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 /
<number>  拨号数字串及可选的 V.25ter 修饰符。
    拨号数字：0-9, *, #, +, A, B, C

OK
AT+CHLD=2    //将激活呼叫置于保持状态，并接受等待呼叫作为激活呼叫。
OK
AT+CLCC                              //查询呼叫状态。
+CLCC: 2,1,0,1,0,"",128
+CLCC: 1,0,1,0,0,"13866783782",129     //第二个呼叫处于保持状态。

OK
ATD15155196746;                       //建立呼叫。
OK
AT+CLCC
+CLCC: 2,1,0,1,0,"",128
+CLCC: 1,0,1,0,0,"13866783782",129     //第二个呼叫处于保持状态。
+CLCC: 3,1,0,1,0,"",128
+CLCC: 4,0,0,0,0,"15155196746",129     //第四个呼叫为激活状态。

OK
AT+CHLD=3   //将一个保持呼叫添加到激活呼叫中，以建立会议（多方）呼叫。
OK
AT+CLCC
+CLCC: 2,1,0,1,0,"",128
+CLCC: 3,1,0,1,0,"",128
+CLCC: 5,0,0,0,0,"sip:mmtel",128

OK
AT+QCHLDIPMPTY="13866783782"       //挂断一个已激活的呼叫。
OK
AT+QCHLDIPMPTY="15155196746"      //挂断一个已激活的呼叫。
OK

7.23. AT^DSCI  呼叫状态指示

该命令配置 TA 是否在 TE 处启用 DSCI 的呈现。
AT^DSCI  呼叫状态指示
测试命令
AT^DSCI=?
响应
^DSCI: (list of supported <n>s)

OK
写入命令
AT^DSCI?
响应
^DSCI: <n>

参数

在 TE 处启用 DSCI 的呈现后，操作后返回非请求结果码：
^DSCI: <id>,<dir>,<stat>,<type>,<number>,<num_type>,<tone_info>
参数
<id>   呼叫 ID
<dir>   呼叫方向
<stat>   呼叫状态
 1 CALL_HOLD（呼叫保持）
 2 CALL_ORIGINAL（呼叫发起）
 3 CALL_CONNECT（呼叫连接）
 4 CALL_INCOMING（来电）
 5 CALL_WAITING（呼叫等待）
 6 CALL_END（呼叫结束）
 7 CALL_ALERTING（呼叫振铃）
<type>   呼叫类型
    0 语音呼叫
    1 PS 呼叫
<number>  电话号码
<num_type>  电话号码类型
<tone_info>  主机播放提示音信息
               0 主机播放提示音
               1 主机不播放提示音

<id>, <dir>, <number>, <number_type> 应为 AT+CLCC 中设置的值。

OK
AT^DSCI=<n> OK
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
<n>  整型。
  0 未提供 DSCI
  1 提供 DSCI
注

示例
//拨打电话。
AT^DSCI=1            //启用 DSCI。
OK
ATD10086;             //拨打 10086。
OK

^DSCI: 1,0,2,0,10086,129,0         //呼叫开始。

^DSCI: 1,0,7,0,10086,129,0        //呼叫振铃。

^DSCI: 1,0,3,0,10086,129,0        //呼叫连接。

ATH
OK

^DSCI: 1,0,6,0,10086,129,0        //呼叫结束。

//有来电
RING

^DSCI: 1,1,4,0,13022100000,129,0     //来电。

RING

^DSCI: 1,1,6,0,13022100000,129,0     //呼叫结束。

NO CARRIER
