# 10 分组域指令 (Packet Domain Commands)

10 分组域指令

## 10.1. AT+CGATT  PS 附着或去附着 (Attachment or Detachment of PS)

该写入命令将 MT 附着到分组域业务，或使 MT 从分组域业务去附着。命令完成后，MT 仍保持 V.25ter 命令状态。如果 MT 已处于所请求的状态，则该命令将被忽略并返回 OK 响应。如果无法达到所请求的状态，则返回 ERROR 或 +CME ERROR 响应。

参数

AT+CGATT  PS 附着或去附着 (Attachment or Detachment of PS)

测试命令

AT+CGATT=?

响应

+CGATT: (list of supported <state>s)

OK

读取命令

AT+CGATT?

响应

+CGATT: <state>

OK

写入命令

AT+CGATT=<state>

响应

OK

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 140 s，由网络决定。

特性 命令是否生效由网络决定。

配置不会被保存。

参考

3GPP TS 27.007

<state>    整型。指示 PS 附着状态。
   0  去附着
   1  附着
   其他值为保留值，执行写入命令时将返回 ERROR 响应。
<err>      错误码。更多详情请参考第 15.4 章。

示例

AT+CGATT=1       //附着到 PS 业务。
OK
AT+CGATT=0       //从 PS 业务去附着。
OK
AT+CGATT?        //查询当前 PS 业务状态。
+CGATT: 0

OK

## 10.2. AT+CGDCONT  定义 PDP 上下文 (Define PDP Context)

该命令用于指定特定上下文 <cid> 的 PDP 上下文参数。写入命令的一种特殊形式（AT+CGDCONT=<cid>）会使上下文 <cid> 的取值变为未定义。不允许更改已激活上下文的定义。

该读取命令返回每个已定义 PDP 上下文的当前设置。

AT+CGDCONT  定义 PDP 上下文 (Define PDP Context)

测试命令

AT+CGDCONT=?

响应

+CGDCONT: (range of supported <cid>s),<PDP_type>,<APN>,<PDP_addr>,(range of supported <data_comp>s),(range of supported <head_comp>s),(list of supported <IPv4_addr_alloc>s),(list of supported <request_type>s)

OK

读取命令

AT+CGDCONT?

响应

+CGDCONT: <cid>,<PDP_type>,<APN>,<PDP_addr>,<data_comp>,<head_comp>,<IPv4_addr_alloc>,<request_type>
[…]

OK

写入命令

AT+CGDCONT=<cid>[,<PDP_type>[,<APN>[,<PDP_addr>[,<data_comp>[,<head_comp>[,<IPv4_addr_alloc>[,<request_type>]]]]]]]

响应

OK

或

ERROR

最大响应时间 300 ms

特性 命令立即生效。

参数

配置将自动保存。

参考

3GPP TS 27.007

<cid>           整型。PDP 上下文标识符。一个用于指定特定 PDP 上下文定义的数值参数。该参数仅在 TE-MT 接口本地有效，并用于其他与 PDP 上下文相关的命令。允许取值的范围（最小值 = 1）由命令的测试形式返回。
<PDP_type> 字符串类型。分组数据协议类型，一个用于指定分组数据协议类型的字符串参数。
"IP"   因特网协议（IETF STD 5）
"PPP"
"IPV6"
"IPV4V6"
<APN> 字符串类型。接入点名称（APN），一个用于选择 GGSN 或外部分组数据网络的逻辑名称参数。如果该值为空或省略，则将请求订阅值。
<PDP_addr>  字符串类型。标识 MT 在 PDP 适用地址空间中的地址。如果该值为空或省略，则在 PDP 启动流程期间可由 TE 提供一个值；否则，将请求动态地址。分配的地址可通过 AT+CGPADDR 读取。
<data_comp> 整型。控制 PDP 数据压缩（仅适用于 SNDCP）（参考 3GPP TS 44.065）。
    0     关（省略时默认值）
    1     开（制造商优选的压缩）
    2     V.42bis
<head_comp> 整型。控制 PDP 头压缩（参考 3GPP TS 44.065 和 3GPP TS 25.323）。
               0      关（省略时默认值）
               1      开
               2      RFC1144
               3      RFC2507
               4      RFC3095
<IPv4_addr_alloc> 整型。控制 MT/TA 如何请求获取 IPv4 地址信息。
  0  通过 NAS 信令分配 IPv4 地址
  1  通过 DHCP 分配 IPv4 地址
<request_type>  整型。指示 PDP 上下文的 PDP 上下文激活请求类型。
          0  PDP 上下文用于新建 PDP 上下文，或用于从非 3GPP 接入网络切换（MT 如何决定 PDP 上下文是用于新建 PDP 上下文还是用于切换，取决于具体实现）。
          1  PDP 上下文用于紧急承载业务

## 10.3. AT+CGQREQ  服务质量配置文件（请求）(Quality of Service Profile (Requested))

该命令允许 TE 指定当 MT 激活 PDP 上下文时使用的服务质量配置文件。

写入命令为上下文 <cid> 指定一个配置文件。写入命令的一种特殊形式 AT+CGQREQ=<cid> 会使上下文编号 <cid> 的请求配置文件变为未定义。该读取命令返回每个已定义上下文的当前设置。详细信息可参见 3GPP TS 23.107。

AT+CGQREQ  服务质量配置文件（请求）(Quality of Service Profile (Requested))

测试命令

AT+CGQREQ=?

响应

+CGQREQ: <PDP_type>,(range of supported <precedence>s),(range of supported <delay>s),(range of supported <reliability>s),(range of supported <peak>s),(range of supported <mean>s)

OK

读取命令

AT+CGQREQ?

响应

+CGQREQ: [<cid>,<precedence>,<delay>,<reliability>,<peak>,<mean>]
[+CGQREQ: <cid>,<precedence>,<delay>,<reliability>,<peak>,<mean>]
[…]

OK

写入命令

AT+CGQREQ=<cid>[,<precedence>[,<delay>[,<reliability>[,<peak>[,<mean>]]]]]

响应

OK

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性 命令立即生效。

配置将自动保存。

参考

3GPP TS 27.007

参数

<cid> 整型。指定特定的 PDP 上下文定义（参见 AT+CGDCONT）。
<PDP_type>    字符串类型。分组数据协议类型。
                 "IP"    因特网协议（IETF STD 5）
                 "PPP"
                 "IPV6"
                 "IPV4V6"
<precedence>  整型。指定优先级类别。
                  0  网络订阅值
                  1  高优先级。业务承诺应优先于优先级类别 2 和 3 得到保障
                  2  普通优先级。业务承诺应优先于优先级类别 3 得到保障
                  3  低优先级。业务承诺应得到保障
<delay> 整型。指定延迟类别。该参数定义了 SDU 通过网络传输时产生的端到端传输延迟。详情请参考表 6。
                  0  网络订阅值
