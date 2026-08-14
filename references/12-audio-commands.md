# 12 音频指令 (Audio Commands)

12 音频指令

12.1. AT+CLVL 扬声器音量等级选择

该指令用于选择 MT 内部扬声器的音量。
参数

AT+CLVL  扬声器音量等级选择
测试命令
AT+CLVL=?
响应
+CLVL: (range of supported <level>s)

OK
读取命令
AT+CLVL?
响应
+CLVL: <level>

OK
写入命令
AT+CLVL=<level>
响应
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置将被保存。
参考
3GPP TS 27.007

<level>  整型。音量等级，其范围由制造商定义（最小值代表最低音量）。范围：0–5。默认值：3。
<err>        错误码。更多详情请参考第 15.4 章。

12.2. AT+CMUT 静音控制

该指令用于在语音通话期间启用/禁用上行链路语音静音。
参数

AT+CMUT  静音控制
测试命令
AT+CMUT=?
响应
+CMUT: (list of supported <n>s)

OK
读取命令
AT+CMUT?
响应
+CMUT: <n>

OK
写入命令
AT+CMUT=<n>
响应
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性
该指令立即生效。
配置不会被保存，必须在通话期间设置。
参考
3GPP TS 27.007

<n>   整型。
   0  静音关闭
   1  静音开启
<err>   错误码。更多详情请参考第 15.4 章。

12.3. AT+QAUDLOOP 启用/禁用音频环回测试

该指令用于启用/禁用音频环回测试。
参数

12.4. AT+VTS DTMF 和音调生成

该指令发送 ASCII 字符，使 MSC 向远端用户传输 DTMF 音调。
该指令只能在语音通话中操作。
AT+QAUDLOOP  启用/禁用音频环回测试
测试命令
AT+QAUDLOOP=?
响应
+QAUDLOOP: (list of supported <enable>s)

OK
读取命令
AT+QAUDLOOP?
响应
+QAUDLOOP: <enable>

OK
写入命令
AT+QAUDLOOP=<enable>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<enable> 整型。用于启用或禁用音频环回测试。
0   禁用音频环回测试
1   启用音频环回测试
<err>    错误码。更多详情请参考第 15.4 章。
AT+VTS  DTMF 和音调生成
测试命令
AT+VTS=?
响应
+VTS: (list of supported <DTMF_string>s),(range of
supported <duration>s)

OK

参数
示例
ATD12345678900;                 //拨号。
OK
//呼叫连接
AT+VTS="1"                      //远端呼叫方可听到 DTMF 音调。
OK
AT+VTS="1234567890A"          //一次发送多个音调。
OK

写入命令
AT+VTS=<DTMF_string>[,<duration>]
响应
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 取决于 <DTMF_string> 和 <duration> 的长度。
特性 /
参考
3GPP TS 27.007

<DTMF_string>  字符串类型。ASCII 字符，范围为 0...9、#、*、A、B、C、D。字符串
应用引号（"..."）括起来。
 一次发送多个音调时，两个音调的时间间隔
 <interval> 可通过 AT+VTD 指定。字符串的最大长度为
 31。
<duration>              每个音调的持续时间，单位为 1/10 秒，允许一定容差。范围：0–255。
 如果持续时间小于网络指定的最短时间，实际持续时间将采用网络指定的时间。
 如果省略该参数，则 <duration> 由 AT+VTD 指定。
<err>               错误码。更多详情请参考第 15.4 章。

12.5. AT+VTD 设置音调持续时间

该指令用于设置 DTMF 音调的持续时间。它还可以在一次性发送多个音调时设置两个音调的时间间隔。
参数

AT+VTD  设置音调持续时间
测试命令
AT+VTD=?
响应
+VTD: (range of supported <duration>s),(range of supported
<interval>s)

OK
读取命令
AT+VTD?
响应
+VTD: <duration>,<interval>

OK
写入命令
AT+VTD=<duration>[,<interval>]
响应
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
参考
3GPP TS 27.007

<duration>  音调持续时间，单位为 1/10 秒，允许一定容差。范围：0–255。默认值：3。
 如果持续时间小于网络指定的最短时间，实际持续时间将采用网络指定的时间。
<interval>            使用 AT+VTS 一次性发送多个音调时，两个音调的时间间隔。范围：0–255。默认值：0。
<err>              错误码。更多详情请参考第 15.4 章。

12.6. AT+QAUDMOD 设置音频模式

该指令用于设置所连接设备所需的音频模式。
参数

AT+QAUDMOD  设置音频模式
测试命令
AT+QAUDMOD=?
响应
+QAUDMOD: (range of supported <mode>s)

OK
读取命令
AT+QAUDMOD?
响应
+QAUDMOD: <mode>

OK
写入命令
AT+QAUDMOD=<mode>
响应
OK

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置将自动保存。
参考
Quectel

<mode>  整型。表示当前配置的音频模式。
0   听筒的回声消除器、噪声抑制器、数字增益和校准参数
1   耳机的回声消除器、噪声抑制器、数字增益和校准参数
2   扬声器的回声消除器、噪声抑制器、数字增益和校准参数
3   关闭所有音频处理功能
4   蓝牙的回声消除器、噪声抑制器、数字增益和校准参数
5   通用音频模式的回声消除器、噪声抑制器、数字增益和校准参数
<err>    错误码。更多详情请参考第 15.4 章。

12.7. AT+QDAI 数字音频接口配置

该指令用于配置数字音频接口。

⚫ 当 <io>=1 时，您可以定义 PCM 格式。在以下条件下，模块可直接使用默认设置（主模式、短同步、2048 kHz 时钟频率、16 位线性数据格式、8 kHz 采样率）。
⚫ 当 <io>=2 时，与 PCM 接口连接的外部编解码器芯片为 NAU8814 型号，可通过 I2C 配置。
⚫ 当 <io>=3 时，与 PCM 接口连接的外部编解码器芯片为 ALC5616 型号，可通过 I2C 配置。
⚫ 当 <io>=5 时，与 PCM 接口连接的外部编解码器芯片为 TLV320AIC3104 型号，可通过 I2C 配置。
⚫ 当 <io>=6 时，与 PCM 接口连接的外部编解码器芯片为 NAU8810 型号，可通过 I2C 配置。

