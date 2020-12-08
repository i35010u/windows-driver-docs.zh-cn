---
title: SIM 工具包命令
description: SIM 工具包命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e9964db3f057aa61a8f9ce0390c448c99b8aa3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814929"
---
# <a name="sim-toolkit-commands"></a>SIM 工具包命令


除非另有说明，否则支持以下 SIM 工具包命令。

## <a name="display-text"></a>显示文本


显示文本，普通优先级，为文本字符串解压缩的8位数据

显示文本字符串的高优先级、已解压缩的8位数据

显示文本、打包、SMS 默认字母

显示文本，延迟后清除消息

显示文本，含160字节的文本字符串

显示文本，在 UICC 会话中向后移动

显示文本，会话已被用户终止

显示文本，无用户响应

显示文本、扩展文本显示

显示文本、持续文本、解包数据8位

显示文本、持续文本、延迟后清除消息

显示文本，持续文本，等待用户 MMI 清除

显示文本，可变超时（10秒）

显示文本，UCS2 编码-中文字符

显示文本，UCS2 编码-片假名字符

## <a name="get-inkey"></a>获取 inkey


仅获取 INKEY，为字符集设置数字，为文本字符串解压缩8位数据

仅获取 INKEY，为字符集设置数字，为文本字符串设置 SMS 默认字母表

获取 INKEY，向后移动

获取 INKEY、中止

获取 INKEY，为字符集设置 SMS 默认字母表;为文本字符串解压缩了8位数据

获取 INKEY，文本字符串的最大长度

获取 INKEY，无用户响应

获取输入的 "是/否" 响应 INKEY

获取 INKEY，帮助信息可用

获取 INKEY，可变时间为10秒

获取 INKEY，UCS2 字母表中的文本字符串编码，成功

获取 INKEY，UCS2 字母表中的文本字符串编码的最大长度，成功

获取 INKEY，UCS2 字母表中的字符，成功

获取 INKEY，UCS2 字母表中的文本字符串编码-中文字符，成功

获取 INKEY，UCS2 字母表中的字符-中文字符，成功

获取 INKEY，UCS2 字母表中的文本字符串编码-片假名字符，成功

获取 INKEY，UCS2 字母表中的文本字符串编码的最大长度-片假名字符，成功

获取 INKEY，UCS2 字母表中的字符-片假名字符，成功

## <a name="get-input"></a>获取输入


仅获取输入、仅数字、SMS 默认字母表、回显文本、支持8位数据消息

仅获取输入、仅数字、SMS 默认字母、回显文本、打包我所需的 SMS 点到点

获取输入、字符集、SMS 默认字母、回显文本、支持8位数据消息

仅获取输入、仅数字、SMS 默认字母、我隐藏文本、支持8位数据消息

仅获取输入、仅数字、SMS 默认字母表、回显文本、支持8位数据消息、20位数

获取输入，向后移动

获取输入、中止

仅获取输入、仅数字、SMS 默认字母表、回显文本、支持8位数据消息、160位数

仅获取输入、仅数字、SMS 默认字母、回显文本、支持8位数据消息、无输入

获取输入，文本字符串的长度为 Null，成功

获取输入，无用户响应

获取输入，输入的默认文本，成功

获取输入，最大长度为的输入的默认文本，成功

在 UCS2 中获取输入文本字符串编码，成功

获取输入，UCS2 中的文本字符串编码的最大长度，成功

获取输入，UCS2 字母表中的字符集，成功

获取输入，UCS2 字母表中的字符集，输入的最大长度，成功

## <a name="more-time"></a>更多时间


更多时间

## <a name="play-tone"></a>播放音调


播放音调

播放音调，UCS2 字母表中的字符集，成功

从中文的 UCS2 字母表中播放的音频字符集成功

播放音调，UCS2 以片假名提供成功

## <a name="poll-interval"></a>轮询间隔


轮询间隔，20秒

轮询间隔， \[ 调用后再次发送轮询状态命令\]

## <a name="provide-local-information"></a>提供本地信息


提供本地信息、位置信息 (MCC、MNC、缺少和单元 ID) 

提供本地信息，将我的 IMEI