<reliability>   整型。指定可靠性类别。
0  网络订阅值
1  非实时业务，无法容忍数据丢失的对错误敏感的应用程序
2  非实时业务，可容忍偶发数据丢失的对错误敏感的应用程序
3  非实时业务，可容忍数据丢失的对错误敏感的应用程序，GMM/SM 和 SMS
4  实时业务，可容忍数据丢失的对错误敏感的应用程序
5  实时业务，可容忍数据丢失的对错误不敏感的应用程序
<peak>    整型。指定峰值吞吐量类别，单位为每秒八位组。
0  网络订阅值
1  最高 1 000（8 kbit/s）
2  最高 2 000（16 kbit/s）
3  最高 4 000（32 kbit/s）
4  最高 8 000（64 kbit/s）
5  最高 16 000（128 kbit/s）
6  最高 32 000（256 kbit/s）
7  最高 64 000（512 kbit/s）
8  最高 128 000（1024 kbit/s）
9  最高 256 000（2048 kbit/s）
<mean>    指定平均吞吐量类别的数值参数，单位为每小时八位组。
                  0  网络订阅值
                  1  100（约 0.22 bit/s）
                  2  200（约 0.44 bit/s）

表 7：延迟类别

3  500（约 1.11 bit/s）
4  1 000（约 2.2 bit/s）
5  2 000（约 4.4 bit/s）
6  5 000（约 11.1 bit/s）
7  10 000（约 22 bit/s）
8  20 000（约 44 bit/s）
9  50 000（约 111 bit/s）
10  100 000（约 0.22 kbit/s）
11  200 000（约 0.44 kbit/s）
12  500 000（约 1.11 kbit/s）
13  1000 000（约 2.2 kbit/s）
14  2 000 000（约 4.4 kbit/s）
15  5 000 000（约 11.1 kbit/s）
16  10 000 000（约 22 kbit/s）
17  20 000 000（约 44 kbit/s）
18  50 000 000（约 111 kbit/s）
31  尽力而为
<err>            错误码。更多详情请参考第 15.4 章。

SDU 大小 延迟类别 平均传输延迟 95 百分位
128 八位组
1（可预测）  < 0.5 < 1.5
2（可预测） < 5 < 25
3（可预测） < 50 < 250
4（尽力而为） 未指定 -
1024 八位组
1（可预测）  < 0.5 < 1.5
2（可预测） < 5 < 25
3（可预测） < 50 < 250
4（尽力而为） 未指定 -

## 10.4. AT+CGQMIN  服务质量配置文件（最小可接受）(Quality of Service Profile (Minimum Acceptable))

该命令允许 TE 指定一个最小可接受配置文件，当 PDP 上下文被激活时，MT 会将协商后的配置文件与最小可接受配置文件进行比对检查。该写入命令为上下文标识参数 <cid> 所标识的上下文指定一个配置文件。

写入命令的一种特殊形式 AT+CGQMIN=<cid> 会使上下文编号 <cid> 的最小可接受配置文件变为未定义。在这种情况下，将不会对协商后的配置文件进行任何检查。该读取命令返回每个已定义上下文的当前设置。详细信息可参见 3GPP TS 23.107。

参数

AT+CGQMIN  服务质量配置文件（最小可接受）(Quality of Service Profile (Minimum Acceptable))

测试命令

AT+CGQMIN=?

响应

+CGQMIN: <PDP_type>,(range of supported <precedence>s),(range of supported <delay>s),(range of supported <reliability>s),(range of supported <peak>s),(range of supported <mean>s)

OK

读取命令

AT+CGQMIN?

响应

+CGQMIN: [<cid>,<precedence>,<delay>,<reliability>,<peak>,<mean>]
[+CGQMIN: <cid>,<precedence>,<delay>,<reliability>,<peak>,<mean>]
[…]

OK

写入命令

AT+CGQMIN=<cid>[,<precedence>[,<delay>[,<reliability>[,<peak>[,<mean>]]]]]

响应

OK

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性 命令立即生效。

配置将自动保存。

参考

3GPP TS 27.007

<cid>        整型。指定特定的 PDP 上下文定义（参见 AT+CGDCONT）。
<PDP_type>     字符串类型。分组数据协议类型。
                "IP"    IPv4。因特网协议（IETF STD 5）。
                "PPP"
                "IPV6"
                "IPV4V6"
<precedence> 整型。指定优先级类别。
                 0     网络订阅值
                 1     高优先级。业务承诺应优先于优先级类别 2 和 3 得到保障
                 2     普通优先级。业务承诺应优先于优先级类别 3 得到保障
                 3     低优先级。业务承诺应得到保障
<delay> 整型。指定延迟类别。该参数定义了 SDU 通过网络传输时产生的端到端传输延迟。详情请参考表 6。
                 0     网络订阅值
<reliability>     整型。指定可靠性类别。
0     网络订阅值
1     非实时业务，无法容忍数据丢失的对错误敏感的应用程序
2     非实时业务，可容忍偶发数据丢失的对错误敏感的应用程序
3     非实时业务，可容忍数据丢失的对错误敏感的应用程序，GMM/SM 和 SMS
4     实时业务，可容忍数据丢失的对错误敏感的应用程序
5     实时业务，可容忍数据丢失的对错误不敏感的应用程序
<peak>   整型。指定峰值吞吐量类别，单位为每秒八位组。
0     网络订阅值
     1     最高 1 000（8 kbit/s）
     2     最高 2 000（16 kbit/s）
     3     最高 4 000（32 kbit/s）
     4     最高 8 000（64 kbit/s）
     5     最高 16 000（128 kbit/s）
     6     最高 32 000（256 kbit/s）
     7     最高 64 000（512 kbit/s）
     8     最高 128 000（1024 kbit/s）
     9     最高 256 000（2048 kbit/s）
<mean>        整型。指定平均吞吐量类别，单位为每小时八位组。
                 0     网络订阅值
                 1     100（约 0.22 bit/s）
                 2     200（约 0.44 bit/s）
     3     500（约 1.11 bit/s）
     4     1 000（约 2.2 bit/s）
     5     2 000（约 4.4 bit/s）
     6     5 000（约 11.1 bit/s）

## 10.5. AT+CGEQREQ  UMTS 服务质量配置文件（请求）(UMTS Quality of Service Profile (Requested))

该命令允许 TE 指定当 MT 激活 PDP 上下文时使用的 UMTS 服务质量配置文件。详细信息可参见 3GPP TS 23.107。

     7     10 000（约 22 bit/s）
     8     20 000（约 44 bit/s）
     9     50 000（约 111 bit/s）
     10    100 000（约 0.22 kbit/s）
     11    200 000（约 0.44 kbit/s）
     12    500 000（约 1.11 kbit/s）
     13    1000 000（约 2.2 kbit/s）
     14    2 000 000（约 4.4 kbit/s）
     15    5 000 000（约 11.1 kbit/s）
     16    10 000 000（约 22 kbit/s）
     17    20 000 000（约 44 kbit/s）
     18    50 000 000（约 111 kbit/s）
     31    尽力而为
<err>        错误码。更多详情请参考第 15.4 章。