AT+QDAI  数字音频接口配置
测试命令
AT+QDAI=?
响应
+QDAI: (range of supported <io>s),(list of supported
<mode>s),(list of supported <fsync>s),(range of supported
<clock>s),(range of supported <format>s),(list of supported
<sample>s),(list of supported <num_slots>s),(range of
supported <slot_mapping>s)

OK
读取命令
AT+QDAI?
响应
+QDAI: <io>[,<mode>,<fsync>,<clock>,<format>,<sample>,<num_slots>,<slot_mapping>]

OK
写入命令
AT+QDAI=<io>[,<mode>,<fsync>,<clock>[,<format>[,<sample>[,<num_slots>,<slot_mapping>]]]]
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令在模块重新启动后生效。
配置将自动保存。
参考
Quectel

参数

1. 4096 kHz 时钟频率仅适用于 16 kHz 采样率。
2. 不支持 128 kHz 时钟频率。
3. 不支持 8 位 a-law 和 8 位 u-law 数据格式。
4. 每帧位数=<clock>/<sample>。例如，如果 <clock> 为 2048 kHz 且 <sample> 为 8 kHz，则每帧位数为 256。每帧位数应大于 16。
5. 选择从模式时，应为模块提供主时钟和同步时钟。
6. 当选择推荐的编解码器并希望使用 16 kHz 采样率时，请输入 <sample>。目前仅 ALC5616 支持 16 kHz（AT+QDAI=3,0,0,5,0,1,1,1）。
7. 带有 R07 的工程软件版本（例如 EG91NAXGAR07A03M1G_01.003.01.003）支持自动匹配编解码器驱动程序，因此您无法使用此指令配置数字音频接口。
<io>         整型。
    1   数字 PCM 输出（客户自定义）
 2      模拟输出（用于音频编解码器 NAU8814）
3      模拟输出（用于我们的默认音频编解码器 ALC5616）
4      模拟输出（用于音频编解码器 MAX9860）
5      模拟输出（用于音频编解码器 TLV320AIC3104）
6      模拟输出（用于音频编解码器 NAU8810）
<mode>      整型。
    0   主模式
 1   从模式
<fsync>      整型。
    0    主模式（短同步）
 1   辅助模式（长同步）
<clock>      整型。时钟频率。
    0     128 kHz
 1     256 kHz
 2     512 kHz
 3    1024 kHz
 4    2048 kHz
5    4096 kHz
<format>     整型。数据格式。
    0    16 位线性
<sample>    整型。采样率。
    0    8 kHz
1    16 kHz
<num_slots> 整型。时隙数量。默认值：1。
<slot_mapping> 整型。时隙映射值。范围：1–16。
注释

示例
AT+QDAI=?     //查询范围。
+QDAI: (1-6),(0,1),(0,1),(0-5),(0-2),(0,1),(1),(1-16)

OK
AT+QDAI?          //查询当前接口配置。
+QDAI: 3,0,0,4,0,0,1,1

OK
AT+QDAI=1,1,0,4,0,0,1,1 //将 AUX PCM 接口设置为从模式、短同步、8 kHz 采样率
 和 2048 kHz BCLK。
OK

12.8. AT+QEEC 设置回声消除参数

该指令用于设置回声消除参数。
参数
AT+QEEC  设置回声消除参数
测试命令
AT+QEEC=?
响应
+QEEC: (range of supported <index>s),(range of supported
<value>s)

OK
读取命令
AT+QEEC?
响应
+QEEC: <index>,<value>
......
+QEEC: <index>,<value>

OK
写入命令
AT+QEEC=<index>,<value>
响应
OK
或
ERROR
特性 该指令立即生效。
配置不会被保存。
<index>  整型。表示参数的索引。范围：0–50。
<value>  整型。表示参数的值。范围：0–65535。

示例
AT+QEEC=?      //查询范围。
+QEEC: (0-50),(0-65535)

OK
AT+QEEC=6,1234 //将索引 6 的值设置为 1234。
OK

12.9. AT+QSIDET 设置当前模式下的侧音增益

该指令用于设置当前模式下的侧音增益值。
参数

AT+QSIDET  设置当前模式下的侧音增益
测试命令
AT+QSIDET=?
响应
+QSIDET: (range of supported <st_gain>s)

OK
读取命令
AT+QSIDET?
响应
+QSIDET: <st_gain>

OK
写入命令
AT+QSIDET=<st_gain>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该配置在下一次音频活动时生效。
该配置不会被保存。
参考
Quectel

<st_gain>   整型。表示当前模式下配置的侧音增益。
  范围：0–65535。默认值：0。

12.10. AT+QMIC 设置麦克风上行增益

该指令用于设置麦克风的上行增益。
参数

12.11. AT+QRXGAIN 设置 RX 下行增益

该指令用于设置 RX 数字增益以改变下行音量。
AT+QMIC  设置麦克风上行增益
测试命令
AT+QMIC=?
响应
+QMIC: (range of supported <txgain>s),(range of supported
<txdgain>s)

OK
读取命令
AT+QMIC?
响应
+QMIC: <txgain>,<txdgain>

OK
写入命令
AT+QMIC=<txgain>[,<txdgain>]
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
配置将被保存。
<txgain>  整型。表示上行链路编解码器增益。范围：0–65535。默认值可能因音频模式不同而不同。
<txdgain>   整型。表示上行链路数字增益。范围：0–65535。默认值可能因音频模式不同而不同。
AT+QRXGAIN  设置 RX 下行增益
测试命令
AT+QRXGAIN=?
响应
+QRXGAIN: (range of supported <rxgain>s)

OK