提供本地信息、网络度量结果 (NMR) 

提供本地信息、日期、时间、时区 \[ 需要 OEM NVRAM 设置\]

提供本地信息，语言设置

提供本地信息，预先计时

提供本地信息、访问技术

提供本地信息，IMEISV \[ 需要 OEM NVRAM 设置\]

<strong>\\</strong>*提供本地信息，搜索模式信息- **\* \* 不支持 \* \\** 网络搜索模式*

提供本地信息 Intra-Frequency UTRAN 度量

提供本地信息、frequency 间 UTRAN 度量

## <a name="refresh"></a>刷新


REFRESH，USIM 初始化

刷新，文件更改通知

刷新、USIM 初始化和文件更改通知

REFRESH、USIM 初始化和完整文件更改通知

刷新，UICC 重置

USIM 在短信下载后进行刷新

刷新，USIM 应用程序重置

刷新，UICC 重置 IMSI 更改过程

刷新，USIM 应用程序重置 IMSI 更改过程

刷新，IMSI 更改过程的3G 会话重置

在调用期间刷新、拒绝 IMSI 更改过程的3G 会话重置

刷新，漫游，UTRAN

刷新，漫游，InterRAT

## <a name="select-item"></a>选择项


选择项目，必需功能，成功

选择项，大菜单，成功

选择项，调用选项，成功

选择项，向后移动，已成功

选择项，"Y"，成功

选择项，大菜单，成功

选择项，默认项，成功

选择项，无用户响应

SELECT ITEM，UCS2 in 西里尔语字符，0x80 UCS2 编码，成功

SELECT ITEM，With UCS2 in 西里尔字符，0x81 UCS2 编码，成功

SELECT ITEM，With UCS2 in 西里尔字符，0x82 UCS2 编码，成功

选择项，其中 UCS2 为中文字符，成功

选择 ITEM，其中 UCS2 为片假名字符，0x80 UCS2 编码，成功

SELECT ITEM，With UCS2-片假名字符，0x81 UCS2 编码，成功

SELECT ITEM，With UCS2-片假名字符，0x82 UCS2 编码，成功

选择项，下一个操作指示器，成功

## <a name="send-dtmf"></a>发送 DTMF


发送 DTMF，其中 Alpha Id 正常

发送 DTMF，包含 alpha 标识符

发送 DTMF，Mobile 不在无 Alpha Id 的语音呼叫中

发送 DTMF，UCS2 中文版，成功

发送 DTMF，UCS2 文本以片假名，成功

## <a name="send-short-message"></a>发送短信


发送短消息，不需要打包，8位数据

发送短消息，需要打包，8位数据

发送短消息，需要打包，无 SMS-Center 地址，8位数据

发送短消息，需要打包，160字节的消息，8位数据

发送短信，不需要打包，SMS 默认字母表，160字节的消息

发送短消息，不需要打包，UCS2 (16 位数据) 

发送短信、alpha 标识符160字节长、SMS 默认字母、成功

发送短信、不需要打包、alpha 标识符长度为 "00"、8位数据、成功

发送短信，不需要打包，8位数据，无 alpha 标识符，成功

## <a name="send-ss"></a>发送 SS


SEND SS、call forward 无条件、all bearers、成功

发送 SS，调用向前无条件，所有 bearers， **\* \* 未完全验证 \* \\** 的返回错误*

发送 SS，调用向前无条件，所有 bearers，拒绝

发送 SS，调用向前无条件，大型 SS 字符串

SEND SS，请求 CLIR 状态，成功，alpha 标识符限制

发送 SS，其中包含 Null Alpha Id (激活到国际号码的呼叫转发) 

发送 SS，UCS2 支持

发送 SS，按中文的 "向前拨"、"bearers"、"成功" 和 "UCS2" 文本

发送 SS，调用向前无条件，所有 bearers，成功，UCS2 文本，以片假名

## <a name="send-ussd"></a>发送 USSD


发送带 Alpha ID 的 USSD、7位数据

发送 USSD，8位数据，具有 Alpha ID

SEND USSD，UCS2 data，with Alpha ID