AT+CGEQREQ  UMTS 服务质量配置文件（请求）(UMTS Quality of Service Profile (Requested))

测试命令

AT+CGEQREQ=?

响应

+CGEQREQ: <PDP_type>,(range of supported <Traffic class>s),(range of supported <Maximum bitrate UL>s),(range of supported <Maximum bitrate DL>s),(range of supported <Guaranteed bitrate UL>s),(range of supported <Guaranteed bitrate DL>s),(range of supported <Delivery order>s),(list of supported <Maximum SDU size>s),(list of supported <SDU error ratio>s),(list of supported <Residual bit error ratio>s),(range of supported <Delivery of erroneous SDUs>s),(list of supported <Transfer delay>s),(range of supported <Traffic handling priority>s),(list of supported <Source statistics descriptor>s),(list of supported <Signalling indication>s)

OK

读取命令

AT+CGEQREQ?

响应

+CGEQREQ: [<cid>,<Traffic class>,<Maximum bitrate UL>,<Maximum bitrate DL>,<Guaranteed bitrate UL>,<Guaranteed bitrate DL>,<Delivery order>,<Maximum SDU size>,<SDU error ratio>,<Residual bit error ratio>,<Delivery of erroneous SDUs>,<Transfer delay>,<Traffic handling priority>,<Source statistics descriptor>,<Signalling indication>]
[...]

OK

写入命令

AT+CGEQREQ=[<cid>[,<Traffic class>[,<Maximum bitrate UL>[,<Maximum bitrate DL>[,<Guaranteed bitrate UL>[,<Guaranteed bitrate DL>[,<Delivery order>[,<Maximum SDU size>[,<SDU error ratio>[,<Residual bit error ratio>[,<Delivery of erroneous SDUs>[,<Transfer delay>[,<Traffic handling priority>[,<Source statistics descriptor>[,<Signalling indication>]]]]]]]]]]]]]]]

响应

OK

或

ERROR

最大响应时间 300 ms

特性 命令立即生效。

配置将自动保存。

参考

3GPP TS 27.007

<cid> 整型。PDP 上下文标识符，一个用于指定特定 PDP 上下文定义的数值参数。该参数仅在 TE-MT 接口本地有效，并用于其他与 PDP 上下文相关的命令。允许取值的范围（最小值 = 1）由命令的测试形式返回。
<PDP_type>                   字符串类型。分组数据协议类型，一个用于指定分组数据协议类型的字符串参数。
"IP"  IPv4。因特网协议（IETF STD 5）
"PPP"
"IPV6"
"IPV4V6"
以下参数定义于 3GPP TS 23.107。
<Traffic class>                整型。指示 UMTS 承载业务为其优化的应用程序类型（参考 3GPP TS 24.008 子条款 10.5.6.5）。如果该参数指定为会话类或流类，则还应提供保证比特率和最大比特率参数。
              0   会话类
              1   流类
              2   交互类
              3   后台类
              4   订阅值
<Maximum bitrate UL>         整型。指示在 SAP 处交付给 UMTS（上行链路业务）的最大 kbit/s 数量。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–11520
<Maximum bitrate DL>  整型。指示在 SAP 处由 UMTS（下行链路业务）交付的最大 kbit/s 数量。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–42200
<Guaranteed bitrate UL>       整型。指示在 SAP 处交付给 UMTS（上行链路业务）的保证 kbit/s 数量（前提是有数据可交付）。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–11520
<Guaranteed bitrate DL>       整型。指示在 SAP 处由 UMTS（下行链路业务）交付的保证 kbit/s 数量（前提是有数据可交付）。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–42200
<Delivery order>           整型。指示 UMTS 承载是否应提供顺序 SDU 交付（参考 3GPP TS 24.008 子条款 10.5.6.5）。
                              0  否
                              1  是
                              2  订阅值
<Maximum SDU size>   整型。(1,2,3,…) 指示以八位组为单位的最大允许 SDU 大小。如果该参数设置为 0，则将请求订阅值（参考 3GPP TS 24.008 子条款 10.5.6.5）。
0   订阅值
                              10–1520（该值必须能被 10 整除且无余数）
1520
<SDU error ratio>       字符串类型。指示丢失或被检测为错误的 SDU 比例的目标值。SDU 错误率仅针对一致性业务定义。该值以 "mEe" 形式指定。例如，目标 SDU 错误率 5 × 10-3 可指定为 "5E3"（例如 AT+CGEQREQ=…,"5E3",…）。
                              "0E0"  订阅值
                              "1E1"
"1E2"
"7E3"
            "1E3"
"1E4"
"1E5"
"1E6"
<Residual bit error ratio>  字符串类型。指示交付的 SDU 中未被检测到的误码率的目标值。如果未请求错误检测，则残余误码率指示交付的 SDU 中的误码率。该值以 "mEe" 形式指定。例如，目标残余误码率 5 × 10-3 可指定为 "5E3"（例如 AT+CGEQREQ=…,"5E3",…）。
"0E0"  订阅值
"5E2"
"1E2"
"5E3"
"4E3"
"1E3"
"1E4"
"1E5"
   "1E6"
   "6E8"
<Delivery of erroneous SDUs> 整型。指示检测为错误的 SDU 是否应被交付（参考 3GPP TS 24.008 子条款 10.5.6.5）。
                              0  否
                              1  是
                              2  不检测
                              3  订阅值
<Transfer delay>        整型。(0,1,2,…) 指示在一个 SAP 请求传输 SDU 到在另一个 SAP 交付之间的目标时间，单位为毫秒。如果该参数设置为 0，则将请求订阅值（参考 3GPP TS 24.008 子条款 10.5.6.5）。
                              0    订阅值
                              100–150（该值必须能被 10 整除且无余数）
200–950（该值必须能被 50 整除且无余数）
1000–4000（该值必须能被 100 整除且无余数）
<Traffic handling priority>     整型。(1,2,3,…) 指定与其他承载的 SDU 相比，处理属于该 UMTS 承载的所有 SDU 的相对重要性。如果该参数设置为 0，则将请求订阅值（参考 3GPP TS 24.008 子条款 10.5.6.5）。

## 10.6. AT+CGEQMIN  UMTS 服务质量配置文件（最小可接受）(UMTS Quality of Service Profile (Minimum Acceptable))

该命令允许 TE 指定一个最小可接受配置文件，MT 会将其与 PDP 上下文建立和 PDP 上下文修改流程中返回的协商配置文件进行比对检查。详细信息可参见 3GPP TS 23.107。

                              0  订阅值
                              1
2
3
<Source statistics descriptor> 整型。指定 PDP 上下文提交的 SDU 的源特性。
                              0  SDU 的特性未知
                              1  SDU 的特性与语音源相对应
<Signalling indication>        整型。指示 PDP 上下文提交的 SDU 的信令内容。
                              0  PDP 上下文未针对信令优化
                              1  PDP 上下文针对信令优化

AT+CGEQMIN  UMTS 服务质量配置文件（最小可接受）(UMTS Quality of Service Profile (Minimum Acceptable))

