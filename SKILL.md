---
name: quectel-at-commands-zh
description: "移远通信（Quectel）LTE 标准模组（EC2x 系列、EG9x 系列、EG2x-G、EM05 系列）AT 指令手册 V2.0 的中文参考。当用户通过串口、USB AT 口或 modem 口使用 Quectel EC25/EC21/EC20 R2.1/EG91/EG95/EG21-G/EG25-G/EM05 模组，需要查询 AT 指令语法、参数、响应、示例、CME/CMS 错误码或 URC 处理方式时使用。涵盖通用、串口接口、状态控制、(U)SIM、网络服务、通话、电话簿、短信、分组域、补充业务、音频、硬件以及 GNSS/DFOTA/FTP/HTTP/MMS/SMTP/TCPIP/SSL 等指令，并含出厂默认值与附录参考。当代码中涉及 pyserial、AT 指令交互，或引用 `AT+CGDCONT`、`AT+CGACT`、`AT+CMGF`、`AT+CMGS`、`AT+COPS`、`AT+CREG`、`AT+CSQ`、`AT+QPOWD`、`AT+CPIN`、`AT+QINDCFG`、`AT+QIACT` 等本手册内的 AT 指令时也会触发。"
metadata:
  version: "1.0"
  language: "zh-CN"
  source: "Quectel EC2x&EG9x&EG2x-G&EM05 Series AT Commands Manual V2.0 (2021-02-24)"
  applicable-modules: "EC25, EC21, EC20 R2.1, EG91, EG95, EG21-G, EG25-G, EM05"
---

# 移远通信 LTE 标准模组 AT 指令手册（中文版）

本手册是 Quectel LTE 标准模组官方 AT 指令手册 V2.0 的中文翻译整理版，适用模组：**EC2x 系列**（EC25、EC21、EC20 R2.1）、**EG9x 系列**（EG95、EG91）、**EG2x-G**（EG25-G、EG21-G）以及 **EM05 系列**。

每章内容分别存放在 `references/` 下的独立参考文件中。指令按 14 个功能章节划分，另附参考附录。

## 适用场景

- 通过串口 / USB AT 接口配置或调试 Quectel LTE 模组
- 查询 AT 指令的语法、参数或响应示例
- 处理 CME/CMS 错误码、URC（主动上报）、出厂默认值或参数保存
- 编写驱动 Quectel 模组的固件或脚本（Python `pyserial`、C、嵌入式）

## 使用方式

1. 根据指令的功能分类，打开下方对应的参考文件。
2. 每条指令包含：指令名称与类型（测试/读取/写入/执行）、语法、参数（下划线为默认值）、响应格式和示例。
3. 常见错误码、URC、字符集及默认值见 `references/15-appendix-references.md`。

### 参考文件

