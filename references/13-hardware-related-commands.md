# 13 硬件相关指令 (Hardware Related Commands)

13 硬件相关指令 (Hardware Related Commands)

13.1. AT+QPOWD  关机

该命令用于关闭模组。执行命令后，UE 立即返回 OK。
随后 UE 注销网络。完成后，UE 输出 POWERED DOWN 并进入
关机状态。注销网络的最长时间为 60 秒。在模组的 STATUS 引脚被拉低或输出 URC POWERED DOWN 之前，
UE 不允许关闭电源，
以避免数据丢失。
参数

13.2. AT+CCLK  时钟

该命令用于设置和查询模组的实时时钟（RTC）。当前设置将一直保留，
直到模组与电源完全断开。
AT+QPOWD  关机
测试命令
AT+QPOWD=?
响应
+QPOWD: (list of supported <n>s)

OK
执行命令
AT+QPOWD[=<n>]
响应
OK

POWERED DOWN
最大响应时间 300 ms
特性 /
<n>      整型。关闭模组。
   0 立即关机
1 正常关机

参数
示例
AT+CCLK?        //查询本地时间。
+CCLK: "08/01/04,00:19:43+00"

OK

13.3. AT+CBC  电池电量

该命令返回 MT 的电池充电状态 <bcs> 和电池电量等级 <bcl>。
AT+CCLK  时钟
测试命令
AT+CCLK=?
响应
OK
读取命令
AT+CCLK?
响应
+CCLK: <time>

OK
写入命令
AT+CCLK=<time>
响应
OK

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该命令立即生效。
配置不会被保存。
参考
3GPP TS 27.007

<time> 字符串类型。格式为 "yy/MM/dd,hh:mm:ss±zz"，表示年（后两位）、月、日、时、分、秒及时区（表示本地时间与 GMT 之间的差值，以刻钟为单位；范围：-48 至 +56）。例如，1994 年 5 月 6 日 22:10:00 GMT+2 小时等于 "94/05/06,22:10:00+08"。
<err>       错误代码。更多详情，请参阅第 15.4 章。
AT+CBC  电池电量
测试命令 响应

参数

13.4. AT+QADC  读取 ADC 值

该命令读取 ADC 通道的电压值。
AT+CBC=? +CBC: (range of supported  <bcs>s),(range of supported
<bcl>s),<voltage>

OK
执行命令
AT+CBC
响应
+CBC: <bcs>,<bcl>,<voltage>

OK

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
参考
3GPP TS 27.007

<bcs>  整型。电池充电状态。
0   ME 未在充电
1   ME 正在充电
2   充电已完成
<bcl>  整型。电池电量等级。
   0–100  电池剩余容量百分比为 0–100
<voltage> 电池电压（mV）。
<err>       错误代码。更多详情，请参阅第 15.4 章。
AT+QADC  读取 ADC 值
测试命令
AT+QADC=?
响应
+QADC: (list of supported <port>s)

OK
读取命令
AT+QADC=<port>
响应
+QADC: <status>,<value>

OK

参数

13.5. AT+QSCLK  启用/禁用低功耗模式

该命令用于启用或禁用低功耗模式。当低功耗模式已启用，且 DTR
和 WAKEUP_IN 均被拉高时，模组直接进入睡眠模式。如果低功耗模式已启用，
但 DTR 和 WAKEUP_IN 均被拉低，则只有在 DTR 和 WAKEUP_IN 被拉高之后，
模组才能进入低功耗模式。

最大响应时间 300 ms
特性 /
<port>     整型。ADC 的通道号。
     0    ADC 通道 0
     1    ADC 通道 1
<status>   整型。ADC 值是否读取成功。
   0    失败
     1    成功
<value>    指定 ADC 通道的电压。单位：mV。
AT+QSCLK  启用/禁用低功耗模式
测试命令
AT+QSCLK=?
响应
+QSCLK: (list of supported <n>s)

OK
读取命令
AT+QSCLK?
响应
+QSCLK: <n>

OK
写入命令
AT+QSCLK=<n>
响应
OK
最大响应时间 300 ms
特性 该命令立即生效
配置不会被保存
参考
Quectel

参数

<n>   整型。禁用或启用低功耗模式。
   0  禁用
   1  启用。由 DTR 引脚和 WAKEUP_IN 引脚控制。