测试命令

AT+CGEQMIN=?

响应

+CGEQMIN: <PDP_type>,(range of supported <Traffic class>s),(range of supported <Maximum bitrate UL>s),(range of supported <Maximum bitrate DL>s),(range of supported <Guaranteed bitrate UL>s),(range of supported <Guaranteed bitrate DL>s),(range of supported <Delivery order>s),(list of supported <Maximum SDU size>s),(list of supported <SDU error ratio>s),(list of supported <Residual bit error ratio>s),(range of supported <Delivery of erroneous SDUs>s),(list of supported <Transfer delay>s),(range of supported <Traffic handling priority>s),(list of supported <Source statistics descriptor>s),(list of supported <Signalling indication>s)

OK

读取命令

AT+CGEQMIN?

响应

+CGEQMIN: [<cid>,<Traffic class>,<Maximum bitrate UL>,<Maximum bitrate DL>,<Guaranteed bitrate UL>,<Guaranteed bitrate DL>,<Delivery order>,<Maximum SDU size>,<SDU error ratio>,<Residual bit error ratio>,<Delivery of erroneous SDUs>,<Transfer delay>,<Traffic handling priority>,<Source statistics descriptor>,<Signalling indication>]

[…]

OK

写入命令

AT+CGEQMIN=[<cid>[,<Traffic class>[,<Maximum bitrate UL>[,<Maximum bitrate DL>[,<Guaranteed bitrate UL>[,<Guaranteed bitrate DL>[,<Delivery order>[,<Maximum SDU size>[,<SDU error ratio>[,<Residual bit error ratio>[,<Delivery of erroneous SDUs>[,<Transfer delay>[,<Traffic handling priority>[,<Source statistics descriptor>[,<Signalling indication>]]]]]]]]]]]]]]]

响应

OK

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性 命令立即生效。

配置将自动保存。

参考

3GPP TS 27.007

<cid> 整型。PDP 上下文标识符。一个用于指定特定 PDP 上下文定义的数值参数。该参数仅在 TE-MT 接口本地有效，并用于其他与 PDP 上下文相关的命令。允许取值的范围（最小值 = 1）由命令的测试形式返回。
<PDP_type>                 字符串类型。分组数据协议类型。一个用于指定分组数据协议类型的字符串参数。
"IP"  IPv4
"PPP"
"IPV6"
"IPV4V6"
以下参数定义于 3GPP TS 23.107。
<Traffic class>                整型。指示 UMTS 承载业务为其优化的应用程序类型（参考 3GPP TS 24.008 子条款 10.5.6.5）。如果该参数指定为会话类或流类，则还应提供保证比特率和最大比特率参数。
              0  会话类
              1  流类
              2  交互类
              3  后台类
              4  订阅值
<Maximum bitrate UL>         整型。指示在 SAP 处交付给 UMTS（上行链路业务）的最大 kbit/s 数量。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–11520
<Maximum bitrate DL>  整型。指示在 SAP 处由 UMTS（下行链路业务）交付的最大 kbit/s 数量。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–42200
<Guaranteed bitrate UL>      整型。指示在 SAP 处交付给 UMTS（上行链路业务）的保证 kbit/s 数量（前提是有数据可交付）。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–11520
<Guaranteed bitrate DL>       整型。指示在 SAP 处由 UMTS（下行链路业务）交付的保证 kbit/s 数量（前提是有数据可交付）。例如，32 kbit/s 的比特率可指定为 32（例如 AT+CGEQREQ=…,32,…）。
                              0  订阅值
                              1–42200
<Delivery order>          整型。指示 UMTS 承载是否应提供顺序 SDU 交付（参考 3GPP TS 24.008 子条款 10.5.6.5）。
                              0  否
                              1  是
                              2  订阅值
<Maximum SDU size>   整型。(1,2,3,…) 指示以八位组为单位的最大允许 SDU 大小。如果该参数设置为 0，则将请求订阅值（参考 3GPP TS 24.008 子条款 10.5.6.5）。
                              0   订阅值
                              10–1520（该值必须能被 10 整除且无余数）
1502
<SDU error ratio>       字符串类型。指示丢失或被检测为错误的 SDU 比例的目标值。SDU 错误率仅针对一致性业务定义。该值以 "mEe" 形式指定。例如，目标 SDU 错误率 5 × 10-3 可指定为 "5E3"（例如 AT+CGEQREQ=…,"5E3",…）。
                             "0E0"  订阅值
                              "1E2"
"7E3"
"1E3"
"1E4"
"1E5"
"1E6"
"1E1"
<Residual bit error ratio>      字符串类型。指示交付的 SDU 中未被检测到的误码率的目标值。如果未请求错误检测，则残余误码率指示交付的 SDU 中的误码率。该值以 "mEe" 形式指定。例如，目标残余误码率 5 × 10-3 可指定为 "5E3"（例如 AT+CGEQREQ=…,"5E3",…）。
"0E0"  订阅值
"5E2"
"1E2"
"5E3"
"4E3"
"1E3"
"1E4"
"1E5"
"1E6"
   "6E8"
<Delivery of erroneous SDUs> 整型。指示检测为错误的 SDU 是否应被交付（参考 3GPP TS 24.008 子条款 10.5.6.5）。
                              0  否
                              1  是
                              2  不检测
                              3  订阅值
<Transfer delay>        整型。指示在一个 SAP 请求传输 SDU 到在另一个 SAP 交付之间的目标时间，单位为毫秒。如果该参数设置为 0，则将请求订阅值（参考 3GPP TS 24.008 子条款 10.5.6.5）。
                              0    订阅值
                              100–150（该值必须能被 10 整除且无余数）
200–950（该值必须能被 50 整除且无余数）
1000–4000（该值必须能被 100 整除且无余数）
<Traffic handling priority>     整型。指定与其他承载的 SDU 相比，处理属于该 UMTS 承载的所有 SDU 的相对重要性。如果该参数设置为 0，则将请求订阅值（参考 3GPP TS 24.008 子条款 10.5.6.5）。

## 10.7. AT+CGACT  激活或去激活 PDP 上下文 (Activate or Deactivate PDP Context)

该写入命令激活或去激活指定的 PDP 上下文。命令完成后，MT 仍保持 V.250 命令状态。如果任何 PDP 上下文已处于所请求的状态，则该上下文的状态保持不变。如果执行命令的激活形式时 MT 尚未进行 PS 附着，则 MT 首先执行 PS 附着，然后尝试激活指定的上下文。如果激活/去激活形式的命令未指定任何 <cid>，则它将激活或去激活所有已定义的上下文。

范围：0–3。默认值：0。

<Source statistics descriptor>  整型。指定 PDP 上下文提交的 SDU 的源特性。
                              0  SDU 的特性未知
                              1  SDU 的特性与语音源相对应
<Signalling indication>        整型。指示 PDP 上下文提交的 SDU 的信令内容。
                              0  PDP 上下文未针对信令优化
                              1  PDP 上下文针对信令优化