| 章节 | 文件 | 内容 |
| --- | --- | --- |
| 1 | `references/01-introduction.md` | 适用模组、语法、字符集、指令端口、URC、关机流程 |
| 2 | `references/02-general-commands.md` | ATI、AT+GMI/GMM/GMR、AT+CGMI/CGMM/CGMR、AT+GSN/CGSN、AT&F/V/W、ATZ、ATQ、ATV、ATE、A/、ATS3-5、ATX、AT+CFUN、AT+CMEE、AT+CSCS、AT+QURCCFG、AT+QAPRDYIND、AT+QDIAGPORT |
| 3 | `references/03-serial-interface-control-commands.md` | AT&C、AT&D、AT+IFC、AT+ICF、AT+IPR、AT+QRIR |
| 4 | `references/04-status-control-commands.md` | AT+CPAS、AT+CEER、AT+QINDCFG、AT+QMBNCFG |
| 5 | `references/05-usim-related-commands.md` | AT+CIMI、AT+CLCK、AT+CPIN、AT+CPWD、AT+CSIM、AT+CRSM、AT+QCCID、AT+QPINC、AT+QINISTAT、AT+QSIMDET、AT+QSIMSTAT、AT+QSIMVOL、AT+CCHO、AT+CGLA、AT+CCHC |
| 6 | `references/06-network-service-commands.md` | AT+COPS、AT+CREG、AT+CSQ、AT+CPOL、AT+COPN、AT+CTZU、AT+CTZR、AT+QLTS、AT+QNWINFO、AT+QSPN、AT+QNETINFO、AT+QNWLOCK、AT+QOPSCFG、AT+QOPS、AT+QFPLMNCFG、AT+QENG、AT+CIND |
| 7 | `references/07-call-related-commands.md` | ATA、ATD、ATH、AT+CVHU、AT+CHUP、+++、ATO、ATS0/6/7/8/10/12、AT+CBST、AT+CSTA、AT+CLCC、AT+CR、AT+CRC、AT+CRLP、AT+QECCNUM、AT+QHUP、AT+QCHLDIPMPTY、AT^DSCI |
| 8 | `references/08-phonebook-commands.md` | AT+CNUM、AT+CPBF、AT+CPBR、AT+CPBS、AT+CPBW |
| 9 | `references/09-short-message-service-commands.md` | AT+CSMS、AT+CMGF、AT+CSCA、AT+CPMS、AT+CMGD、AT+CMGL、AT+CMGR、AT+CMGS、AT+CMMS、AT+CMGW、AT+CMSS、AT+CNMA、AT+CNMI、AT+CSCB、AT+CSDH、AT+CSMP、AT+QCMGS、AT+QCMGR |
| 10 | `references/10-packet-domain-commands.md` | AT+CGATT、AT+CGDCONT、AT+CGQREQ、AT+CGQMIN、AT+CGEQREQ、AT+CGEQMIN、AT+CGACT、AT+CGDATA、AT+CGPADDR、AT+CGCLASS、AT+CGREG、AT+CGEREP、AT+CGSMS、AT+CEREG、AT+QGDCNT、AT+QAUGDCNT、AT+QNETDEVSTATUS、AT+CGCONTRDP |
| 11 | `references/11-supplementary-service-commands.md` | AT+CCFC、AT+CCWA、AT+CHLD、AT+CLIP、AT+CLIR、AT+COLP、AT+CSSN、AT+CUSD |
| 12 | `references/12-audio-commands.md` | AT+CLVL、AT+CMUT、AT+QAUDLOOP、AT+VTS、AT+VTD、AT+QAUDMOD、AT+QDAI、AT+QEEC、AT+QSIDET、AT+QMIC、AT+QRXGAIN、AT+QIIC、AT+QTONEDET、AT+QLDTMF、AT+QWDTMF、AT+QLTONE、AT+QAUDRD、AT+QPSND、AT+QTTS、AT+QTTSETUP、AT+QWTTS、AT+QAUDCFG、AT+QAUDPLAY、AT+QAUDPLAYGAIN、AT+QAUDRDGAIN、AT+QACDBLOAD、AT+QACDBREAD、AT+QACDBDEL |
| 13 | `references/13-hardware-related-commands.md` | AT+QPOWD、AT+CCLK、AT+CBC、AT+QADC、AT+QSCLK |
| 14 | `references/14-other-related-commands.md` | GNSS、DFOTA、FTP(S)、HTTP(S)、MMS、SMTP、TCP(IP)、SSL 相关指令概览（详见各 Quectel 应用笔记） |
| 15 | `references/15-appendix-references.md` | 出厂默认值（AT&F）、AT&W/ATZ 可保存设置、CME 错误码、CMS 错误码、URC 汇总、SMS 字符集转换、AT+CEER 释放原因列表 |

## 指令索引（按章节）

以下为从手册提取的完整指令索引。

## 1. 引言

语法规则、支持的字符集（GSM、UCS2、IRA）、指令端口（主 UART、USB modem 口、USB AT 口）、URC 行为及推荐的关机流程（AT+QPOWD）。详见 `references/01-introduction.md`。

## 2. 通用指令

| AT 指令 | 说明 |
| --- | --- |
| `ATI` | 显示模组标识信息 |
| `AT+GMI` | 请求制造商标识 |
| `AT+GMM` | 请求型号标识 |
| `AT+GMR` | 请求固件版本标识 |
| `AT+CGMI` | 请求制造商标识 |
| `AT+CGMM` | 请求 MT 型号标识 |
| `AT+CGMR` | 请求 MT 固件版本标识 |
| `AT+GSN` | 请求国际移动设备标识（IMEI）和 SN |
| `AT+CGSN` | 请求国际移动设备标识（IMEI） |
| `AT&F` | 将 AT 指令设置复位为出厂默认值 |
| `AT&V` | 显示当前配置 |
| `AT&W` | 将当前设置存储到用户定义配置文件 |
| `ATZ` | 将所有当前参数设置为用户定义配置文件 |
| `ATQ` | 设置结果码显示模式 |
| `ATV` | MT 响应格式 |
| `ATE` | 设置指令回显模式 |
| `A/` | 重复上一条指令行 |
| `ATS3` | 设置命令行终止符 |
| `ATS4` | 设置响应格式字符 |
| `ATS5` | 设置命令行编辑字符 |
| `ATX` | 设置 CONNECT 结果码格式并监视呼叫进程 |
| `AT+CFUN` | 设置 UE 功能 |
| `AT+CMEE` | 错误消息格式 |
| `AT+CSCS` | 选择 TE 字符集 |
| `AT+QURCCFG` | 配置 URC 指示选项 |
| `AT+QAPRDYIND` | 配置上报指定 URC |
| `AT+QDIAGPORT` | 调试 UART 配置 |

