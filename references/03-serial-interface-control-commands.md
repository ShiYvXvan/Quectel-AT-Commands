# 3 串行接口控制指令 (Serial Interface Control Commands)

3 串行接口控制指令

3.1. AT&C  设置 DCD 功能模式

该命令控制 UE 的 DCD（数据载波检测）线路的行为。
参数

3.2. AT&D  设置 DTR 功能模式

该命令决定在数据模式下，当 DTR 线路由低电平变为高电平时，UE 如何响应。
AT&C  设置 DCD 功能模式
执行命令
AT&C[<value>]
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置可以通过 AT&W 保存。
参考
V.25ter

<value>  整型。它决定电路状态（DCD）与远端接收线路信号检测之间的关系。
   0  DCD 线路始终为 ON
1  DCD 线路仅在存在数据载波时为 ON
AT&D  设置 DTR 功能模式
执行命令
AT&D[<value>]
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。

参数

3.3. AT+IFC  设置 TE-TA 本地数据流控

该命令决定数据模式下串口的流控行为。
参数
该配置可以通过 AT&W 保存。
参考
V.25ter

<value>  整型。
   0  TA 忽略 DTR 状态
   1  DTR 由低到高：保持已连接的通话并切换到命令模式。
2   DTR 由低到高：断开数据通话并切换到命令模式。当 DTR 处于高电平时，自动应答功能被禁用。
AT+IFC  设置 TE-TA 本地数据流控
测试命令
AT+IFC=?
响应
+IFC: (list of supported <dce_by_dte>s),(list of supported
<dte_by_dce>s)

OK
读取命令
AT+IFC?
响应
+IFC: <dce_by_dte>,<dte_by_dce>

OK
写入命令
AT+IFC=<dce_by_dte>,<dte_by_dce>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置可以通过 AT&W 保存。
参考
V.25ter

<dce_by_dte>  整型。指定 TE 在从 TA 接收数据时使用的方法。
         0  无

流控仅适用于数据模式。
示例
AT+IFC=2,2          //打开硬件流控。
OK

AT+IFC?
+IFC: 2,2

OK

3.4. AT+ICF  设置 TE-TA 控制字符帧格式

该命令决定 TA 从 TE 接收的串行接口字符帧格式和校验位。
         2  RTS 流控
<dte_by_dce>  整型。指定 TA 在从 TE 接收数据时使用的方法。
         0  无
         2  CTS 流控
AT+ICF  设置 TE-TA 控制字符帧格式
测试命令
AT+ICF=?
响应
+ICF: (list of supported <format>s),(list of supported
<parity>s)

OK
读取命令
AT+ICF?
响应
+ICF: <format>,<parity>

OK
写入命令
AT+ICF=[<format>,[<parity>]]
响应
OK
或
ERROR
最大响应时间 300 ms
注释

参数

1. 该命令适用于命令状态。
2. 如果 <format> 字段指定无校验位，则省略 <parity> 字段。

3.5. AT+IPR  设置 TE-TA 固定本地速率

该命令查询并设置 UART 的波特率。
特性 该指令立即生效。
该配置可以通过 AT&W 保存。
参考
V.25ter

<format>  整型。
    3  8 个数据位，0 个校验位，1 个停止位
<parity>  整型。
    0  奇校验（Odd）
          1  偶校验（Even）
          2  标记（Mark (1)）
 3  空号（Space (0)）
AT+IPR  设置 TE-TA 固定本地速率
测试命令
AT+IPR=?
响应
+IPR: (list of supported auto detectable <rate>s),(list of
supported fixed-only <rate>s)

OK
读取命令
AT+IPR?
响应
+IPR: <rate>

OK
写入命令
AT+IPR=<rate>
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
该配置可以通过 AT&W 保存。
注释

参数

1. 如果设置了固定波特率，请确保 TE（DTE，通常为外部处理器）和 TA（DCE，移远通信模组）均配置为相同的速率。
2. AT+IPR 的值无法通过 AT&F 和 ATZ 恢复；但可以通过 AT&W 保存。
3. 在多路复用模式下，无法通过写入命令 AT+IPR=<rate> 更改波特率；即使在写入命令后执行 AT&W，该设置也无效且无法保存。
4. 选定的波特率在写入命令执行并确认 OK 后生效。
示例
AT+IPR=115200       //将固定波特率设置为 115200bps
OK
AT&W                                 //保存当前设置，即模组重启后串口通信
          速度为 115200 bps
OK
AT+IPR?
+IPR: 115200

OK
AT+IPR=115200;&W      //将固定波特率设置为 115200bps 并保存当前设置
OK
参考
V.25ter

<rate>  字符串类型。每秒波特率。
            4800
9600
   19200
   38400
      57600
115200
            230400
460800
921600
2900000
3000000
3200000
3686400
4000000
注释

3.6. AT+QRIR  将 RI 行为恢复为非激活

该命令将 RI 行为恢复为非激活。

如果 RI（振铃指示）行为为 "always"，则可以通过执行命令将其恢复为非激活。RI 行为由 AT+QCFG 控制。更多详细信息，请参阅 AT+QCFG="urc/ri/ring"、AT+QCFG="urc/ri/smsincoming" 和 AT+QCFG="urc/ri/other"。
AT+QRIR  将 RI 行为恢复为非激活
测试命令
AT+QRIR=?
响应
OK
执行命令
AT+QRIR
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
该配置不会被自动保存。