<err>                         错误码。更多详情请参考第 15.4 章。

AT+CGACT  激活或去激活 PDP 上下文 (Activate or Deactivate PDP Context)

测试命令

AT+CGACT=?

响应

+CGACT: (list of supported <state>s)

OK

读取命令

AT+CGACT?

响应

+CGACT: <cid>,<state>
[+CGACT: <cid>,<state>
…]

OK

写入命令

AT+CGACT=<state>,<cid>

响应

OK

或

NO CARRIER

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 150 s，由网络决定。

特性 命令是否生效由网络决定。

配置不会被保存。

参数

示例

AT+CGDCONT=1,"IP","UNINET"   //定义 PDP 上下文。
OK
AT+CGACT=1,1       //激活 PDP。
OK
AT+CGACT=0,1       //去激活 PDP。
OK

## 10.8. AT+CGDATA  进入数据状态 (Enter Data State)

该写入命令使 MT 执行使用一种或多种分组域 PDP 类型在 TE 与网络之间建立通信所需的任何操作。这可能包括执行 PS 附着以及一个或多个 PDP 上下文激活。AT 命令行中位于 AT+CGDATA 之后的任何命令都不会被 MT 处理。

如果 <L2P> 值不被 MT 接受，则 MT 应返回 ERROR 或 +CME ERROR 响应。否则，MT 发出中间结果码 CONNECT 并进入 V.250 在线数据状态。数据传输完成后，且第 2 层协议终止流程已成功完成后，将重新进入命令状态，MT 返回最终结果码 OK。

参考

3GPP TS 27.007

<state>  整型。指示 PDP 上下文激活状态。
   0  去激活
   1  激活
   其他值为保留值，执行写入命令时将返回 ERROR 响应
<cid>      整型。指定特定的 PDP 上下文定义（参见 AT+CGDCONT）。
<err>       错误码。更多详情请参考第 15.4 章。

AT+CGDATA  进入数据状态 (Enter Data State)

测试命令

AT+CGDATA=?

响应

+CGDATA: (list of supported <L2P>s)

OK

写入命令

AT+CGDATA=<L2P>[,<cid>[,<cid>[,…]]]

响应

CONNECT

或

参数

## 10.9. AT+CGPADDR  显示 PDP 地址 (Show PDP Address)

该写入命令返回指定上下文标识符的 PDP 地址列表。如果未指定 <cid>，则返回所有已定义上下文的地址。

或

ERROR

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性 命令是否生效由网络决定。

配置不会被保存。

参考

3GPP TS 27.007

<L2P>    字符串类型。指示 TE 与 MT 之间使用的第 2 层协议：
      PPP  用于 IP 等 PDP 的点对点协议
    其他值不受支持，执行命令时将返回 ERROR 响应
<cid> 整型。指定特定的 PDP 上下文定义（参见 AT+CGDCONT）。
<err>      错误码。更多详情请参考第 15.4 章。

AT+CGPADDR  显示 PDP 地址 (Show PDP Address)

测试命令

AT+CGPADDR=?

响应

+CGPADDR: (list of defined <cid>s)

OK

写入命令

AT+CGPADDR[=<cid>[,<cid>[,…]]]

响应

+CGPADDR: <cid>,<PDP_addr>
[+CGPADDR: <cid>,<PDP_addr>
…]

OK

或

ERROR

最大响应时间 300 ms

特性 命令是否生效由网络决定。

参数

示例

AT+CGDCONT=1,"IP","UNINET"   //定义 PDP 上下文。
OK
AT+CGACT=1,1       //激活 PDP。
OK
AT+CGPADDR=1       //显示 PDP 地址。
+CGPADDR: 1,"10.76.51.180"

OK

## 10.10. AT+CGCLASS  GPRS 移动台类别 (GPRS Mobile Station Class)

该命令设置 MT 按照指定的操作模式运行。参见 3GPP TS 23.060。

配置不会被保存。

参考

3GPP TS 27.007

<cid>   整型。指定特定的 PDP 上下文定义（参见 AT+CGDCONT）。
<PDP_addr>    字符串类型。标识 MT 在 PDP 适用地址空间中的地址。该地址可以是静态的，也可以是动态的。对于静态地址，它将是定义上下文时由 AT+CGDCONT 设置的地址。对于动态地址，它将是使用 <cid> 引用的上下文定义的上一次 PDP 上下文激活期间分配的地址。如果没有可用地址，则省略 <PDP_address>。

AT+CGCLASS  GPRS 移动台类别 (GPRS Mobile Station Class)

测试命令

AT+CGCLASS=?

响应

+CGCLASS: (list of supported <class>s)

OK

读取命令

AT+CGCLASS?

响应

+CGCLASS: <class>

OK

写入命令

AT+CGCLASS=<class>

响应

OK

参数

## 10.11. AT+CGREG  网络注册状态 (Network Registration Status)

该命令查询网络注册状态，并控制主动上报结果码的呈现：当 <n>=1 且 MT 在 GERAN/UTRAN 中的 GPRS 网络注册状态发生变化时，上报 +CGREG: <stat>；当 <n>=2 且 GERAN/UTRAN 中的网络小区发生变化时，上报主动上报结果码 +CGREG: <stat>[,[<lac>],[<ci>],[<AcT>]]。

或

ERROR

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性 命令立即生效。

配置将自动保存。

参考

3GPP TS 27.007

<class>    字符串类型。指示 GPRS 移动类别（功能按降序排列）
            "A"   A 类
<err>         错误码。更多详情请参考第 15.4 章。

AT+CGREG  网络注册状态 (Network Registration Status)

测试命令

AT+CGREG=?

响应

+CGREG: (list of supported <n>s)

OK

读取命令

AT+CGREG?

响应

+CGREG: <n>,<stat>[,<lac>,<ci>[,<AcT>]]

OK

写入命令

AT+CGREG[=<n>]

响应

OK

或

ERROR

最大响应时间 300 ms

特性 命令立即生效。

参数

示例

AT+CGREG=2
OK
AT+CGATT=0
OK
配置将自动保存。

参考

3GPP TS 27.007

<n>   整型。控制指定 URC 的呈现。
   0 禁用网络注册主动上报结果码
   1 启用网络注册主动上报结果码 +CGREG: <stat>
   2 启用网络注册及位置信息主动上报结果码 +CGREG: <stat>[,<lac>,<ci>[,<AcT>]]
<stat>     整型。网络注册状态。
   0 未注册。MT 当前未在搜索要注册的运营商。UE 处于 GMM 状态 GMM-NULL 或 GMM-DEREGISTERED-INITIATED。GPRS 业务被禁用，但如果用户请求，允许 UE 为 GPRS 进行附着。
   1 已注册，归属网络。UE 在归属 PLMN 上处于 GMM 状态 GMM-REGISTERED 或 GMM-ROUTING-AREA-UPDATING-INITIATED。
            2 未注册，但 MT 当前正尝试附着或搜索要注册的运营商。UE 处于 GMM 状态 GMM-DEREGISTERED 或 GMM-REGISTERED-INITIATED。GPRS 业务已启用，但当前没有可用的允许 PLMN。一旦有允许的 PLMN 可用，UE 将启动 GPRS 附着。
   3 注册被拒绝。UE 处于 GMM 状态 GMM-NULL。GPRS 业务被禁用，如果用户请求，不允许 UE 为 GPRS 进行附着。
   4 未知
   5 已注册，漫游