## 3. 串口接口控制指令

| AT 指令 | 说明 |
| --- | --- |
| `AT&C` | 设置 DCD 功能模式 |
| `AT&D` | 设置 DTR 功能模式 |
| `AT+IFC` | 设置 TE-TA 本地数据流控制 |
| `AT+ICF` | 设置 TE-TA 控制字符帧格式 |
| `AT+IPR` | 设置 TE-TA 固定本地波特率 |
| `AT+QRIR` | 将 RI 行为恢复为不活动 |

## 4. 状态控制指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+CPAS` | 移动设备活动状态 |
| `AT+CEER` | 扩展错误报告 |
| `AT+QINDCFG` | URC 指示配置 |
| `AT+QMBNCFG` | MBN 文件配置设置 |

## 5. (U)SIM 相关指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+CIMI` | 请求国际移动用户标识（IMSI） |
| `AT+CLCK` | 功能锁 |
| `AT+CPIN` | 输入 PIN 码 |
| `AT+CPWD` | 修改密码 |
| `AT+CSIM` | 通用 (U)SIM 访问 |
| `AT+CRSM` | 受限 (U)SIM 访问 |
| `AT+QCCID` | 显示 ICCID |
| `AT+QPINC` | 显示 PIN 剩余次数计数器 |
| `AT+QINISTAT` | 查询 (U)SIM 卡初始化状态 |
| `AT+QSIMDET` | (U)SIM 卡检测 |
| `AT+QSIMSTAT` | (U)SIM 卡插入状态上报 |
| `AT+QSIMVOL` | 固定 (U)SIM 卡供电电压 |
| `AT+CCHO` | 打开逻辑通道 |
| `AT+CGLA` | UICC 逻辑通道访问 |
| `AT+CCHC` | 关闭逻辑通道 |

## 6. 网络服务指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+COPS` | 运营商选择 |
| `AT+CREG` | 网络注册状态 |
| `AT+CSQ` | 信号质量报告 |
| `AT+CPOL` | 首选运营商列表 |
| `AT+COPN` | 读取运营商名称 |
| `AT+CTZU` | 自动时区更新 |
| `AT+CTZR` | 时区上报 |
| `AT+QLTS` | 获取通过网络同步的最新时间 |
| `AT+QNWINFO` | 查询网络信息 |
| `AT+QSPN` | 显示注册网络名称 |
| `AT+QNETINFO` | 查询各 RAT 网络信息 |
| `AT+QNWLOCK` | 网络锁定配置 |
| `AT+QOPSCFG` | 配置 2G/3G/4G 待扫描频段 / 在 LTE 中显示 RSSI |
| `AT+QOPS` | 频段扫描 |
| `AT+QFPLMNCFG` | FPLMN 配置 |
| `AT+QENG` | 开启/关闭工程模式 |
| `AT+CIND` | 控制指示指令 |

## 7. 通话相关指令

| AT 指令 | 说明 |
| --- | --- |
| `ATA` | 接听来电 |
| `ATD` | 主叫拨号 |
| `ATH` | 断开现有连接 |
| `AT+CVHU` | 语音挂断控制 |
| `AT+CHUP` | 挂断语音通话 |
| `+++` | 从数据模式切换到指令模式 |
| `ATO` | 从指令模式切换到数据模式 |
| `ATS0` | 设置自动接听前的振铃次数 |
| `ATS6` | 设置盲拨号前的暂停时间 |
| `ATS7` | 设置等待连接完成的时间 |
| `ATS8` | 设置逗号拨号修饰符等待时间 |
| `ATS10` | 设置指示数据载波消失后的断连延时 |
| `ATS12` | 设置使用 +++ 退出透传模式的间隔 |
| `AT+CBST` | 选择承载业务类型 |
| `AT+CSTA` | 选择地址类型 |
| `AT+CLCC` | 列出 ME 当前通话 |
| `AT+CR` | 业务上报控制 |
| `AT+CRC` | 设置来电指示的蜂窝结果码 |
| `AT+CRLP` | 选择无线链路协议参数 |
| `AT+QECCNUM` | 配置紧急呼叫号码 |
| `AT+QHUP` | 以指定释放原因挂断通话 |
| `AT+QCHLDIPMPTY` | 挂断 VoLTE 多方通话中的一路通话 |
| `AT^DSCI` | 通话状态指示 |