参数
示例
AT+QRXGAIN=?
+QRXGAIN: (0-65535)

OK
AT+QRXGAIN?                //查询当前配置。
+QRXGAIN: 20577

OK
AT+QRXGAIN=8192        //将数字增益设置为 8192。
OK
AT+QRXGAIN?          //查询当前配置。
+QRXGAIN: 8192

OK

读取命令
AT+QRXGAIN?
响应
+QRXGAIN: <rxgain>

OK
写入命令
AT+QRXGAIN=<rxgain>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<rxgain> 整型。下行链路数字增益。范围：0–65535。默认值因音频模式而异。

12.12. AT+QIIC 通过 IIC 读写编解码器

该指令通过 IIC 接口配置编解码器。
参数
示例
AT+QIIC=1,0x1B,0x00,2 // 读取寄存器值，从设备地址：0x1B，寄存器
   地址：0x00，读取两个字节。
+QIIC: 0x0021

OK
AT+QIIC  通过 IIC 读写编解码器
测试命令
AT+QIIC=?
响应
+QIIC: (list of supported <rw>s),(range of supported
<device>s),(range of supported <addr>s),(list of supported
<bytes>s),(range of supported <value>s)

OK
写入命令
AT+QIIC=<rw>,<device>,<addr>,<bytes>[,<value>]
响应
如果 <rw>=0，应指定所有配置参数：
OK

如果 <rw>=1，应省略 <value>：
+QIIC: <value>

OK
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<rw> 整型。
0 写入命令
1 读取命令
<device> 十六进制整型。
0-0xFF  7 位设备地址
<addr> 十六进制整型。
0-0xFF  寄存器地址
<bytes> 整型。读取或写入的字节长度。范围：1–2。
<value> 十六进制整型。
0-0xFFFF  数据值

AT+QIIC=0,0x1B,0x00,2,0x0000 //写入寄存器值，从设备地址：0x1B，寄存器地址：
0x00，写入两个字节。
OK

12.13. AT+QTONEDET 启用/禁用 DTMF 检测

该指令用于启用或禁用 DTMF 检测。如果启用了此功能，对端发送的 DTMF 音调将被检测并在指定的串口上上报。
参数

DTMF 字符 - ASCII：
DTMF ASCII DTMF ASCII
0 48 8 56
1 49 9 57
2 50 A 65
3 51 B 66
AT+QTONEDET  启用/禁用 DTMF 检测
测试命令
AT+QTONEDET=?
响应
+QTONEDET: (list of supported <enable>s)

OK
读取命令
AT+QTONEDET?
响应
+QTONEDET: <enable>

OK
写入命令
AT+QTONEDET=<enable>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<enable>      整型。启用或禁用 DTMF 检测。
0    禁用
1    启用
注意

4 52 C 67
5 53 D 68
6 54 * 42
7 55 # 35

12.14. AT+QLDTMF 播放本地 DTMF

该指令用于播放本地 DTMF 字符串。本地 DTMF 字符串的最大长度为 20 个字符。它也可用于停止播放本地 DTMF。
参数
AT+QLDTMF  播放本地 DTMF
测试命令
AT+QLDTMF=?
响应
+QLDTMF: (range of supported <n>s),(list of supported
<DTMF_string>s)

OK
写入命令
AT+QLDTMF=<n>,<DTMF_string>[,<y>]
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>

当 DTMF 字符串完全播放完毕后：
+QLDTMF:5
执行命令
停止播放 DTMF 字符串
AT+QLDTMF
响应
OK
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<n> 整型。表示每个 DTMF 的播放时间和静音时间。范围：1–1000。单位：
当 <y>=1 时为 1/100 秒，当未设置 <y> 时为 1/10 秒。
<DTMF_string> 字符串类型。DTMF 字符串。最大长度：20 个字符（以逗号分隔）。
DTMF 格式：0-9、*、#、A-D。