<lac>       字符串类型。十六进制格式的双字节位置区码（例如 "00C3" 等于十进制的 195）。
<ci>       字符串类型。十六进制格式的 16 位（GSM）或 28 位（UMTS/LTE）小区 ID。
<AcT>      整型。选择的接入技术。
0 GSM
2 UTRAN
3 GSM W/EGPRS
4 UTRAN W/HSDPA
5 UTRAN W/HSUPA
6 UTRAN W/HSDPA 和 HSUPA
            7 E-UTRAN

+CGREG: 2
AT+CGATT=1
OK

+CGREG: 1,"D504","80428B5",7

## 10.12. AT+CGEREP  分组域事件上报 (Packet Domain Event Reporting)

该写入命令启用或禁用在分组域 MT 或网络中出现某些事件时，MT 向 TE 发送主动上报结果码 +CGEV: XXX。<mode> 控制本命令中指定的主动上报结果码的处理方式。<bfr> 控制当 <mode>=1 或 2 时对缓存结果码的影响。

参数

AT+CGEREP  分组域事件上报 (Packet Domain Event Reporting)

测试命令

AT+CGEREP=?

响应

+CGEREP: (range of supported <mode>s),(list of supported <bfr>s)

OK

读取命令

AT+CGEREP?

响应

+CGEREP: <mode>,<bfr>

OK

写入命令

AT+CGEREP=<mode>[,<bfr>]

响应

OK

或

ERROR

执行命令

AT+CGEREP

响应

OK

最大响应时间 300 ms

特性 命令立即生效。

配置将自动保存。

参考

3GPP TS 27.007

<mode>  整型。控制本命令中指定的主动上报结果码的处理方式。

主动上报结果码及对应事件定义如下：
1. +CGEV: REJECT <PDP_type>, <PDP_addr>: 当 MT 无法通过 +CRING 主动上报结果码向 TE 报告网络对 PDP 上下文激活的请求时发生，并被自动拒绝。
注意：该事件不适用于 EPS。
2. +CGEV: NW REACT <PDP_type>, <PDP_addr>,[<cid>]: 网络已请求重新激活上下文。如果 MT 知道用于重新激活上下文的 <cid>，则提供该值。
注意：该事件不适用于 EPS。
3. +CGEV: NW DEACT <PDP_type>, <PDP_addr>,[<cid>]: 网络已强制去激活上下文。如果 MT 知道用于激活上下文的 <cid>，则提供该值。
4. +CGEV: ME DEACT <PDP_type>, <PDP_addr>,[<cid>]: 移动设备已强制去激活上下文。如果 MT 知道用于激活上下文的 <cid>，则提供该值。
5. +CGEV: NW DETACH: 网络已强制进行分组域去附着。这意味着所有激活的上下文都已被去激活。这些不会分别上报。
6. +CGEV: ME DETACH: 移动设备已强制进行分组域去附着。这意味着所有激活的上下文都已被去激活。这些不会分别上报。
7. +CGEV: NW CLASS <class>: 网络已强制更改 MS 类别。上报最高可用类别（参见 AT+CGCLASS）。
8. +CGEV: ME CLASS <class>: 移动设备已强制更改 MS 类别。上报最高可用类别（参见 AT+CGCLASS）。
9. +CGEV: PDN ACT <cid>: 已激活一个上下文。该上下文表示 LTE 中的 PDN 连接或 GSM/UMTS 中的主 PDP 上下文。
10. +CGEV: PDN DEACT <cid>: 已去激活一个上下文。该上下文表示 LTE 中的 PDN 连接或 GSM/UMTS 中的主 PDP 上下文。

0 在 MT 中缓存主动上报结果码；如果 MT 结果码缓冲区已满，可丢弃最早的结果码。不会将任何结果码转发给 TE。
1 当 MT-TE 链路被占用（例如处于在线数据模式）时丢弃主动上报结果码，否则直接将它们转发给 TE。
2 当 MT-TE 链路被占用（例如处于在线数据模式）时，在 MT 中缓存主动上报结果码，并在 MT-TE 链路变为可用时将缓存的结果码转发给 TE。否则直接将它们转发给 TE。

<bfr>  整型。控制对缓存结果码的影响。
0 当指定 <mode> 1 或 2 时，清除本命令中定义的 MT 主动上报结果码缓冲区。
1 当指定 <mode> 1 或 2 时，将本命令中定义的 MT 主动上报结果码缓冲区转发给 TE（在转发结果码之前应给出 OK 响应）。

注意

示例

AT+CGEREP=?
+CGEREP: (0-2),(0,1)

OK
AT+CGEREP?
+CGEREP: 0,0

OK

## 10.13. AT+CGSMS  选择 MO SMS 消息的业务 (Select Service for MO SMS Messages)

该命令指定 MT 用于发送 MO（移动台发起）SMS 消息的业务或业务偏好。

参数

AT+CGSMS  选择 MO SMS 消息的业务 (Select Service for MO SMS Messages)

测试命令

AT+CGSMS=?

响应

+CGSMS: (range of supported <service>s)

OK

读取命令

AT+CGSMS?

响应

+CGSMS: <service>

OK

写入命令

AT+CGSMS=[<service>]

响应

OK

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性

参考

3GPP TS 27.007

<service> 整型。指示要使用的业务或业务偏好。
   0 GPRS
   1 电路交换
   2 GPRS 优先（如果 GPRS 不可用则使用电路交换）
   3 电路交换优先（如果电路交换不可用则使用 GPRS）
<err>      错误码。更多详情请参考第 15.4 章。

## 10.14. AT+CEREG  EPS 网络注册状态 (EPS Network Registration Status)

该命令查询网络注册状态，并控制主动上报结果码的呈现：当 <n>=1 且 MT 在 E-UTRAN 中的 EPS 网络注册状态发生变化时，上报 +CEREG: <stat>；当 <n>=2 且 E-UTRAN 中的网络小区发生变化时，上报主动上报结果码 +CEREG: <stat>[,[<tac>],[<ci>],[<AcT>]]。

参数

AT+CEREG  EPS 网络注册状态 (EPS Network Registration Status)

测试命令

AT+CEREG=?

响应

+CEREG: (list of supported <n>s)

OK

读取命令

AT+CEREG?

响应

+CEREG: <n>,<stat>[,<tac>,<ci>[,<AcT>]]

OK

写入命令

AT+CEREG[=<n>]

响应

OK

或

ERROR

最大响应时间 300 ms

特性

参考

3GPP TS 27.007

