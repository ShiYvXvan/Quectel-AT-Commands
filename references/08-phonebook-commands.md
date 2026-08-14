# 8 电话簿指令 (Phonebook Commands)

8 电话簿指令

8.1. AT+CNUM  订户号码

该命令从 (U)SIM 中获取订户自己的号码。
参数

AT+CNUM  订户号码
测试命令
AT+CNUM=?
响应
OK
执行命令
AT+CNUM
响应
[+CNUM: [<alpha>],<number>,<type>]
[+CNUM: [<alpha>],<number>,<type>]

OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
参考
3GPP 27.007

<alpha> 与 <number> 相关联的可选字母数字字符串。所使用的字符集
 应为通过 AT+CSCS 命令选择的字符集。
<number>  字符串类型的电话号码，格式由 <type> 指定。
<type> 整型格式的地址类型八位组（参见 3GPP TS 24.008）。通常，有以下三种取值：
129     未知类型
       145  国际类型（包含字符 "+"）
                161    国内类型
<err>           错误码。更多详情请参阅第 15.4 章。

8.2. AT+CPBF  查找电话簿条目

该命令从通过 AT+CPBS 选择的当前电话簿存储区中搜索以给定 <findtext> 字符串开头的电话簿条目，并按字母数字顺序返回所有找到的条目。
参数
AT+CPBF  查找电话簿条目
测试命令
AT+CPBF=?
响应
+CPBF: <nlength>,<tlength>

OK
写入命令
AT+CPBF=<findtext>
响应
[+CPBF: <index>,<number>,<type>,<text>]
[…]

OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
最大响应时间 取决于电话簿条目的存储区。
特性 /
参考
3GPP 27.007

<nlength>       整型。指示字段 <number> 的最大长度。
<tlength>       整型。指示字段 <text> 的最大长度。
<findtext> 字符串类型。当前 TE 字符集中由 AT+CSCS 指定的最大长度
为 <tlength> 的字段。
<number>  字符串类型。电话号码，格式由 <type> 指定。
<index>     整型。在电话簿存储区的位置号范围内。
<type>  整型格式的地址类型八位组（参见 3GPP TS 24.008）。通常，有以下三种取值：
129     未知类型
       145  国际类型（包含字符 "+"）
                161    国内类型
<text>          字符串类型字段，最大长度为 <tlength>，使用当前 TE 字符集中由
AT+CSCS 指定的字符集。

8.3. AT+CPBR  读取电话簿条目

该命令从通过 AT+CPBS 选择的当前电话簿存储区中读取位置号范围 <index1>... <index2> 内的电话簿条目。如果省略 <index2>，则只返回位置 <index1>。
参数
<err>           错误码。更多详情请参阅第 15.4 章。
AT+CPBR  读取电话簿条目
测试命令
AT+CPBR=?
响应
+CPBR: (list of supported <index>s),<nlength>,<tlength>

OK
写入命令
AT+CPBR=<index1>[,<index2>]
响应
+CPBR: <index1>,<number>,<type>,<text>
[+CPBR: <index2>,<number>,<type>,<text>
[…]]

OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
最大响应时间 取决于电话簿条目的存储区。
特性 /
参考
3GPP 27.007

<index>  整型。电话簿存储区的位置号。
<nlength>        整型。指示字段 <number> 的最大长度。
<tlength>       整型。指示字段 <text> 的最大长度。
<index1>     整型。要读取的第一个电话簿记录。
<index2>     整型。要读取的最后一个电话簿记录。
<number>  字符串类型。电话号码，格式由 <type> 指定。
<type> 整型格式的地址类型八位组（参见 3GPP TS 24.008）。通常，有以下三种取值：
129     未知类型

8.4. AT+CPBS  选择电话簿存储区

该命令选择电话簿存储区，其他电话簿命令将使用该存储区。读取命令返回当前选定的存储区、已使用位置的数量以及存储区中的位置总数（在制造商支持的情况下）。测试命令返回支持的存储区作为复合值。
       145  国际类型（包含字符 "+"）
                161    国内类型
<text>          字符串类型。当前 TE 字符集中由 AT+CSCS 指定的最大
长度为 <tlength> 的字段。
<err>           错误码。更多详情请参阅第 15.4 章。
AT+CPBS  选择电话簿存储区
测试命令
AT+CPBS=?
响应
+CPBS: (list of supported <storage>s)

OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
读取命令
AT+CPBS?
响应
+CPBS: <storage>,<used>,<total>

OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
写入命令
AT+CPBS=<storage>
响应
OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /

参数

8.5. AT+CPBW  写入电话簿条目

该命令在通过 AT+CPBS 选择的当前电话簿存储区的 <index> 位置写入电话簿条目。也可以删除 <index> 位置的电话簿条目。
参考
3GPP 27.007

<storage> 字符串类型。电话簿存储区。
 "SM" (U)SIM 电话簿
"DC"  ME 已拨电话列表（AT+CPBW 可能不适用于该存储区）
"FD"    (U)SIM 固定拨号电话簿（AT+CPBW 操作需要 PIN2 权限）
"LD"    (U)SIM 最后拨号电话簿（AT+CPBW 可能不适用于该存储区）
"MC" ME 未接（未应答）呼叫列表（AT+CPBW 可能不适用于该
存储区）
"ME"    移动设备电话簿
"RC"    ME 已接电话列表（AT+CPBW 可能不适用于该存储区）
"EN"    (U)SIM（或 ME）紧急号码（AT+CPBW 可能不适用于该
存储区）
"ON" (U)SIM 自有号码（MSISDN）列表
<used>  整型。指示所选存储区中已使用位置的总数。
<total>    整型。指示所选存储区中位置的总数。
<err>       错误码。更多详情请参阅第 15.4 章。
AT+CPBW  写入电话簿条目
测试命令
AT+CPBW=?
响应
+CPBW: (range of supported <index>s),<nlength>,(list of
supported <type>s),<tlength>
OK
或
ERROR

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
写入命令
AT+CPBW=[<index>][,<number>[,<ty
pe>[,<text>]]]
响应
OK
或
ERROR

参数
示例
AT+CSCS="GSM"
OK
AT+CPBW=10,"15021012496",129,"QUECTEL"
OK           //在位置 10 新建一个电话簿条目。
AT+CPBW=10        //删除位置 10 处的条目。
OK
AT+CPBR=10
OK

如果存在与 ME 功能相关的任何错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
参考
3GPP 27.007

<index> 整型。电话簿存储区的位置号。如果未给出 <index>，将使用第一个
空闲条目。如果仅将 <index> 作为唯一参数给出，则删除由
<index> 指定的电话簿条目。
<nlength>      整型。指示字段 <number> 的最大长度。
<tlength>       整型。指示字段 <text> 的最大长度。
<number>  字符串类型的电话号码，格式由 <type> 指定
<type> 整型格式的地址类型八位组（参见 3GPP TS 24.008）。通常，有以下三种取值：
129     未知类型
       145  国际类型（包含字符 "+"）
                161    国内类型
<text>          字符串类型字段，最大长度为 <tlength>，使用当前 TE 字符集中由
AT+CSCS 指定的字符集。
<err>        错误码。更多详情请参阅第 15.4 章。