示例
AT+QLDTMF=?
+QLDTMF: (1-1000),(0-9,*,#,A-D)

OK
AT+QLDTMF=2,"A,B,1,2,#"     //播放本地 DTMF 字符串 A,B,1,2,#，ON 和静音时间为 200 ms。

OK
AT+QLDTMF      //停止播放本地 DTMF。
OK

12.15. AT+QWDTMF 在通话期间将 DTMF 文件播放或发送到远端

该指令用于在通话期间将 DTMF 文件播放或发送到远端。
<y> 整型。如果省略该参数，则 <n> 的单位为 1/10 秒。如果
该参数指定为 1，则 <n> 的单位为 1/100 秒。
<err> 错误码。更多详情请参考第 15.4 章。
AT+QWDTMF  将 DTMF 文件播放或发送到远端
测试命令
AT+QWDTMF=?
响应
+QWDTMF: (list of supported <ulmute>s),(list of supported
<dlmute>s),(list of supported <DTMF_string>s),(range of
supported <duration>s),(range of supported <pause>s)

OK
读取命令
AT+QWDTMF?
响应
+QWDTMF: <status>

OK
写入命令
AT+QWDTMF=<ulmute>,<dlmute>,<DTMF_string>,<duration>,<pause>
响应
OK

当 DTMF 播放完成后：
+QWDTMF: 6
或
ERROR
最大响应时间 300 ms
特性 /

参数
示例
AT+QWDTMF=?
+QWDTMF: (0,1),(0,1),(0-9,*,#,A-G),(1-1000)

OK
AT+QWDTMF=1,1,"A,B,1,2,#",100       //播放 DTMF 字符串 A,B,1,2,# 并在通话期间将其发送到远端

OK
+QWDTMF: 6                     //DTMF 播放完成。
AT+QWDTMF?         //查询 DTMF 播放器状态。
+QWDTMF: 0

OK

12.16. AT+QLTONE 播放本地自定义音调

该指令用于播放本地自定义音调。<period_on> 表示播放时间，<period_off> 表示静音时间，<duration> 表示总时间。
<ulmute>   整型。是否静音上行链路 DTMF。
     0  静音
     1  不静音
<dlmute>         整型。是否静音下行链路 DTMF。
     0  静音
     1  不静音
<DTMF_string>   字符串类型。DTMF 字符串。最大长度：16 个字符（以逗号分隔）。
  DTMF 格式：0–9、*、#、A–D、E（1400 Hz）、F（2300 Hz）、G（1000 Hz）。
<duration>   整型。DTMF 播放时间，单位：毫秒。范围：55–1000。
<status>   整型。DTMF 播放器的状态。
     0  空闲
     1  忙
<pause>   整型。播放 DTMF 的间隔。范围：55–1000。
AT+QLTONE  播放本地自定义音调
测试命令
AT+QLTONE=?
响应
+QLTONE: (list of supported <mode>s),(range of supported
<frequency>s),(range of supported <period_on>s),(range of
supported <period_off>s),(range of supported <duration>s)

参数
示例
AT+QLTONE=?
+QLTONE: (0,1),(100-4000),(0-1000),(0-1000),(0-15300000)

OK
AT+QLTONE=1,1000,200,300,3000 //播放一个 1000 Hz 的音调，播放时间为 200 ms，静音时间为
300 ms。总时间为 3000 ms。
OK

+QLTONE: 0

OK
写入命令
AT+QLTONE=<mode>[,<frequency>,<period_on>,<period_off>,<duration>]
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>

当音调完全播放完毕后：
+QLTONE: 0
执行命令
停止播放本地自定义音调。
AT+QLTONE
响应
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<mode>        整型。
0       停止播放
1    开始播放
<frequency>  整型。音调的频率。范围：100–4000。单位：Hz。
<period_on>    整型。音调的播放时间。范围：0–1000。单位：ms。
<period_off> 整型。音调的静音时间。范围：0–1000。单位：ms。
<duration>     整型。音调的总时间。范围：0–15300000。单位：ms。
<err>           错误码。更多详情请参考第 15.4 章。

AT+QLTONE=0      //停止播放。
OK

12.17. AT+QAUDRD 录制媒体文件

该指令用于录制语音通话期间的上行或下行语音，或在空闲状态下录制本地麦克风的声音，并将其保存到文件中。
参数
AT+QAUDRD  录制媒体文件
测试命令
AT+QAUDRD=?
响应
+QAUDRD: (list of supported <state>s),"filename",(list of
supported <format>),(list of supported <dlink>s)

OK
读取命令
AT+QAUDRD?
响应
+QAUDRD: <state>

OK
写入命令
AT+QAUDRD=<control>[,<filename>[,<format>[,<dlink>]]]
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>
最大响应时间 300 ms
特性 /
<state>         整型。
0   模块未在录制媒体文件
1   模块正在录制媒体文件
<control>       整型。
0   停止录制
1   开始录制
<filename>  字符串类型。所录制的媒体文件的名称。

<format>  整型。文件的格式。
    3  FORMAT_AMR

1. <filename> 是用于保存录制文件的路径，默认路径为 /data/ufs 目录。
2. EC2x、EG9x、EG2x-G 和 EM05 系列模块支持播放 wav 或 amr 格式的媒体文件，采样频率为 8 kHz 和 16 kHz，单声道，16 位量化。
3. 如果录制文件的名称和格式与现有文件相同，或发生未知错误，模块将上报 +QAUDRIND: 0,1。
4. 如果当前录制被其他音频任务中断，模块将上报 +QAUDRIND: 0,6。
5. 如果没有空间进行录制，模块将上报 +QAUDRIND: 0,3。
6. 模块支持录制上行和下行音频数据，但不支持同时录制。
7. 如果文件格式与文件扩展名不一致，该指令将返回错误。

表 8：URC +QAUDRIND: 0,<code> 中 <code> 的说明
示例
AT+QAUDRD=1,"A.wav",13,0  //以 wav 格式录制上行声音，并将其存储在 UFS 中。
OK
AT+QAUDRD=0     //停止录制。
OK
AT+QAUDRD=1,"B.wav",13,1     //以 wav 格式录制下行声音，并将其存储在 UFS 中。
OK
AT+QAUDRD=0     //停止录制。
OK

    13  WAV_PCM16
<dlink>   整型。录制上行或下行声音。
0  录制上行声音
    1  录制下行声音
<err>           错误码。更多详情请参考第 15.4 章。
<code> 含义
0 保留
1 未知错误
3 没有空间录制
6 被其他音频任务中断
注释

12.18. AT+QPSND 播放 WAV 文件

该指令用于播放本地 wave 文件。
参数
AT+QPSND  播放 WAV 文件
测试命令
AT+QPSND=?
响应
+QPSND: (list of supported <control>s),"filename",(list of
supported <repeat>s),(list of supported <ulmute>s),(list of
supported <dlmute>s)

OK
读取命令
AT+QPSND?
响应
+QPSND: <state>

OK
写入命令
AT+QPSND=<control>,<filename>,<repeat>[,<ulmute>[,<dlmute>]]
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>

当播放完成后：
+QPSND: 0
最大响应时间 300 ms
特性 /
<state> 整型。
0 模块未在播放本地音频文件
1 模块正在播放本地音频文件
<control> 整型。
0 停止播放本地音频文件
1 开始播放本地音频文件
<filename> 字符串类型。要播放的文件的名称。
<repeat> 整型。是否重复播放。
0 仅播放一次
1 重复播放

1. <filename> 包括文件路径、文件名和文件后缀。默认播放路径为 /data/ufs。
2. EC2x、EG9x、EG2x-G 和 EM05 系列模块支持播放 wav、amr 或 mp3 格式的媒体文件，采样频率为 8 kHz 和 16 kHz，单声道，16 位量化。
示例
AT+QPSND=1,"A.wav",0            //播放存储在 UFS 中的 wave 文件。
OK

+QPSND: 0
AT+QPSND=1,"A.wav",0,1,1        //在通话进行时向远端播放 wave 文件。
OK

+QPSND: 0

12.19. AT+QTTS 播放文本

该指令用于播放文本。
<ulmute> 整型。是否静音上行链路。
0 静音
1 不静音
<dlmute> 整型。是否静音下行链路。
0 静音
1 不静音
<err> 错误码。更多详情请参考第 15.4 章。
AT+QTTS  播放文本
测试命令
AT+QTTS=?
响应
+QTTS: (range of supported <mode>s),<text>

OK
读取命令
AT+QTTS?
响应
+QTTS: <status>

OK
写入命令
AT+QTTS=<mode>[,<text>]
响应
OK
注释

参数

1. 模块支持在非通话过程中使用 AT+QTTS 或 AT+QWTTS 播放 TTS。
2. 呼叫时 TTS 将被终止。
3. 模块支持播放 TTS 和音频，但不能同时播放。
示例
AT+QTTS=?
+QTTS: (0-2),<text>

OK
AT+QTTS=1,"6B228FCE4F7F752879FB8FDC6A215757"//播放一个 UCS2 字符串。
OK

+QTTS: 0
AT+QTTS=2,"hello world,你好"      //播放一个 ASCII 字符串。
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>

当播放完成后：
+QTTS: 0
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<mode> 整型。开始/停止播放，并指定 <text> 的格式。
0 停止播放，可省略 <text>。
1 开始播放，且 <text> 为 UCS2 编码。
2 开始播放，且 <text> 为字符：通常为 ASCII，中文为 GBK 编码。
<text> 字符串类型。要播放的文本。文本格式根据 <mode> 的不同而不同。最大
长度：548 字节。
<status> 整型。TTS 播放器的状态。
0 空闲
1 忙
<err> 错误码。更多详情请参考第 15.4 章。
注释

OK

+QTTS: 0
AT+QTTS=0           //停止播放。
OK

12.20. AT+QTTSETUP 设置 TTS

该指令用于设置 TTS 语速并调节音量。
参数
AT+QTTSETUP  设置 TTS
测试命令
AT+QTTSETUP=?
响应
+QTTSETUP: (list of supported <mode>s),(list of supported
<ID>s),(range of supported <value>s)

OK
读取命令
AT+QTTSETUP?
响应
OK
写入命令
AT+QTTSETUP=<mode>,<ID>[,<value>]
响应
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<mode> 整型。
1 写入参数的值
2 读取参数的值
<ID> 整型。
1 设置/读取语速
2 设置/读取音量
<value> 整型。语速或音量的值。如果 <mode>=2，请在写入命令中省略该值。

示例
AT+QTTSETUP=?
+QTTSETUP: (1,2),(1,2),(-32768~32767)

OK
AT+QTTSETUP=1,2,0       //将音量设置为 0。
OK

12.21. AT+QWTTS 播放文本或将文本发送到远端

该指令用于在通话时将文本播放或发送到远端。
TTS 语速。范围：-32768–32767。默认值：0。
TTS 音量。范围：-32768–32767。默认值：0。
<err> 错误码。更多详情请参考第 15.4 章。
AT+QWTTS  播放文本或将文本发送到远端
测试命令
AT+QWTTS=?
响应
+QWTTS: (list of supported <ulmute>s),(list of supported
<dlmute>s),(range of supported <mode>s),<text>

OK
读取命令
AT+QWTTS?
响应
+QWTTS: <status>

OK
写入命令
AT+QWTTS=<ulmute>,<dlmute>,<mode>,<text>
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>

当播放完成后：
+QWTTS: 0
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。

示例

1. 上报 +QWTTS: 4111 表示 TTS 被呼叫事件中断。
2. 在非通话状态下，播放 TTS 会上报 +CME ERROR: 903。
3. 在通话状态下，静音上行和下行音量后，播放 TTS 会上报 +CME ERROR: 903。
4. 如果 <ulmute> 和 <dlmute> 被设置为无效值，模块将上报 +CME ERROR: 902。
5. 模块支持播放 txt 字符，最大长度为 543 字节。
6. 播放空字符时，模块将上报 +CME ERROR: 902。
示例
AT+QWTTS=?
+QWTTS:(0,1),(0,1),(0-2),<text>

OK
AT+QWTTS=1,1,1,"6B228FCE4F7F752879FB8FDC6A215757"  //播放一个 UCS2 字符串并在通话期间将其发送到远端。
OK

+QWTTS: 0               //播放完成。
AT+QWTTS=1,0,2,"hello world,你好"                  //在通话期间向远端播放一个 ASCII 字符串。
OK
<ulmute> 整型。是否静音上行音量。
0 静音
1 不静音
<dlmute> 整型。是否静音下行音量。
0 静音
1 不静音
<mode> 整型。开始/停止播放，并指定 <text> 的格式。
0 停止播放，可省略 <text>
1 开始播放，且 <text> 为 UCS2 编码
2 开始播放，且 <text> 为字符，通常为 ASCII，中文为 GBK 编码
<text> 字符串类型。要播放的文本。文本格式根据 <mode> 的不同而不同。最大长度：543 字节。
<status> 整型。TTS 播放器的状态。
0 空闲
1 忙
<err> 错误码。更多详情请参考第 15.4 章。
注释

+QWTTS: 0             //播放完成。
AT+QWTTS=1,0,0                  //停止播放。
OK

12.22. AT+QAUDCFG 查询和配置音频调优过程

该指令用于查询和配置各种音频调优过程。

12.22.1. AT+QAUDCFG="alc5616/dlgain" 设置编解码器 ALC5616 的下行增益等级
该指令用于设置或查询编解码器 ALC5616 的下行增益等级。
AT+QAUDCFG  查询和配置音频调优过程
测试命令
AT+QAUDCFG=?
响应
+QAUDCFG: "alc5616/dlgain",(range of supported <level>s)
+QAUDCFG: "alc5616/ulgain",(range of supported <level>s)
+QAUDCFG: "tonevolume",(range of supported <tone_volume>s)
+QAUDCFG: "alc5616/pwrctr",(list of supported <enable>s)
+QAUDCFG: "nau8814/dlgain",(list of supported <level>s)
+QAUDCFG: "nau8814/aoutput",(list of supported <level>s)
+QAUDCFG: "encgain",(list of supported <control>s),(range of
supported <gain>s)
+QAUDCFG: "voltedtmfcfg",(range of supported <duration>s),(range
of supported <volume>s)
+QAUDCFG: "decgain",(range of supported <gain>s)
+QAUDCFG: "fns",(list of supported <fns>s),(list of supported
<enable>s)
+QAUDCFG: "nau8810/config",(range of supported <addr>s),(range
of supported <value>s),...

OK
最大响应时间 300 ms
AT+QAUDCFG="alc5616/dlgain"  设置编解码器 ALC5616 的下行增益等级
写入命令
AT+QAUDCFG="alc5616/dlgain"[,<level>]

响应
如果省略可选参数，则查询当前配置：
+QCFG: "alc5616/dlgain",<level>

参数
示例
AT+QAUDCFG="alc5616/dlgain",85     //将下行增益设置为 85。
OK
AT+QAUDCFG="alc5616/dlgain"    //查询当前下行增益。
+QCFG: "alc5616/dlgain", 85

OK

12.22.2. AT+QAUDCFG="alc5616/ulgain" 设置编解码器 ALC5616 的上行增益等级
该指令用于设置或查询编解码器 ALC5616 的上行增益等级。

OK

如果指定了可选参数，则设置下行增益等级：
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<level>      整型。ALC5616 的下行增益。范围：0–100。默认值：79。
<err>        错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="alc5616/ulgain"  设置编解码器 ALC5616 的上行增益等级
写入命令
AT+QAUDCFG="alc5616/ulgain"[,<level>]

响应
如果省略可选参数，则查询当前配置：
+QCFG: "alc5616/ulgain",<level>

OK

参数
示例
AT+QAUDCFG="alc5616/ulgain",85     //将上行增益设置为 85。
OK
AT+QAUDCFG="alc5616/ulgain"    //查询当前上行增益。
+QCFG: "alc5616/ulgain", 85

OK

12.22.3. AT+QAUDCFG="tonevolume" 设置音调音量
该指令用于设置或查询音调音量。
如果指定了可选参数，则设置上行增益等级：
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<level>       整型。ALC5616 的上行增益。范围：0–100。默认值：73。
<err>         错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="tonevolume"  设置音调音量
写入命令
AT+QAUDCFG="tonevolume"[,<tone_volume>]
响应
如果省略可选参数，则查询当前配置：
+QCFG: "tonevolume",<tone_volume>

OK

如果指定了可选参数，则设置音调音量：
OK
或
ERROR

参数
示例
AT+QAUDCFG="tonevolume",10 //将音调音量设置为 10。
OK
AT+QAUDCFG="tonevolume"    //查询当前音量。
+QCFG: "tonevolume",10

OK

12.22.4. AT+QAUDCFG="alc5616/pwrctr" 启用/禁用上电复位
该指令用于在编解码器电源复位到 MX-66h 寄存器时启用或禁用上电复位。
如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置将自动保存。
<tone_volume>       整型。音调音量值。范围：0–100。默认值：10。
<err>                 错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="alc5616/pwrctr"  启用/禁用上电复位
写入命令
AT+QAUDCFG="alc5616/pwrctr"[,<enable>]
响应
如果省略可选参数，则查询当前配置：
+QCFG: "alc5616/pwrctr",<enable>

OK

如果指定了可选参数，则启用/禁用上电复位
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms

参数
示例
AT+QAUDCFG=?
+QAUDCFG: "alc5616/pwrctr",(0-1)

OK
AT+QAUDCFG="alc5616/pwrctr",1    //启用上电复位。
OK
AT+QAUDCFG="alc5616/pwrctr"        //查询当前配置。
+QCFG: "alc5616/pwrctr", 1

OK

12.22.5. AT+QAUDCFG="nau8814/dlgain" 设置编解码器 NAU8814 的下行增益等级
该指令用于设置或查询编解码器 NAU8814 的下行增益等级。
特性 该指令立即生效。
配置不会被保存。
<enable>   整型。在编解码器电源复位到 MX-66h 寄存器时启用/禁用上电复位。
             0 禁用
    1 启用
<err>       错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="nau8814/dlgain"  设置编解码器 NAU8814 的下行增益等级
写入命令
AT+QAUDCFG="nau8814/dlgain"[,<level>]

响应
如果省略可选参数，则查询当前配置：
+QCFG: "nau8814/dlgain",<level>

OK

如果指定了可选参数，则设置下行增益等级：
OK
或
ERROR

参数
示例
AT+QAUDCFG="nau8814/dlgain",85    //将下行增益设置为 85。
OK
AT+QAUDCFG="nau8814/dlgain"
+QCFG: "nau8814/dlgain",85        //查询当前下行增益。

OK

12.22.6. AT+QAUDCFG="nau8814/aoutput" 设置编解码器 NAU8814 的模拟输出
该指令用于设置或查询编解码器 NAU8814 的模拟输出。

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<level>      整型。NAU8814 的下行增益。范围：0–100。默认值：79。
<err>        错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="nau8814/aoutput"  设置编解码器 NAU8814 的模拟输出
写入命令
AT+QAUDCFG="nau8814/aoutput"[,<level>]

响应
如果省略可选参数，则查询当前配置：
+QCFG: "nau8814/output",<level>

OK

如果指定了可选参数，则设置编解码器 NAU8814 的模拟输出：
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：

参数
示例
AT+QAUDCFG="nau8814/aoutput",1     //设置单声道混音器输出。
OK
AT+QAUDCFG="nau8814/aoutput"    //查询当前输出配置。
+QCFG: "nau8814/analog/output",0

OK

12.22.7. AT+QAUDCFG="encgain" 设置上行链路 ENC 增益
该指令用于设置或查询上行链路 ENC 增益。
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<level>         整型。输出模式。
    0 扬声器混音器输出
 1 单声道混音器输出
<err>           错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="encgain"  设置上行链路 ENC 增益
写入命令
AT+QAUDCFG="encgain"[,<control>,<gain>]

响应
如果省略可选参数，则返回当前配置：
+QCFG: "encgain",<control>,<gain>

OK

如果指定了可选参数，则设置上行链路 ENC 增益：
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>

参数
示例
AT+QAUDCFG="encgain",1,65535     //启用 ENC 并将 ENC 增益设置为 65535。
OK
AT+QAUDCFG="encgain"      //查询当前上行增益。
+QCFG: "encgain",1,65535

OK

12.22.8. AT+QAUDCFG="voltedtmfcfg" 设置 VoLTE DTMF 音调的持续时间和音量
该指令用于设置或查询模块接收到的 VoLTE DTMF 音调的持续时间和音量。
如果从未设置过该指令或将持续时间设置为 0，则 VoLTE DTMF 音调的持续时间由网络控制，音量采用默认值 200 x 2.5 ms。这样，网络设置的持续时间不能长于默认的 500 ms，否则模块会将其截断为 500 ms。
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<control>   整型。启用/禁用 ENC。
    0    禁用
    1    启用
<gain>         整型。ENC 增益。范围：0–65535。默认值：8192。
<err>           错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="voltedtmfcfg"  设置 VoLTE DTMF 音调的持续时间和音量
写入命令
AT+QAUDCFG="voltedtmfcfg"[,<duration>[,<volume>]]
响应
如果省略可选参数，则返回当前配置：
+QCFG: "voltedtmfcfg",<duration>,<volume>

OK

如果指定了可选参数，则设置 VoLTE DTMF 音调的持续时间和音量：
OK

参数

VoLTE DTMF 两个音调之间的时间间隔比持续时间稍长。
示例
AT+QAUDCFG="voltedtmfcfg",40,5000     //将 VoLTE DTMF 持续时间设置为 100 ms，将音量设置为 5000。
OK
AT+QAUDCFG="voltedtmfcfg"            //查询当前配置。
+QCFG: "voltedtmfcfg",40,5000

OK

12.22.9. AT+QAUDCFG="decgain" 设置下行链路 DEC 增益
该指令用于设置或查询下行链路 DEC 增益。
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<duration>  整型。DTMF 音调的持续时间。单位：2.5 ms。范围：1–1000。默认值：200。
<volume>  整型。DTMF 音调的音量。范围：0–65535。默认值：5000。
<err>           错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="decgain"  设置下行链路 DEC 增益
写入命令
AT+QAUDCFG="decgain"[,<gain>]
响应
如果省略可选参数，则查询当前配置：
+QCFG: "decgain",<gain>

OK

注释

参数
示例
AT+QAUDCFG="decgain",65535        //将下行链路 DEC 增益设置为 65535。
OK
AT+QAUDCFG="decgain"        //查询当前下行链路 DEC 增益。
+QAUDCFG: "decgain", 65535

OK

12.22.10. AT+QAUDCFG="fns" 启用/禁用噪声抑制
该指令用于启用/禁用噪声抑制功能并查询当前配置。
如果指定了可选参数，则设置下行链路 DEC 增益：
OK
或
ERROR

如果出现任何与 ME 功能相关的错误：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<gain>  整型。下行链路 DEC 增益。范围：0–65535。默认值随 ACDB 的配置而变化。
<err>  错误码。更多详情请参考第 15.4 章。
AT+QAUDCFG="fns"  启用/禁用噪声抑制
写入命令
AT+QAUDCFG="fns"[,<fns>,<enable>]
响应
如果省略可选参数，则查询当前配置：
+QCFG: "fns",<fns>,<enable>

OK

如果指定了可选参数，则启用/禁用噪声抑制功能：
OK

参数

12.22.11. AT+QAUDCFG="nau8810/config" 设置编解码器 NAU8810 的寄存器值
该指令用于设置和查询编解码器 NAU8810 的寄存器值。
参数

或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<fns>  整型。配置噪声抑制功能。始终为 0。
<enable> 整型。启用或禁用噪声抑制功能。
   0 禁用
   1 启用
AT+QAUDCFG="nau8810/config"  设置编解码器 NAU8810 的寄存器值
写入命令
AT+QAUDCFG="nau8810/config"[,<addr>,<value>[,<addr>,<value>[,…]]]
响应
如果省略可选参数，则查询当前配置：
+QCFG: "nau8810/config",<addr>,<value>[,<addr>,<value>[,..]]

OK

如果指定了可选参数，则设置寄存器值：
OK
或
ERROR
最大响应时间 300 ms
特性 该指令立即生效。
配置将自动保存。
<addr>  整型。NAU8810 寄存器的地址。范围：0–255。
<value>  整型。NAU8810 寄存器的值。范围：0–255。

12.23. AT+QAUDPLAY 播放媒体文件

该指令用于播放本地媒体文件。
参数

AT+QAUDPLAY  播放媒体文件
测试命令
AT+QAUDPLAY=?
响应
+QAUDPLAY: "filename",(list of supported <state>s)

OK
读取命令
AT+QAUDPLAY?
响应
+QAUDPLAY: <state>

OK
写入命令
AT+QAUDPLAY=<filename>,<repeat>
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>

当播放完成后：
+QAUDPLAY: 0
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<state>   整型。
    0 模块未在播放媒体文件
    1 模块正在播放媒体文件
<filename>  字符串类型。要播放的文件的名称，包括文件路径、文件名和文件后缀。文件路径必须为 UFS。
<repeat>  整型。是否重复播放文件。
    0 仅播放一次
    1 重复播放
<err>   错误码。更多详情请参考第 15.4 章。

1. 如果发生未知错误，模块将上报 +QAUDPIND: 0,1。
2. 如果当前播放被其他音频任务中断，模块将上报 +QAUDPIND: 0,6。
3. EC2x、EG9x、EG2x-G 和 EM05 系列模块支持播放 wav、amr 或 mp3 格式的媒体文件，采样频率为 8 kHz 和 16 kHz，单声道，16 位量化。

12.24. AT+QAUDPLAYGAIN 设置音频播放增益

该指令用于设置音频播放增益以改变音频播放音量。
参数

AT+QAUDPLAYGAIN  设置音频播放增益
测试命令
AT+QAUDPLAYGAIN=?
响应
+QAUDPLAYGAIN: (range of supported <audplay_gain>s)

OK
读取命令
AT+QAUDPLAYGAIN?
响应
+QAUDPLAYGAIN: <audplay_gain>

OK
写入命令
AT+QAUDPLAYGAIN=<audplay_gain>
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。
<audplay_gain> 整型。音频播放增益。范围：0–65535。默认值因音频模式而异。
<err>           错误码。更多详情请参考第 15.4 章。
注释

示例
AT+QAUDPLAYGAIN=?
+QAUDPLAYGAIN: (0-65535)

OK
AT+QAUDPLAYGAIN?          //查询当前配置。
+QAUDPLAYGAIN: 8192

OK
AT+QAUDPLAYGAIN=4096    //将音频播放增益设置为 4096。
OK
AT+QAUDPLAYGAIN?          //查询当前配置。
+QAUDPLAYGAIN: 4096

OK

12.25. AT+QAUDRDGAIN 设置音频录制增益

该指令用于设置音频录制增益以改变音频录制音量。
AT+QAUDRDGAIN  设置音频录制增益
测试命令
AT+QAUDRDGAIN=?
响应
+QAUDRDGAIN: (range of supported <audrd_gain>s)

OK
读取命令
AT+QAUDRDGAIN?
响应
+QAUDRDGAIN: <audrd_gain>

OK
写入命令
AT+QAUDRDGAIN=<audrd_gain>
响应
OK
或
ERROR

如果错误与 ME 功能相关：
+CME ERROR: <err>
最大响应时间 300 ms
特性 该指令立即生效。
配置不会被保存。

参数
示例
AT+QAUDRDGAIN=?
+QAUDRDGAIN: (0-65535)

OK
AT+QAUDRDGAIN?            //查询当前配置。
+QAUDRDGAIN: 8192

OK
AT+QAUDRDGAIN=4096        //将音频录制增益设置为 4096。
OK
AT+QAUDRDGAIN?          //查询当前配置。
+QAUDRDGAIN: 4096

OK

12.26. AT+QACDBLOAD 写入 ACDB 文件

该指令将音频 DSP 参数配置文件（ACDB 文件）写入模块，并分别在 modem 侧和 AP 侧自动保存一份副本。导入新的 ACDB 文件后，<version> 的值将增加 1。
<audrd_gain> 整型。音频录制增益。范围：0–65535。默认值随音频模式而变化。
<err>          错误码。更多详情请参考第 15.4 章。
AT+QACDBLOAD  写入 ACDB 文件
测试命令
AT+QACDBLOAD=?
响应
+QACDBLOAD: "filename",<file_length>

OK
写入命令
AT+QACDBLOAD=<filename>,<file_length>
响应
CONNECT
<input data>
OK

+QACDBLOAD: <written_length>
或

参数
示例
AT+QACDBLOAD="11.acdb",100
CONNECT
<input data>
OK

+QACDBLOAD: 100
AT+QACDBLOAD?
+QACDBLOAD: "modem","11.acdb",100,1
+QACDBLOAD: "AP","11.acdb",100,1

OK

12.27. AT+QACDBREAD 读取 ACDB 文件

该指令用于读取存储在 modem 侧或 AP 侧的音频 DSP 参数配置文件（ACDB 文件）。
ERROR
读取命令
AT+QACDBLOAD?
响应
+QACDBLOAD: "modem","filename",<file_length>,<version>
+QACDBLOAD: "ap","filename",<file_length>,<version>

OK
最大响应时间 300 ms
特性 该指令在模块重新启动后生效。
配置将自动保存。
<filename>   字符串类型。ACDB 文件的名称。
<file_length>  整型。ACDB 文件的大小。
<written_length> 整型。实际写入的 ACDB 文件的长度。
<version>   整型。ACDB 文件的版本。
AT+QACDBREAD  读取 ACDB 文件
测试命令
AT+QACDBREAD=?
响应
+QACDBREAD: "filename",(list of supported <location>s)

参数
示例
AT+QACDBREAD="11.acdb",0
CONNECT
<output data>
OK

+QACDBREAD: 100

12.28. AT+QACDBDEL 删除 ACDB 文件

该指令用于删除存储在 modem 侧或 AP 侧的音频 DSP 参数配置文件（ACDB 文件）。

OK
写入命令
AT+QACDBREAD="filename",<location>
响应
CONNECT
<output data>
OK

+QACDBREAD: <read_length>
或
ERROR
最大响应时间 300 ms
特性 /
<filename>   字符串类型。ACDB 文件的名称。
<read_length>  整型。实际读取的 ACDB 文件的长度。
<location>   整型。ACDB 文件的位置。
0 Modem 侧
1 AP 侧
AT+QACDBDEL  删除 ACDB 文件
测试命令
AT+QACDBDEL=?
响应
+QACDBDEL: "filename",(list of supported
<location>s)

参数
示例
AT+QACDBDEL="11.acdb",1
OK
AT+QACDBLOAD?
+QACDBLOAD: "modem","11.acdb",100,1

OK

OK
写入命令
AT+QACDBDEL="filename",<location>
响应
OK
或
ERROR
最大响应时间 300 ms
特性 /
<filename>   字符串类型。ACDB 文件的名称。
<location>   整型。ACDB 文件的位置。
0 Modem 侧
1 AP 侧