<n>  整型。控制主动上报结果码 +CEREG: <stat> 的呈现。
   0 禁用网络注册主动上报结果码
   1 启用网络注册主动上报结果码 +CEREG: <stat>
   2 启用网络注册及位置信息主动上报结果码 +CEREG: <stat>[,<tac>,<ci>[,<AcT>]]
<stat> 整型。
   0 未注册。MT 当前未在搜索要注册的运营商
   1 已注册，归属网络
   2 未注册，但 MT 当前正尝试附着或搜索要注册的运营商
   3 注册被拒绝
   4 未知
   5 已注册，漫游
<tac> 字符串类型。十六进制格式的双字节跟踪区码。
<ci> 字符串类型。十六进制格式的 28 位 E-UTRAN 小区 ID。
<AcT> 整型。选择的接入技术。
   0 GSM
   2 UTRAN
   3 GSM W/EGPRS
   4 UTRAN W/HSDPA
   5 UTRAN W/HSUPA
   6 UTRAN W/HSDPA 和 HSUPA
   7 E-UTRAN

## 10.15. AT+QGDCNT  分组数据计数器 (Packet Data Counter)

该命令允许应用程序查看模块发送或接收了多少字节。

AT+QGDCNT  分组数据计数器 (Packet Data Counter)

测试命令

AT+QGDCNT=?

响应

+QGDCNT: (list of supported <op>s)

OK

读取命令

AT+QGDCNT?

响应

+QGDCNT: <bytes_sent>,<bytes_recv>

OK

写入命令

AT+QGDCNT=<op>

响应

OK

或

ERROR

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性 命令是否生效由网络决定。

配置不会被保存。

参数

<op> 整型。与数据计数器相关的操作。
0 重置数据计数器
1 将数据计数器的结果保存到 NVM
如果需要自动保存结果，请参考 AT+QAUGDCNT。
<bytes_sent> 整型。已发送的字节数。
<bytes_recv> 整型。已接收的字节数。
<err> 错误码。更多详情请参考第 15.4 章。

当 MT 上电时，<bytes_sent> 和 <bytes_recv> 从 NVM 中的数据计数器结果加载。NVM 中的默认结果为 0。

示例

AT+QGDCNT=?      //测试命令。
+QGDCNT: (0,1)

OK
AT+QGDCNT?  //查询当前发送和接收的字节数。
+QGDCNT: 3832,4618

OK
AT+QGDCNT=1  //将结果保存到 NVM。
OK
AT+QGDCNT=0  //重置数据计数器。
OK

## 10.16. AT+QAUGDCNT  自动保存分组数据计数器 (Auto Save Packet Data Counter)

该命令允许 AT+QGDCNT 自动将结果保存到 NVM。

AT+QAUGDCNT  自动保存分组数据计数器 (Auto Save Packet Data Counter)

测试命令

AT+QAUGDCNT=?

响应

+QAUGDCNT: (list of supported <value>s)

OK

读取命令

AT+QAUGDCNT?

响应

+QAUGDCNT: <value>

注意

参数

<value> 整型。该参数是 AT+QGDCNT 自动将结果保存到 NV 的时间间隔。范围：0, 30–65535。默认值：0。单位：秒。如果设置为 0，则禁用自动保存功能。
<err> 错误码。更多详情请参考第 15.4 章。

示例

AT+QAUGDCNT=?      //测试命令。
+QAUGDCNT: (0,30-65535)

OK
AT+QGDCNT=35   //将 <value> 设置为 35。
OK
AT+QAUGDCNT?  //查询自动保存的时间间隔。
+QAUGDCNT: 35

OK

写入命令

AT+QAUGDCNT=<value>

响应

OK

或

ERROR

如果出现与 ME 功能相关的任何错误：

+CME ERROR: <err>

最大响应时间 300 ms

特性 命令是否生效由网络决定。

配置不会被保存。

## 10.17. AT$QCRMCALL  启动或停止 RmNet 呼叫 (Start or Stop an RmNet Call)

该命令根据 <action> 参数触发 RmNet 呼叫，通常是启动 RmNet 呼叫或停止 RmNet 呼叫。

AT$QCRMCALL  启动或停止 RmNet 呼叫 (Start or Stop an RmNet Call)

测试命令

AT$QCRMCALL=?

响应

$QCRMCALL: (list of supported <action>s),(range of supported <instance>s),(range of supported <IP_type>s),(list of supported <tech_pref>s),(list of supported <call_type>s),,

OK

读取命令

AT$QCRMCALL?

响应

如果已建立 RmNet 呼叫：
$QCRMCALL: <instance>,<call_Type>

OK

或

ERROR

写入命令

AT$QCRMCALL=<action>,<instance>[,<IP_type>[,<tech_pref>[,<profile_num>]]]

响应

OK

或

ERROR

最大响应时间

特性 /

参数

<action> 整型。
0 停止 RmNet 呼叫
1 启动 RmNet 呼叫
<instance> 整型。当前该参数只能设置为 1。
<IP_type> 整型。
1 呼叫类型为 IPV4
2 呼叫类型为 IPV6
3 呼叫类型为 IPV4V6
<tech_pref> 整型。
1 3GPP2(CMDA/HDR/EHPRD)
2 3GPP(GSM/WCDMA/LTE/TDS-CDMA)
<profile_num> 整型。范围：1–24, 100–179。
<call_type> 字符串类型。
V4 IPv4 呼叫
V6 IPv6 呼叫

示例

AT$QCRMCALL=?      //测试命令。
$QCRMCALL: (0,1),(1,2,3,4,5,6,7,8),(1-3),(1-2),(1-24,100-179),,

OK
AT$QCRMCALL=1,1,1,2,1    //启动一个 IPv4 RmNet 呼叫。
$QCRMCALL: 1,V4

OK
AT$QCRMCALL?
$QCRMCALL: 1,V4

OK

## 10.18. AT+QNETDEVSTATUS  查询 RmNet 设备状态 (Query RmNet Device Status)

该命令可以查询 RmNet 设备状态。

参数

<on_off> 整型。
0 禁用 RmNet 设备状态 URC
1 启用 RmNet 设备状态 URC
<state> 整型。
0 启用 RmNet 设备状态 URC
1 RmNet 呼叫已就绪，MCU 可通过 DHCP 或 QMI 获取 IP 地址
2 RmNet 呼叫已连接

AT+QNETDEVSTATUS  查询 RmNet 设备状态 (Query RmNet Device Status)

测试命令

AT+QNETDEVSTATUS=?

响应

+QNETDEVSTATUS: (list of supported <on_off>s)

OK

读取命令

AT+QNETDEVSTATUS?

响应

如果存在 RmNet 呼叫，将包含 <state>、<IP_type> 和 <instance>。
+QNETDEVSTATUS: <on_off>[,<state>[,<IP_type>[,<instance>]]]

OK

写入命令

AT+QNETDEVSTATUS=<on_off>

响应

OK

或

ERROR

最大响应时间 300 ms

特性 /

<IP_type> 整型。
4 IPv4 呼叫
6 IPv6 呼叫
其他值无效。
<instance> 整型。RmNet 呼叫实例。始终为 1。