## 8. 电话簿指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+CNUM` | 用户号码 |
| `AT+CPBF` | 查找电话簿条目 |
| `AT+CPBR` | 读取电话簿条目 |
| `AT+CPBS` | 选择电话簿存储区 |
| `AT+CPBW` | 写入电话簿条目 |

## 9. 短信服务指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+CSMS` | 选择消息服务 |
| `AT+CMGF` | 消息格式 |
| `AT+CSCA` | 短信中心地址 |
| `AT+CPMS` | 首选消息存储 |
| `AT+CMGD` | 删除消息 |
| `AT+CMGL` | 列出消息 |
| `AT+CMGR` | 读取消息 |
| `AT+CMGS` | 发送消息 |
| `AT+CMMS` | 更多消息待发送 |
| `AT+CMGW` | 将消息写入存储器 |
| `AT+CMSS` | 从存储器发送消息 |
| `AT+CNMA` | 向 UE/TE 发送新消息确认 |
| `AT+CNMI` | 短信事件上报配置 |
| `AT+CSCB` | 选择小区广播消息类型 |
| `AT+CSDH` | 显示短信文本模式参数 |
| `AT+CSMP` | 设置短信文本模式参数 |
| `AT+QCMGS` | 发送长短信（合并短信） |
| `AT+QCMGR` | 读取长短信（合并短信） |

## 10. 分组域指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+CGATT` | PS 附着或去附着 |
| `AT+CGDCONT` | 定义 PDP 上下文 |
| `AT+CGQREQ` | 服务质量（请求） |
| `AT+CGQMIN` | 服务质量（最小可接受） |
| `AT+CGEQREQ` | UMTS 服务质量（请求） |
| `AT+CGEQMIN` | UMTS 服务质量（最小可接受） |
| `AT+CGACT` | 激活或去激活 PDP 上下文 |
| `AT+CGDATA` | 进入数据状态 |
| `AT+CGPADDR` | 显示 PDP 地址 |
| `AT+CGCLASS` | GPRS 移动台类别 |
| `AT+CGREG` | 网络注册状态 |
| `AT+CGEREP` | 分组域事件上报 |
| `AT+CGSMS` | 选择 MO 短信服务 |
| `AT+CEREG` | EPS 网络注册状态 |
| `AT+QGDCNT` | 分组数据计数器 |
| `AT+QAUGDCNT` | 自动保存分组数据计数器 |
| `AT+QNETDEVSTATUS` | 查询 RmNet 设备状态 |
| `AT+CGCONTRDP` | PDP 上下文读取动态参数 |

## 11. 补充业务指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+CCFC` | 呼叫转移号码与条件控制 |
| `AT+CCWA` | 呼叫等待控制 |
| `AT+CHLD` | 呼叫相关补充业务 |
| `AT+CLIP` | 主叫号码显示 |
| `AT+CLIR` | 主叫号码限制 |
| `AT+COLP` | 被连接线路识别显示 |
| `AT+CSSN` | 补充业务通知 |
| `AT+CUSD` | 非结构化补充业务数据 |

## 12. 音频指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+CLVL` | 扬声器音量等级选择 |
| `AT+CMUT` | 静音控制 |
| `AT+QAUDLOOP` | 启用/禁用音频环路测试 |
| `AT+VTS` | DTMF 与音频产生 |
| `AT+VTD` | 设置音频时长 |
| `AT+QAUDMOD` | 设置音频模式 |
| `AT+QDAI` | 数字音频接口配置 |
| `AT+QEEC` | 设置回声消除参数 |
| `AT+QSIDET` | 设置当前模式的侧音增益 |
| `AT+QMIC` | 设置麦克风上行增益 |
| `AT+QRXGAIN` | 设置 RX 下行增益 |
| `AT+QIIC` | 通过 IIC 读写 Codec |
| `AT+QTONEDET` | 启用/禁用 DTMF 检测 |
| `AT+QLDTMF` | 播放本地 DTMF |
| `AT+QWDTMF` | 播放或向远端发送 DTMF 文件 |
| `AT+QLTONE` | 播放本地自定义音频 |
| `AT+QAUDRD` | 录制媒体文件 |
| `AT+QPSND` | 播放 WAV 文件 |
| `AT+QTTS` | 播放文本（语音合成） |
| `AT+QTTSETUP` | 设置 TTS |
| `AT+QWTTS` | 播放文本或向远端发送文本 |
| `AT+QAUDCFG` | 查询和配置音频调优过程 |
| `AT+QAUDPLAY` | 播放媒体文件 |
| `AT+QAUDPLAYGAIN` | 设置音频播放增益 |
| `AT+QAUDRDGAIN` | 设置音频录制增益 |
| `AT+QACDBLOAD` | 写入 ACDB 文件 |
| `AT+QACDBREAD` | 读取 ACDB 文件 |
| `AT+QACDBDEL` | 删除 ACDB 文件 |