发送 USSD，7位数据，失败 (返回错误) 

发送 USSD，7位数据，失败的 (拒绝) 

发送 USSD，7位数据，具有较大的 Alpha ID，256个字符

发送 USSD，7位数据，无 Alpha ID

发送 USSD，7位数据，含 null Alpha ID

## <a name="set-up-call"></a>设置呼叫


设置呼叫，用户和已连接的呼叫确认

设置呼叫，用户拒绝呼叫

设置呼叫，将所有其他呼叫置于保持状态，忙

设置呼叫，断开所有其他呼叫，我忙碌

设置呼叫，仅在其他呼叫当前不繁忙的情况下调用

设置调用，将所有其他调用置于保持状态，不允许调用保留

设置呼叫，最大拨号号码字符串，无 alpha 标识符

设置调用，256字节长度，长第一个 alpha 标识符

设置调用，称为 "参与方子地址"

设置呼叫，重拨的最长持续时间

## <a name="set-up-event-list"></a>设置事件列表


设置事件列表，设置呼叫连接事件

设置事件列表，替换事件

设置事件列表，删除事件

设置事件列表，删除我的电源重启事件

## <a name="set-up-menu"></a>设置菜单


设置菜单和菜单选项，无需帮助请求、替换和删除工具包菜单

设置菜单、包含多个项目的大型菜单

设置菜单和菜单选择，并提供帮助请求、替换和删除工具包菜单

设置菜单、下一个操作指示器 "发送 SM"、"设置呼叫"、"启动浏览器"、"提供本地信息"、成功

设置菜单和菜单选项，无需帮助请求、替换和删除工具包菜单，并在西里尔字符中使用 UCS2

设置菜单和菜单选项，无需帮助请求、替换和删除工具包菜单，使用中文字符 UCS2

设置菜单和菜单选择，无需帮助请求，替换和删除工具包菜单，以片假名字符 UCS2

## <a name="timer-management"></a>计时器管理


计时器管理，启动计时器1，获取计时器的当前值并停用计时器

计时器管理，启动计时器2，获取计时器的当前值并停用计时器

计时器管理，启动计时器8，获取计时器的当前值并停用计时器

计时器管理，尝试获取未启动的计时器的当前值

计时器管理，尝试停用未启动的计时器

计时器管理，启动8个计时器

## <a name="call-control-by-usim"></a>通过 USIM 调用 control


通过 USIM 调用 CONTROL，按用户设置呼叫尝试，USIM 使用 "90 00" 响应

按 USIM 呼叫控制，设置用户的呼叫尝试，不进行修改

通过 USIM 调用 CONTROL，设置调用主动命令导致的呼叫尝试，无需修改即可

通过 USIM 调用 CONTROL，按用户设置呼叫尝试，不允许

使用不带 ALPHA ID 的 USIM 调用 CONTROL，并设置调用主动型命令导致的调用尝试，不允许这样做

使用不带 ALPHA ID 的 USIM 调用 CONTROL，按用户设置调用尝试，允许进行修改

使用不带 ALPHA ID 的 USIM 调用 CONTROL，并设置调用主动型命令导致的调用尝试，允许进行修改

按 USIM 调用控制、设置用户的呼叫尝试、允许修改：紧急呼叫

通过 USIM 调用 CONTROL，设置用户的呼叫尝试，允许修改： EFECC 中的数字

通过 USIM 调用 CONTROL，设置用户拨打紧急电话的呼叫尝试

通过 USIM 调用 CONTROL，通过调用寄存器设置呼叫，USIM 使用 "90 00" 响应

通过 USIM 调用 CONTROL，通过呼叫注册设置呼叫，允许而不进行修改

通过 USIM 调用 CONTROL，通过呼叫注册设置呼叫，不允许使用

通过 USIM 调用 CONTROL，通过呼叫注册设置呼叫，允许进行修改

通过 USIM、send SS 调用 CONTROL，USIM 使用 "90 00" 响应

通过 USIM、send SS 调用 CONTROL，允许而不进行修改

通过 USIM、send SS 调用 CONTROL，不允许这样做

通过 USIM、send SS 调用 CONTROL，允许进行修改