当模块成功从网络获取 IP 地址后，<state> 将变为 1，并且模块将保留 IP 地址 2 分钟，以等待 MCU 通过 DHCP 或 QMI 从模块请求 IP 地址。如果模块在 2 分钟内未收到 IP 地址请求，模块将断开 RmNet 呼叫。

示例

AT+QNETDEVSTATUS=?   //测试命令。
+QNETDEVSTATUS: (0,1)

OK
AT+QNETDEVSTATUS?    //查询命令。
+QNETDEVSTATUS: 0

OK
AT+QNETDEVSTATUS=1   //启用 RmNet 设备状态 URC。
OK
AT+QNETDEVSTATUS?    //查询命令。
+QNETDEVSTATUS: 1

OK
AT$QCRMCALL=1,1,1,2,1   //启动一个 IPv4 RmNet 呼叫。
$QCRMCALL: 1,4

OK

+QNETDEVSTATUS: 1,1,4,1   //RmNet 呼叫已就绪 URC。

+QNETDEVSTATUS: 1,2,4,1   //MCU 从模块获取 IP 地址。

AT+QNETDEVSTATUS?    //查询当前配置。
+QNETDEVSTATUS: 1,2,4,1

OK
AT$QCRMCALL=0,1,1,2,1   //停止一个 IPv4 RmNet 呼叫。
OK
注意

+QNETDEVSTATUS: 1,0,4,1   //模块上报 RmNet 呼叫断开 URC。
AT+QNETDEVSTATUS?    //查询当前配置。
+QNETDEVSTATUS: 1

OK

## 10.19. AT+CGCONTRDP  读取 PDP 上下文动态参数 (PDP Context Read Dynamic Parameters)

AT+CGCONTRDP  读取 PDP 上下文动态参数 (PDP Context Read Dynamic Parameters)

测试命令

AT+CGCONTRDP=?

响应

+CGCONTRDP: (list of supported <cid>s)

OK

写入命令

AT+CGCONTRDP[=<cid>]

响应

+CGCONTRDP: <cid>,<bearer_id>,<APN>[,<local_addr and subnet_mask>[,<gw_addr>[,<DNS_prim_addr>[,<DNS_sec_addr>[,<P-CSCF_prim_addr>[,<P-CSCF_sec_addr>[,<IM_CN_Signalling_Flag>[,<LIPA_indication>[,<IPv4_MTU>[,<WLAN_Offload>[,<Local_Addr_Ind>[,<Non-IP_MTU>[,<Serving_PLMN_rate_control_value>]]]]]]]]]]]]]]

[+CGCONTRDP: <cid>,<bearer_id>,<APN>[,<local_addr and subnet_mask>[,<gw_addr>[,<DNS_prim_addr>[,<DNS_sec_addr>[,<P-CSCF_prim_addr>[,<P-CSCF_sec_addr>[,<IM_CN_Signalling_Flag>[,<LIPA_indication>[,<IPv4_MTU>[,<WLAN_Offload>[,<Local_Addr_Ind>[,<Non-IP_MTU>[,<Serving_PLMN_rate_control_value>]]]]]]]]]]]]]]

[...]

OK

或

ERROR

最大响应时间 300 ms

特性 /

参数

<cid> 整型。指定特定的非次级 PDP 上下文定义。该参数仅在 TE-MT 接口本地有效，并用于其他与 PDP 上下文相关的命令。
<bearer_id> 整型。标识承载，即 EPS 中的 EPS 承载和 UMTS/GPRS 中的 NSAPI。
1 RmNet 呼叫已就绪，MCU 可通过 DHCP 或 QMI 获取 IP 地址
2 RmNet 呼叫已连接
<APN> 字符串类型。用于选择 GGSN 或外部分组数据网络的逻辑名称。
<local_addr and subnet_mask> 字符串类型。显示 MT 的 IP 地址和子网掩码。该字符串以点分隔的数字（0–255）参数形式给出：IPv4 为 "a1.a2.a3.a4.m1.m2.m3.m4"，IPv6 为 "a1.a2.a3.a4.a5.a6.a7.a8.a9.a10.a11.a12.a13.a14.a15.a16.m1.m2.m3.m4.m5.m6.m7.m8.m9.m10.m11.m12.m13.m14.m15.m16"。
<gw_addr> 字符串类型。显示 MT 的网关地址。该字符串以点分隔的数字（0–255）参数形式给出。
<DNS_prim_addr> 字符串类型。显示主 DNS 服务器的 IP 地址。
<DNS_sec_addr> 字符串类型。显示次 DNS 服务器的 IP 地址。
<P-CSCF_prim_addr> 字符串类型。显示主 P-CSCF 服务器的 IP 地址。
<P-CSCF_sec_addr> 字符串类型。显示次 P-CSCF 服务器的 IP 地址。
<IM_CN_Signalling_Flag> 整型。显示该 PDP 上下文是否仅用于 IM CN 子系统相关的信令。
0 PDP 上下文不仅用于 IM CN 子系统相关的信令
1 PDP 上下文仅用于 IM CN 子系统相关的信令
<LIPA_indication> 整型。指示该 PDP 上下文是否通过 LIPA PDN 连接提供连接。该参数不能由 TE 设置。
0 未收到该 PDP 上下文通过 LIPA PDN 连接提供连接的指示
1 已收到该 PDP 上下文通过 LIPA PDN 连接提供连接的指示
<IPv4_MTU> 整型。显示 IPv4 MTU 大小，单位为八位组。
<WLAN_Offload> 整型。指示是否可以通过 WLAN 使用指定 PDN 连接来分流业务。这指的是 3GPP TS 24.008 [8] 子条款 10.5.6.20 中规定的 WLAN offload 可接受性 IE 的第 1 和第 2 位。
0 处于 S1 模式或 Iu 模式时，通过 WLAN 分流 PDN 连接的业务不可接受。
1 处于 S1 模式时通过 WLAN 分流 PDN 连接的业务可接受，但在 Iu 模式下不可接受。
2 处于 Iu 模式时通过 WLAN 分流 PDN 连接的业务可接受，但在 S1 模式下不可接受。
3 处于 S1 模式或 Iu 模式时，通过 WLAN 分流 PDN 连接的业务均可接受。
<Local_Addr_Ind> 整型。指示 MS 和网络是否支持 TFT 中的本地 IP 地址（参见 3GPP TS 24.301 [83] 和 3GPP TS 24.008 [8] 子条款 10.5.6.3）。
0 指示 MS 或网络或两者均不支持 TFT 中的本地 IP 地址
1 指示 MS 和网络都支持 TFT 中的本地 IP 地址
<Non-IP_MTU> 整型。显示 Non-IP MTU 大小，单位为八位组。
<Serving_PLMN_rate_control_value> 整型。指示 UE 在 6 分钟时间间隔内允许发送的最大上行消息数。这指的是 3GPP TS 24.301 [8] 子条款 9.9.4.28 中规定的 Serving PLMN rate control IE 的第 3 至第 4 个八位组。