## 13. 硬件相关指令

| AT 指令 | 说明 |
| --- | --- |
| `AT+QPOWD` | 关机 |
| `AT+CCLK` | 时钟 |
| `AT+CBC` | 电池电量 |
| `AT+QADC` | 读取 ADC 值 |
| `AT+QSCLK` | 启用/禁用低功耗模式 |

## 14. 其他相关指令

指令概览（详情见各 Quectel 专用应用笔记）：

- **GNSS（定位）**：AT+QGPSCFG、AT+QGPSDEL、AT+QGPS、AT+QGPSEND、AT+QGPSLOC、AT+QGPSGNMEA、AT+QGPSXTRA、AT+QGPSXTRATIME、AT+QGPSXTRADATA
- **DFOTA（差分升级）**：AT+QFOTADL
- **FTP(S)**：AT+QFTPCFG、AT+QFTPOPEN、AT+QFTPCWD、AT+QFTPPWD、AT+QFTPPUT、AT+QFTPGET、AT+QFTPSIZE、AT+QFTPDEL、AT+QFTPMKDIR、AT+QFTPRMDIR、AT+QFTPLIST、AT+QFTPNLIST、AT+QFTPMLSD、AT+QFTPMDTM、AT+QFTPRENAME、AT+QFTPLEN、AT+QFTPSTAT、AT+QFTPCLOSE
- **HTTP(S)**：AT+QHTTPCFG、AT+QHTTPURL、AT+QHTTPGET、AT+QHTTPGETEX、AT+QHTTPPOST、AT+QHTTPPOSTFILE、AT+QHTTPREAD、AT+QHTTPREADFILE、AT+QHTTPSTOP
- **MMS（彩信）**：AT+QMMSCFG、AT+QMMSEDIT、AT+QMMSEND
- **SMTP**：AT+QSMTPCFG、AT+QSMTPDST、AT+QSMTPSUB、AT+QSMTPBODY、AT+QSMTPATT、AT+QSMTPCLR、AT+QSMTPPUT
- **TCP(IP)**：AT+QICSGP、AT+QIACT、AT+QIDEACT、AT+QIOPEN、AT+QICLOSE、AT+QISTATE、AT+QISEND、AT+QIRD、AT+QISENDEX、AT+QISWTMD、AT+QPING、AT+QNTP、AT+QIDNSCFG、AT+QIDNSGIP
- **SSL**：AT+QSSLCFG、AT+QSSLOPEN、AT+QSSLCLOSE、AT+QSSLWRITE、AT+QSSLREAD、AT+QSSLSTATE

## 15. 附录参考

- 可通过 AT&F 恢复的出厂默认设置
- 可通过 AT&W / ATZ 存储的 AT 指令设置
- CME 错误码汇总（+CME ERROR: <err>）
- CMS 错误码汇总（+CMS ERROR: <err>）
- URC 汇总
- SMS 字符集转换（GSM 7-bit、IRA、UCS2）
- AT+CEER 释放原因文本列表

完整列表见 `references/15-appendix-references.md`。

## 快速上手示例

数据连接常用初始化流程：

```text
AT                     -> OK
AT+CPIN?               -> +CPIN: READY   （检查 SIM 卡）
AT+CREG?               -> +CREG: 0,1     （已注册网络）
AT+CSQ                 -> +CSQ: 25,99    （信号质量）
AT+CGDCONT=1,"IP","apn"  -> OK           （定义 PDP 上下文）
AT+CGACT=1,1           -> OK             （激活 PDP 上下文）
```

关机（推荐的安全关机方式；收到 POWERED DOWN 后等待 1 秒再断电）：

```text
AT+QPOWD               -> POWERED DOWN
```

文本模式发送短信：

```text
AT+CMGF=1              -> OK
AT+CMGS="+8613800138000"
> hello world
+CMGS: <mr>            -> OK
```

## 说明

- 手册中带下划线的参数值为默认值。
- URC（主动上报）无需请求即上报；典型示例：来电 `RING`、短信到达、`+QIND`、关机 `POWERED DOWN`。
- 带 `*` 标记的指令处于开发中，可能不受支持。
- 本 skill 是根据移远官方手册 V2.0（2021-02-24）整理的中文参考。请以移远针对您具体模组/固件版本的最新文档为准。