通过 USIM 调用 CONTROL，设置不在 EF FDN 中的调用

通过 USIM 调用 CONTROL，在 EF FDN 中设置调用，USIM 使用 "90 00" 响应

通过 USIM 调用 CONTROL，在 EF FDN 中设置调用，但允许不进行修改

通过 USIM 调用 CONTROL，在 EF FDN 中设置调用，不允许这样做

通过 USIM 调用 CONTROL，在 EF FDN 中设置调用，允许进行修改

## <a name="ms-sm-control-by-usim"></a>USIM 的 MS SM 控制


按 USIM 的 MO SM 控制，允许使用主动命令，不修改

通过 USIM、用户短信、允许、无修改的 MO SM 控制

按 USIM 的 MO SM 控制，不允许使用主动命令

使用用户短信的 USIM SM 控制，不允许使用

按 USIM 进行的 MO SM 控制，使用主动命令，允许进行修改

通过 USIM、用户短信、允许修改的 MO SM 控制

## <a name="envelope-timer-expiration"></a>信封计时器过期


信封计时器过期，从计时器管理：挂起的主动 UICC 命令

信封计时器过期，从计时器管理： UICC 应用程序工具包繁忙

## <a name="event-download"></a>事件下载


事件下载，呼叫已连接

事件下载，呼叫已连接，我支持设置呼叫

事件下载，呼叫断开连接

事件下载位置状态

事件下载 MT 呼叫

事件下载，用户活动

事件下载，可用数据，GPRS

事件下载，链接上的通道状态已删除

**\\** 事件下载，*\* \* 不支持 \* \** <em>网络搜索模式更改事件</em>*

## <a name="open-channel"></a>打开通道


开放式通道，即时链接建立，GPRS，无本地地址，无 alpha 标识符，无网络访问名称

开放通道，即时链接建立，GPRS，无本地地址，无 alpha 标识符，具有网络访问名称

开放式通道，即时链接建立，GPRS，带 alpha 标识符

开放式通道，即时链接建立，GPRS，含 null alpha 标识符

打开频道、立即链接建立、GPRS、执行了修改 (缓冲区大小的命令) 

开放式通道，即时链接建立，GPRS，带 alpha 标识符，用户不接受主动命令

## <a name="get-channel-status"></a>获取通道状态


获取状态，未打开任何 BIP 通道

获取状态，当前已打开 BIP 通道

删除链接后获取状态

## <a name="send-data"></a>发送数据


发送数据，即时模式

发送数据，存储模式

在存储模式下发送数据，2次连续发送数据命令

发送数据，存储模式，已完全使用 Tx 缓冲器

发送数据，其中包含 Alpha ID、存储模式、已完全使用的 Tx 缓冲区

发送数据，使用错误的通道标识符的即时模式

## <a name="receive-data"></a>接收数据


接收数据，已打开通道

## <a name="close-channel"></a>关闭频道


结束通道，成功

闭合通道，通道标识符无效

关闭频道，在已关闭的频道上

## <a name="terminal-profile"></a>终端配置文件


终端配置文件，3GPP

终端配置文件，Microsoft 要求

## <a name="smspp"></a>SMS – PP


SMS PP，UICC 通过 "61XX" (确认来做出响应) 

SMS PP，更多时间

SMS PP，数据编码/消息类

SMS PP，GDC UDH

SMS PP，连接 SMS 8 位参考编号

SMS PP，USIM 安全标头

## <a name="bip-download"></a>BIP 下载


BIP UDP 下载，3G，浏览菜单

BIP TCP 下载、3G、传入呼叫

BIP UDP 下载，2G，传入呼叫

<strong>\\</strong>*BIP 下载， **\* \* 不支持 \* \\** 在下载过程中丢失网络*

## <a name="sms-cb"></a>SMS CB


**注意**  
OEM 必须修改和启用用于单元广播的 SMS 提供程序

 

SMS CB，无显示

<strong>\\</strong>*SMS CB， **\* \* 不支持 \* \\** 显示*

## <a name="related-topics"></a>相关主题


[SIM 工具包](sim-toolkit.md)

 

 






