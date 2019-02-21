---
title: Tracelog 命令语法
description: Tracelog 有命令 （或操作） 的启动、 停止和控制跟踪会话。
ms.assetid: 13c85a1e-77ea-47d7-bb97-ff9141a8a531
keywords:
- Tracelog 命令语法驱动程序开发工具
topic_type:
- apiref
api_name:
- Tracelog Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3010002b73323b6f086d1e486ef633fa54481180
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554818"
---
# <a name="tracelog-command-syntax"></a>Tracelog 命令语法


Tracelog 有命令 （或操作） 的启动、 停止和控制[跟踪会话](trace-session.md)。

> [!NOTE]
> 若要控制跟踪会话必须是 Performance Log Users 组或计算机上的管理员组的成员 (**以管理员身份运行**)。

```
    tracelog [actions] [options] | [-h | -help | -?] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数

有关跟踪日志参数的信息，请参阅\[ [*操作*](#actions) \] \[ [*选项*](#options)\].

### <a name="actions"></a>\[*actions*\]

<span id="_______-addautologger__LoggerName_"></span><span id="_______-addautologger__loggername_"></span><span id="_______-ADDAUTOLOGGER__LOGGERNAME_"></span> **-addautologger** \[*LoggerName*\]  
对于自动记录器会话配置的注册表项。 自动记录器会话是用于在系统启动期间跟踪驱动程序或其他跟踪提供程序的活动的首选的方法。 必须指定的会话 GUID using **-sessionguid**选项。 **Tracelog addautologger**命令采用与相同的选项**Tracelog-启动**命令。

<span id="_______-capturestate__LoggerName_"></span><span id="_______-capturestate__loggername_"></span><span id="_______-CAPTURESTATE__LOGGERNAME_"></span> **-capturestate** \[*LoggerName*\]  
请求启用到的所有提供程序*LoggerName*记录状态信息。 已启用的关键字有助于确定的记录的信息种类。

<span id="_______-disable__LoggerName_"></span><span id="_______-disable__loggername_"></span><span id="_______-DISABLE__LOGGERNAME_"></span> **-disable** \[*LoggerName*\]  
禁用指定的跟踪提供程序。 当禁用提供程序时，它将继续运行，但它将停止生成跟踪消息。

**Tracelog-停止**命令停止会话之前禁用跟踪提供程序。 不需要停止跟踪会话之前禁用提供程序。 但是，可以使用**tracelog-禁用**命令，而无需停止跟踪会话禁用所选提供程序。

禁用停止跟踪提供程序将跟踪消息发送到跟踪会话缓冲区，但它不会刷新缓冲区或停止跟踪会话。 使用**tracelog-刷新**命令将缓冲区刷新和一个**tracelog-停止**或**tracelog-x** （停止所有） 命令以停止跟踪会话。

使用 Tracelog **EnableTrace**函数，实现**tracelog-禁用**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

<span id="_______-enable__LoggerName_"></span><span id="_______-enable__loggername_"></span><span id="_______-ENABLE__LOGGERNAME_"></span> **-enable** \[*LoggerName*\]  
启用一个或多个跟踪提供程序*LoggerName*跟踪会话。

启用提供程序时，提供程序生成跟踪消息，并将其发送到跟踪会话的缓冲区。 如果提供程序未运行 （或未加载） 当你启用它，系统*预寄存器*提供程序，即，它为 ETW 注册数据库中的提供程序保留空间并将保存启用命令。 当提供程序启动并实际注册时，它接收已保存的启用命令，并开始将跟踪消息发送到会话。

**Tracelog-开始**命令将启用指定由可选的任何提供程序**guid**中的参数**tracelog-启动**命令。 不需要提交单独**tracelog-启用**命令。

可以使用**tracelog-启用**命令，将提供程序添加到某个正在运行的跟踪会话，而跟踪，提供程序更改的标志和级别，或若要重新启用的提供程序通过使用禁用**tracelog-禁用**命令。

使用时**tracelog-启用**命令，首先提交**tracelog-启动**命令以启动跟踪会话，并提交**tracelog-启用**命令以启用提供程序。

但不能禁用它，可以反复启用正在运行的提供程序。 （您可能会执行此操作以更改标志和级别。）

跟踪标志和使用指定的跟踪级别 **-标志**并 **-级别**参数传递给所表示的所有跟踪提供程序**guid**参数。 若要为每个跟踪提供程序指定不同的标志和级别，将提交单独**tracelog-启用**命令对于每个提供程序，具有其自己的标志和级别设置。

如果启用任何 NT 内核记录器标志 (如 **-noprocess**， **-nothread**， **-fio**，或者 **-cm**) 而全局记录器跟踪会话正在运行全局会话将转换为 NT 内核记录器跟踪会话的记录器。 在启动过程中，此功能旨在跟踪内核事件。

<span id="_______-enableex__LoggerName_"></span><span id="_______-enableex__loggername_"></span><span id="_______-ENABLEEX__LOGGERNAME_"></span> **-enableex** \[*LoggerName*\]  
与相同 **-启用**。 跟踪日志的未来版本中可能会删除此选项。

<span id="_______-enumguid______"></span><span id="_______-ENUMGUID______"></span> **-enumguid**   
枚举 （或列出） 可以在系统上的提供商[注册](registered-provider.md)使用事件跟踪 Windows (ETW)。 Enumguid 显示的说明，请参阅[Tracelog Enumguid 显示](tracelog-enumguid-display.md)。

使用 Tracelog **EnumerateTraceGuids**函数，实现**tracelog enumguid**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

<span id="_______-enumguidex___guid_"></span><span id="_______-ENUMGUIDEX___GUID_"></span> **-enumguidex** \[**\#**<em>guid</em>\]  
枚举 （或列出） 可以在系统上的提供商[注册](registered-provider.md)使用事件跟踪 Windows (ETW)。 EnumguidEx 显示的说明，请参阅[Tracelog Enumguid 显示](tracelog-enumguid-display.md)。

使用 Tracelog **EnumerateTraceGuidsEx**函数，实现**tracelog enumguidex**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

<span id="_______-flush___LoggerName__"></span><span id="_______-flush___loggername__"></span><span id="_______-FLUSH___LOGGERNAME__"></span> **-flush** \[*LoggerName*\]   
刷新活动的缓冲区*LoggerName*跟踪会话。 如果*LoggerName*未指定，则跟踪日志刷新的缓冲区[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

这强制刷新是除了跟踪消息缓冲区已满时以及当停止跟踪会话时，会自动执行刷新，此外还包括激活的刷新计时器刷新 (**-ft**)。

时刷新跟踪会话的缓冲区，缓冲区中的事件会立即传递到跟踪日志或跟踪使用者。

正在刷新不会禁用跟踪提供程序或重定向的跟踪消息。 缓冲区被刷新后，跟踪提供程序将继续向这些缓冲区写入事件。

使用 Tracelog **FlushTrace**函数，实现**tracelog-刷新**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

可以使用**tracelog-刷新**命令 **-f** *Logfile*选项以刷新当前正在对指定的缓冲区的跟踪消息[跟踪日志](trace-log.md)(.etl) 文件。 此参数的有效期仅为缓冲的跟踪会话 (**-缓冲**); 对于其他跟踪会话类型， **-f**参数将被忽略。

此刷新会影响仅缓冲区的当前内容。 它不重未来的跟踪消息定向到跟踪日志。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l** \[*-lp*\]  
列出了在计算机上运行的所有跟踪会话的属性。

如果传递 **-lp**选项时，Tracelog 还将列出为每个会话启用的所有提供程序。

<span id="_______-q___LoggerName_"></span><span id="_______-q___loggername_"></span><span id="_______-Q___LOGGERNAME_"></span> **-q** \[*LoggerName*\] \[*-lp*\]  
列出 （查询） 指定的跟踪会话的属性。 如果未指定*LoggerName*，Tracelog 查询[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

如果传递 **-lp**选项时，Tracelog 还将列出所有启用到该会话的提供程序。

<span id="_______-remove_GlobalLogger______"></span><span id="_______-remove_globallogger______"></span><span id="_______-REMOVE_GLOBALLOGGER______"></span> **-remove GlobalLogger**   
删除并重新注册表值初始化全局记录器跟踪会话。 它将开始条目的值设置为 0 （不启动），并删除其他注册表项。 **Tracelog-删除**命令仅适用于全局记录器跟踪会话。 所有其他会话名称值均无效。

**Tracelog-删除**命令不是必需。 但是，如果未设置的值**启动**为 0 的条目，全局记录器会话开始每次重新启动系统。

如果不使用**tracelog-删除**命令，从上一个会话的选项是仍在注册表中，并且它们将用于在新的会话除非在提交**tracelog-启动**命令不同的值相同的选项。

<span id="_______-start__LoggerName_"></span><span id="_______-start__loggername_"></span><span id="_______-START__LOGGERNAME_"></span> **-start** \[*LoggerName*\]  
启动跟踪会话使用*LoggerName*选择来表示跟踪会话。

使用**GlobalLogger**作为*LoggerName*若要指定[全局记录器跟踪会话](global-logger-trace-session.md)。 在会话启动时重新启动计算机。

*LoggerName*可以任何名称符合 Windows 命名准则，最多 1,024 个字符。 如果名称包含空格，将名称括在引号中。 Tracelog 不区分大小写。

默认值是 **"NT 内核记录器"**。 如果省略此参数，启动 Tracelog [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)并声明错误，如果您使用**guid**参数来指定不同的跟踪提供程序。

<span id="_______-stop__LoggerName_"></span><span id="_______-stop__loggername_"></span><span id="_______-STOP__LOGGERNAME_"></span> **-stop** \[*LoggerName*\]  
在指定的跟踪会话中禁用提供程序，然后终止该会话。

**Tracelog-停止**命令同时禁用跟踪提供程序，并停止跟踪会话。 一个**tracelog-禁用**命令仅禁用跟踪提供程序。

如果在启动[启动时全局记录器会话](boot-time-global-logger-session.md)其中跟踪了内核事件，需要使用该命令**tracelog-停止"NT 内核记录器"** 或**tracelog-停止 GlobalLogger**来将其停止。 当你使用任一命令以停止[全局记录器跟踪会话](global-logger-trace-session.md)跟踪会话，Tracelog 停止提供程序，但不重置注册表项的值。 若要重置全局记录器注册表项的值，请使用**tracelog-删除**。

<span id="-systemrundown__LoggerName_"></span><span id="-systemrundown__loggername_"></span><span id="-SYSTEMRUNDOWN__LOGGERNAME_"></span>**-systemrundown** \[*LoggerName*\]  
请求登录断开事件定向到 SystemTraceProvider *LoggerName*会话。 请参阅[配置和启动 SystemTraceProvider 会话](https://msdn.microsoft.com/library/windows/desktop/jj883720)有关启动跟踪会话信息。

此命令才在 Windows 8 和更高版本的 Windows 上可用。

<span id="_______-timeout_______value______"></span><span id="_______-TIMEOUT_______VALUE______"></span> **-timeout** *value*   
指定以毫秒 (ms) 为单位的超时值，以启用与提供程序时使用**tracelog-启用**命令。 默认超时值为 0。

如果超时值为 0，跟踪日志将调用每个提供程序启用回调，并立即返回，而无需等待要完成的回调。

若要以同步方式启用提供程序，请指定一个超时值。 如果指定的超时值时，Tracelog 将等待，直到每个提供程序启用回调退出或超时过期。

在上一次启用多个提供程序时，超时是按顺序应用到每个。

<span id="_______-update_____LoggerName__"></span><span id="_______-update_____loggername__"></span><span id="_______-UPDATE_____LOGGERNAME__"></span> **-update** \[*LoggerName*\]   
**Tracelog-更新**命令将在运行时更改跟踪会话的属性。

在**tracelog-更新**命令，则-**guid**仅更新专用跟踪会话时，参数是有效 (**-um**)。若要添加或删除提供程序从标准跟踪会话，会话正在运行时，使用**tracelog-启用**并**tracelog-禁用**命令。

如果启动一个跟踪日志会话 (**-f**)，可以更新到实时会话 (**-rt**)，但消息仍要发送到跟踪使用者除了跟踪日志。 通过更新，不能消除在会话中的日志。 但是，您可以添加到跟踪日志会话的实时消息传递之前，必须首先使用**tracelog-刷新**命令来刷新缓冲区。

如果启动实时会话 (**-rt**)，然后更新到跟踪日志会话 (**-f**)，新的跟踪消息将无法再直接发送到跟踪使用者; 它们只发送给跟踪日志。 要将跟踪日志添加到实时跟踪会话，请同时使用 **-rt**并 **-f**中**tracelog-更新**命令。 您可以添加到跟踪日志会话的实时消息传递之前，必须先使用**tracelog-刷新**命令来刷新缓冲区。

无法更新[全局记录器跟踪会话](global-logger-trace-session.md)。

对专用 （用户模式） 跟踪会话中，可以更新日志文件名称 (**-f**) 和刷新计时器值 (**-ft**)。

若要更新的标志和级别，使用**tracelog-启用**命令以重新启用具有新标志或级别的提供程序。

使用 Tracelog **ControlTrace**函数，实现**tracelog-更新**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

### <a name="options"></a>\[*options*\]

<span id="_-addtotriagedump_______"></span><span id="_-ADDTOTRIAGEDUMP_______"></span> **-addtotriagedump**   
> [!NOTE]
> 可能需要查看使用调试器的内核转储事件时，此选项应不使用除外。

指定的任何活动会话缓冲区可用于添加到会审内存转储。 会审转储受限的大小，而且如果会话的缓冲区会导致超出其最大大小的转储，缓冲区将遗漏。

<span id="_______-append______"></span><span id="_______-APPEND______"></span> **-append**   
将跟踪消息附加到指定的事件跟踪日志 (.etl) 文件 **-f**参数。 默认值是创建一个新的文件。

此参数是仅在包含的命令中有效 **-f** ，但不包括 **-rt**或 **-cir**。

<span id="_______-b_______BufferSize______"></span><span id="_______-b_______buffersize______"></span><span id="_______-B_______BUFFERSIZE______"></span> **-b** *BufferSize*   
指定大小，以 kb 为单位，每个缓冲区分配的跟踪会话。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。

<span id="-bt_n"></span><span id="-BT_N"></span>**-bt** *n*  
指定的数量 (*n*) 的缓冲区填满之前开始将刷新它们。 此选项才可用在 Windows 8.1 中启动。

<span id="_______-buffering______"></span><span id="_______-BUFFERING______"></span> **-buffering**   
启动缓存的跟踪会话。

在缓冲的跟踪会话中，将跟踪缓冲区中保留跟踪消息。 它们不是发送到跟踪使用者或跟踪日志中记录。

<span id="_______-cir_______MaxFileSize______"></span><span id="_______-cir_______maxfilesize______"></span><span id="_______-CIR_______MAXFILESIZE______"></span> **-cir** *MaxFileSize*   
指定循环日志记录 （位于文件结尾，记录最早的邮件通过新消息） 在事件跟踪日志 (.etl) 文件。 *MaxFileSize*以 mb 为单位指定文件的最大大小。 无需*MaxFileSize*值，此参数将被忽略。

默认值是按顺序与文件大小没有限制日志记录。

<span id="_______-cm______"></span><span id="_______-CM______"></span> **-cm**   
启用跟踪的注册表 （配置管理器） 访问权限。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="_______-critsec______"></span><span id="_______-CRITSEC______"></span> **-critsec**   
在专用跟踪会话中跟踪对过程的关键部分事件。 可以在任何用户模式进程，甚至是未检测的跟踪的一个启动关键部分过程记录器。

使用 **-pid**来指定进程。 不要使用**guid**与 **-critsec**。 系统定义的自定义 GUID (CritSecGuid) 的关键部分跟踪。 不能使用 **-堆**并 **-critsec**在同一命令中。

<span id="_______-dpcisr______"></span><span id="_______-DPCISR______"></span> **-dpcisr**   
启用延迟的过程调用 (Dpc) 的跟踪中断服务请求 (Isr) 映像加载事件 (**-i m g**)，并在内核中的上下文切换。 仅为 NT 内核记录器跟踪会话，此参数才有效。

仅在跟踪日志包含在 Windows 驱动程序工具包适用于 Windows Vista 和更高版本的 WDK 版本中支持此选项。 **– 对 dpcisr**选项不能用于 **-eflag**选项。

使用 **-UsePerfCounter**参数与 **-执行 dpcisr**。 此参数，为每个事件，提供了一个唯一的时间戳，需要使用 Tracerpt，用来设置格式和解释 DPC/ISR 事件的工具。 有关解释和格式化这些事件的信息，请参阅下面的"注释"。

<span id="_______-eflag________n_________flag..._"></span><span id="_______-EFLAG________N_________FLAG..._"></span> **-eflag** *n* \[*flag*...\]  
启用内核事件使用的附加标志[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，最值得注意的是，要启用跟踪的 DPC、 ISR 和上下文的标志切换事件。 **-Eflag**选项不能用于 **– 执行 dpcisr**选项。

<span id="_______-enableproperty________n______"></span><span id="_______-ENABLEPROPERTY________N______"></span> **-enableproperty** *n*   
请参阅的说明*EnabledProperties*中*EnableParameters*结构作为参数传递给[EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)说明和支持的值。

<span id="-EventIdFilter_____-in-out_n_id1_id2_..."></span><span id="-eventidfilter_____-in-out_n_id1_id2_..."></span><span id="-EVENTIDFILTER_____-IN-OUT_N_ID1_ID2_..."></span>**-EventIdFilter** {**-in**|**-out**} **** *n* **** *id1 id2 ...*  
指定与事件 id 筛选器*n*事件 id (最大 64 事件 id 允许)。 此选项才可用在 Windows 8.1 中启动。

<span id="___-ExeFilter____Executable_file____Executable_file_...__"></span><span id="___-exefilter____executable_file____executable_file_...__"></span><span id="___-EXEFILTER____EXECUTABLE_FILE____EXECUTABLE_FILE_...__"></span> **-ExeFilter** *Executable\_file* \[**;** *Executable\_file* ...\]   
指定要筛选的可执行文件的名称。 可以指定文件的列表。 单独使用分号分隔的文件的名称。 排除未列出的文件。 此选项才可用在 Windows 8.1 中启动。

<span id="_______-f___LogFile_"></span><span id="_______-f___logfile_"></span><span id="_______-F___LOGFILE_"></span> **-f** \[*LogFile*\]  
启动跟踪日志会话。 *日志文件*指定的路径 （可选） 和事件跟踪日志 (.etl) 文件的文件名。 默认值为 c:\\LogFile.etl。 若要将远程计算机上的文件，包括路径中的计算机名称或 IP 地址。

如果您使用 **-rt**与 **-f**，跟踪消息发送给使用者和事件跟踪日志文件。 不能使用 **-rt**或 **-f**与 **-缓冲**。

<span id="_______-fio______"></span><span id="_______-FIO______"></span> **-fio**   
启用文件 I/O 事件的跟踪。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="_______-flag_______Flag______"></span><span id="_______-flag_______flag______"></span><span id="_______-FLAG_______FLAG______"></span> **-flag** *Flag*   
> [!NOTE]
> 已按关键字取代标志。 使用 **-matchanykw**除非要启用 WPP 提供程序。

指定[跟踪标志](trace-flags.md)有关[提供程序](trace-provider.md)跟踪会话中。 标志值确定跟踪提供程序生成的事件。

*标志*表示十进制或十六进制格式中的跟踪提供程序中定义的标志值。 默认值为 0 从通过 0xFF000000 0x01000000 的值被保留供将来使用。

标志值的含义是单独定义的每个跟踪提供程序。 通常情况下，标志表示越来越详细的报告级别。

中指定的标志值**tracelog-启动**命令将应用于所有跟踪提供程序中跟踪会话。 若要为每个跟踪提供程序设置不同的标志，请使用**tracelog-启用**。

<span id="_______-ft_______FlushTime______"></span><span id="_______-ft_______flushtime______"></span><span id="_______-FT_______FLUSHTIME______"></span> **-ft** *FlushTime*   
指定何种频率，以秒为单位，跟踪消息缓冲区被刷新。 最小的刷新时间为 1 秒。 默认值为 0 （无强制刷新）。

这强制刷新是补充和跟踪消息缓冲区已满时停止跟踪会话时，会发生自动刷新。

请参阅**tracelog-刷新命令**。

<span id="_______-guid___GUID___GUIDFile_"></span><span id="_______-guid___guid___guidfile_"></span><span id="_______-GUID___GUID___GUIDFILE_"></span> **-guid** {*\#GUID* | *file* | *\*name*}  
使指定的跟踪提供程序。

如果指定的文件，跟踪日志将在文件中指定的所有提供程序启用跟踪。 该文件的格式必须为：

```text
; comment line
guid1;matchanykeyword;level
guid2;matchanykeyword;level
```

如果指定了提供程序 GUID，GUID 必须为前面带有数字符号 (*\#*)。

如果指定的提供程序名称，名称必须为前面带有星号 (*\**)。 然后会将名称转换为使用的相同算法的 GUID。NET 的事件源。 然后将使用此 GUID 来启用的提供程序。

如果省略此参数，则任何跟踪提供程序将消息不发送到跟踪会话。 但是，从开始跟踪会话之后, 您可以使用**tracelog-启用**命令以启用会话的一个或多个跟踪提供程序。

<span id="_______-gs______"></span><span id="_______-GS______"></span> **-gs**   
生成全局序列号为每个跟踪消息。

全局序列号的计算机上的所有跟踪会话是唯一的。 默认情况下，没有序列号。

此参数不是有效，且 NT 内核记录器跟踪会话。

<span id="_______-heap______"></span><span id="_______-HEAP______"></span> **-heap**   
跟踪用户模式进程堆内存事件。 可以在任何用户模式进程，甚至是未检测的跟踪的一个来开始堆过程记录器。

使用 **-pid**来指定进程。 不要使用**guid**与 **-堆**。 系统定义堆内存跟踪的自定义的 GUID (HeapGuid)。 不能使用 **-堆**并 **-critsec**在同一命令中。

<span id="_______-hf______"></span><span id="_______-HF______"></span> **-hf**   
启用跟踪的硬页面错误 （需要磁盘访问，以解决的页面错误）。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="-hybridshutdown_stoppersist"></span><span id="-HYBRIDSHUTDOWN_STOPPERSIST"></span>**-hybridshutdown** {**stop**|**persist**}  
控制混合关闭记录器行为。 此选项才可用在 Windows 8 中启动。

*停止*将导致系统将执行混合关闭时停止该会话。
*保留*将导致系统重新启动从混合关闭后继续会话。

<span id="_______-img______"></span><span id="_______-IMG______"></span> **-img**   
启用映像加载事件的跟踪。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="___-independent___"></span><span id="___-INDEPENDENT___"></span> **-independent**   
> [!NOTE]
> 独立模式应启用对每个跟踪会话。

对跟踪会话启用独立模式。 独立模式允许会话，以收集其他非独立于模式会话中已删除的事件。 此选项才可用在 Windows 8.1 中启动。

<span id="_______-kb______"></span><span id="_______-KB______"></span> **-kb**   
使用日志文件大小 (kb)。 默认值为兆字节 (MB)。

<span id="_______-kd______"></span><span id="_______-KD______"></span> **-kd**   
将跟踪消息重定向到 KD 或的 Windbg 中，附加者为准。 此参数还将跟踪缓冲区大小设置为 3 KB，在调试器中，最大缓冲区大小，并忽略任何 **-b**命令中的参数。

在提交具有的 Tracelog 命令时，必须运行调试器 **-kd**。 否则，跟踪日志将停止响应。

有关在内核调试程序中显示跟踪消息的信息，请参阅注释。

**-Lbr** *EventName\[**+** EventName+...\]:Filter\[**,** Filter,...\]*  
在内核事件配置 LBR 跟踪。

使用 **-eflag 帮助**有关内核事件的列表。

<span id="_______-level________n______"></span><span id="_______-LEVEL________N______"></span> **-level** *n*   
指定[跟踪级别](trace-level.md)中跟踪会话提供程序。 级别确定跟踪提供程序生成的事件。

*级别*表示十进制或十六进制格式的级别值。 默认值为 0

级别值的含义是单独定义的每个跟踪提供程序。 通常情况下，跟踪级别表示 （信息、 警告或错误） 事件的严重性。

中指定的级别值**tracelog-启动**命令将应用于所有跟踪提供程序中跟踪会话。 若要为每个跟踪提供程序设置不同级别，使用**tracelog-启用**。

<span id="_______-lowcapacity______"></span><span id="_______-LOWCAPACITY______"></span> **-lowcapacity**   
> [!NOTE]
> 除非，不应使用此选项需要降低内存成本。 使用此选项可使每个事件日志更慢。

使用一次一个缓冲区收集多个处理器上生成的事件。 此选项选择事件\_跟踪\_否\_每\_处理器\_缓冲日志记录模式。 有关详细信息，请参阅 Windows SDK。

<span id="_______-ls______"></span><span id="_______-LS______"></span> **-ls**   
生成本地序列号为每个跟踪消息。

本地序列号跟踪会话中是唯一的。 默认情况下，没有序列号。

此参数不是有效，且 NT 内核记录器跟踪会话。

<span id="_______-max_______NumberOfBuffers______"></span><span id="_______-max_______numberofbuffers______"></span><span id="_______-MAX_______NUMBEROFBUFFERS______"></span> **-max** *NumberOfBuffers*   
指定用于跟踪会话分配跟踪日志的缓冲区的最大数目。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。

<span id="_______-matchallkw________n______"></span><span id="_______-MATCHALLKW________N______"></span> **-matchallkw** *n*   
指定*MatchAllKeyWord*限制的事件的类别的位掩码的提供程序写入并结合使用 **-matchanykw**选项。

此位掩码是可选的。 如果事件的关键字满足中指定的条件-**matchanykw**选项，提供程序将写入事件仅当此掩码中的位的所有存在于事件的关键字。 如果不使用此掩码 **-matchanykw**为零。

跟踪日志将值传递*n*中*MatchAllKeyWord*参数[EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)函数调用。 请参阅 Windows SDK 的详细信息。

<span id="_______-matchanykw________n______"></span><span id="_______-MATCHANYKW________N______"></span> **-matchanykw** *n*   
指定*MatchAnyKeyword*位掩码，用于确定类别的事件提供程序写入。

提供程序写入事件，如果有事件的关键字位与匹配任何位设置此掩码中。 跟踪日志将值传递*n*中*MatchAnyKeyWord*参数[EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)函数调用。 请参阅 Windows SDK 的详细信息。

<span id="_______-min_______NumberOfBuffers______"></span><span id="_______-min_______numberofbuffers______"></span><span id="_______-MIN_______NUMBEROFBUFFERS______"></span> **-min** *NumberOfBuffers*   
指定用于存储跟踪消息最初分配的缓冲区数。 当缓冲区已满时，Tracelog 会分配更多的缓冲区，直到它达到最大值。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。

<span id="_______-newfile_______MaxFileSize______"></span><span id="_______-newfile_______maxfilesize______"></span><span id="_______-NEWFILE_______MAXFILESIZE______"></span> **-newfile** *MaxFileSize*   
创建一个新的事件跟踪日志 (.etl) 文件，只要现有文件达到*MaxFileSize*。 *MaxFileSize*以 mb 为单位指定每个日志文件的最大大小。 无需*MaxFileSize*值，此参数将被忽略。

使用时 **-newfile**，则还必须使用 **-f** *日志文件*参数和的值*日志文件*必须包含一个名称字符 **%d**以指示十进制模式-例如，trace%d.etl。 否则，该命令将失败，错误\_无效\_名称。 Windows 会创建一个新文件每次递增的十进制值中的文件的名称。

此参数不是有效，且预先分配 (**-prealloc**)、 循环日志记录 (**-cir**)、 与 NT 内核记录器会话或专用跟踪会话。

<span id="_______-nodisk______"></span><span id="_______-NODISK______"></span> **-nodisk**   
物理磁盘 I/O 事件的禁用跟踪。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="_______-nonet______"></span><span id="_______-NONET______"></span> **-nonet**   
TCP/IP 和用户数据报协议 (UDP) 事件的禁用跟踪。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="_______-noprocess______"></span><span id="_______-NOPROCESS______"></span> **-noprocess**   
禁用跟踪的开始和结束每个进程。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="_______-nothread______"></span><span id="_______-NOTHREAD______"></span> **-nothread**   
禁用跟踪的开始和结束每个线程。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="_______-paged______"></span><span id="_______-PAGED______"></span> **-paged**   
用于跟踪消息缓冲区的可分页内存。 默认情况下，事件跟踪使用不可分页的内存缓冲区。

需要不可分页的内存提供程序将不能将事件记录到使用可分页内存的会话。

<span id="_______-pids________PIDs_PID__PID..._"></span><span id="_______-pids________pids_pid__pid..._"></span><span id="_______-PIDS________PIDS_PID__PID..._"></span> **-pid**  *\#Pid PID* \[ *PID*...\]  
指定的用户模式中的堆内存或关键部分跟踪会话运行进行处理。 仅对于有效 **-堆**或 **-critsec**。

*\#Pid*使用此参数指定的 Id 列出的进程数。 *PID*表示进程标识符。 可以使用此参数指定最多十个 Pid。

当多个进程，如单个程序时创建多个进程中运行的提供程序时，请列出多个 Pid。

<span id="___-PidFilter____n_pid1_pid2_..."></span><span id="___-pidfilter____n_pid1_pid2_..."></span><span id="___-PIDFILTER____N_PID1_PID2_..."></span> **-PidFilter** *n* *pid1 pid2 ...*  
指定的 Pid 筛选器*n* Pid (允许的最大 8)。 此选项才可用在 Windows 8.1 中启动。

<span id="_______-pf______"></span><span id="_______-PF______"></span> **-pf**   
启用跟踪的所有页面错误。 仅为 NT 内核记录器跟踪会话，此参数才有效。

<span id="___________________-PkgIdFilter____Package_Full_Name____Package_Full_Name..._"></span><span id="___________________-pkgidfilter____package_full_name____package_full_name..._"></span><span id="___________________-PKGIDFILTER____PACKAGE_FULL_NAME____PACKAGE_FULL_NAME..._"></span> **-PkgIdFilter** *Package Full Name* \[ **;***Package Full Name*...\]  
指定包 ID 筛选器。 可以指定的包文件的列表。 单独使用分号分隔的文件的名称。

<span id="___-PkgAppIdFilter_____PRAID____PRAID..._"></span><span id="___-pkgappidfilter_____praid____praid..._"></span><span id="___-PKGAPPIDFILTER_____PRAID____PRAID..._"></span> **-PkgAppIdFilter** *PRAID* \[**;***PRAID*...\]  
指定相对于包的应用程序标识符 (PRAID) 筛选器。 PRAID 是内包的应用程序的唯一标识符。 您可以指定多个*PRAID*。 单独使用分号分隔的 Id。 此选项是适用于 UWP 应用在 Windows 8.1 中启动。

<span id="-Pmc_Ctrs_Events"></span><span id="-pmc_ctrs_events"></span><span id="-PMC_CTRS_EVENTS"></span>**-Pmc** *Ctr1,Ctr2,...:Name+Name+...*  
配置性能监视器计数器 (PMC) 采样上指定的内核事件。 此选项才可用在 Windows 8 中启动。

使用 **-ProfileSource 帮助**计数器的列表。
使用 **-eflag 帮助**有关内核事件的列表。

<span id="_______-prealloc______"></span><span id="_______-PREALLOC______"></span> **-prealloc**   
启动会话之前.etl 文件的保留空间。

此参数需要 **-seq**或 **-cir**与*MaxFileSize*。 它不是有效，且 **-newfile**。

<span id="-ProfileSource_src"></span><span id="-profilesource_src"></span><span id="-PROFILESOURCE_SRC"></span>**-ProfileSource** *src*  
配置要使用的分析源。 对于源的列表，可以使用命令**tracelog-ProfileSource 帮助**。 此选项才可用在 Windows 8 中启动。

此选项才适用于 Windows 8 和更高版本的 Windows。

<span id="_______-rt______"></span><span id="_______-RT______"></span> **-rt**   
启动一个实时跟踪会话。 (跟踪日志会话 (**-f**) 是默认值。)

如果您使用 **-rt**并 **-f**，跟踪消息发送到跟踪使用者和事件跟踪日志文件。 不能使用 **-rt**或 **-f**与 **-缓冲**。 有关详细信息，请参阅[跟踪会话](trace-session.md)。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-secure**   
启用跟踪在安全模式下。 此选项选择事件\_跟踪\_SECURE\_模式日志记录模式。 将限制谁可以将事件记录到与具有 TRACELOG 会话\_日志\_事件的权限。

<span id="_______-sessionguid______"></span><span id="_______-SESSIONGUID______"></span> **-sessionguid**   
指定自动记录器会话 GUID 注册表值。

<span id="-SetProfInt_n_src"></span><span id="-setprofint_n_src"></span><span id="-SETPROFINT_N_SRC"></span>**-SetProfInt** *n* **** *src*  
> [!IMPORTANT]
> 不建议更改的分析时间间隔。

配置分析时间间隔 (*n*) 指定的源，其中*n*为 100ns 个单位。 默认值为 10000 （这是等效于 1 毫秒）。 此选项才可用在 Windows 8 中启动。

<span id="_______-seq_______MaxFileSize______"></span><span id="_______-seq_______maxfilesize______"></span><span id="_______-SEQ_______MAXFILESIZE______"></span> **-seq** *MaxFileSize*   
指定向事件跟踪日志 (.etl) 文件顺序 （在文件尾，停止记录事件） 的日志记录。 *MaxFileSize*以 mb 为单位指定文件的最大大小。 无需*MaxFileSize*值，此参数将被忽略。

顺序日志记录是默认值，但可以使用此参数，若要设置最大文件大小，或使用 **-prealloc**。 如果不提供此参数，则文件大小没有限制。

<span id="_______-sourceguid________SourceGuid______"></span><span id="_______-sourceguid________sourceguid______"></span><span id="_______-SOURCEGUID________SOURCEGUID______"></span> **-sourceguid** *SourceGuid*   
指定作为传递的 GUID *SourceId*参数[EnableTraceEx](https://go.microsoft.com/fwlink/p/?linkid=103398)或[EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)函数。 *SourceId*标识该提供程序启用的会话。

**-stackwalk** \[*事件*\]  
指定要收集堆栈上的内核事件。 使用 **-eflag 帮助**有关内核事件的列表。 此参数是仅适用于 NT 内核记录器或系统记录器跟踪会话。

<span id="________________-StackWalkFilter_-in-outnid1_id2_..."></span><span id="________________-stackwalkfilter_-in-outnid1_id2_..."></span><span id="________________-STACKWALKFILTER_-IN-OUTNID1_ID2_..."></span> **-StackWalkFilter** {**-in**|**-out**}*nid1 id2 ...*  
指定与事件 ID 筛选器*n*事件 Id （最大 64 事件 Id 允许）。 此选项才可用在 Windows 8.1 中启动。

<span id="-systemlogger"></span><span id="-SYSTEMLOGGER"></span>**-systemlogger**  
记录器可以接收 SystemTraceProvider 事件。 请参阅[配置和启动 SystemTraceProvider 会话](https://msdn.microsoft.com/library/windows/desktop/jj883720)。 此选项才可用在 Windows 8 中启动。

<span id="_______-um______"></span><span id="_______-UM______"></span> **-um**   
指定此参数是必需的专用跟踪会话的专用跟踪会话。

<span id="_______-UseCPUCycle______"></span><span id="_______-usecpucycle______"></span><span id="_______-USECPUCYCLE______"></span> **-UseCPUCycle**   
使用处理器的频率 （也称为"CPU 时钟周期"） 来测量每条跟踪消息的时间。

此计时器提供最高的可能解决方法，但它是非常敏感的很容易出错，尤其是在电源管理的系统和多处理器计算机上。 例如，如果具有 ARM 处理器的计算机上指定此计时器，它可能会导致无序事件。 相反， **-UsePerfCounter**建议对于高分辨率的跟踪。

**-UsePerfCounter**是默认计时器事件跟踪。

<span id="_______-UsePerfCounter______"></span><span id="_______-useperfcounter______"></span><span id="_______-USEPERFCOUNTER______"></span> **-UsePerfCounter**   
记录的高分辨率性能计数器的值的时钟，而不是分辨率更低的系统时间，与每条跟踪消息。

性能计数器时钟中大约 100 毫微秒为单位的计数，因为它为每个事件提供唯一时间戳。

**-UsePerfCounter**是默认计时器事件跟踪。

<span id="_______-UseSystemTime______"></span><span id="_______-usesystemtime______"></span><span id="_______-USESYSTEMTIME______"></span> **-UseSystemTime**   
记录的系统时间，而不是高分辨率性能计数器的时钟时间，与每条跟踪消息。 由于系统计时器的分辨率为 10 毫秒 （相比，性能计数器时钟的 100 纳秒），多个事件可以具有相同的系统时间。

**-UsePerfCounter**是默认计时器事件跟踪。

<span id="_______-_____help___-_______"></span><span id="_______-_____HELP___-_______"></span> **-? |帮助 |-?**   
显示用法信息。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

以下注释适用于多个跟踪日志命令。

### <a name="span-idsyntaxerrorsspanspan-idsyntaxerrorsspansyntax-errors"></a><span id="syntax_errors"></span><span id="SYNTAX_ERRORS"></span>语法错误

Tracelog 不显示所有不正确的语法组合，例如当您尝试更新不能更改的设置的错误。 相反，它将忽略该命令的无效部分，并显示一条成功消息。

### <a name="span-idsystemloggersspanspan-idsystemloggersspansystem-loggers"></a><span id="system_loggers"></span><span id="SYSTEM_LOGGERS"></span>系统的记录器

Windows 使用跟踪会话用于多种用途，其中一些关键正确操作。 不停止任何跟踪会话未启动的。

### <a name="span-idenumguidspanspan-idenumguidspanenumguid"></a><span id="enumguid"></span><span id="ENUMGUID"></span>Enumguid

若要确定是否**tracelog-开始**或**tracelog-启用**命令是否成功，请使用**tracelog enumguid**命令用于确定是否提供程序已启用，以及如何将**tracelog-l （列表）** 命令来检查跟踪会话的属性。

### <a name="span-idrealtimeandlogsessionsspanspan-idrealtimeandlogsessionsspanreal-time-and-log-sessions"></a><span id="real_time_and_log_sessions"></span><span id="REAL_TIME_AND_LOG_SESSIONS"></span>实时备份和日志会话

跟踪会话可以是实时跟踪会话和跟踪日志会话。 如果包括 **-rt** （实时） 和 **-f** （日志会话） 参数在同一命令中，系统会发送缓冲区内容日志和跟踪使用者。 但是，可以添加到跟踪日志会话的实时消息传递之前，缓冲区必须刷新通过使用**tracelog-刷新**命令。

如果启动实时会话 (**-rt**)，然后更新到日志会话 (**-f**)，任何新的跟踪消息只发送给日志文件。 若要添加到实时会话日志文件，可以同时使用 **-rt**并 **-f**中**tracelog-更新**命令。

如果在启动日志会话 (**-f**)，可以更新到实时会话 (**-rt**)，但继续发送到跟踪使用者除了日志消息。 通过更新，不能消除在会话中的日志。

若要显示或将跟踪消息保存在实时的一次性仅会话中，您还可以使用跟踪使用者，如[Tracefmt](tracefmt.md)，或使用[TraceView](traceview.md)，这是一个跟踪控制器 （如跟踪日志） 和跟踪使用者。 在使用 Tracefmt，请务必包括 **-rt** Tracefmt 命令中的参数。

### <a name="span-idflagsandlevelsspanspan-idflagsandlevelsspanflags-and-levels"></a><span id="flags_and_levels"></span><span id="FLAGS_AND_LEVELS"></span>标志和级别

大多数跟踪提供程序不会生成任何跟踪消息，除非将标志或级别设置为特定值。 提供程序使用标志或级别来控制正在跟踪的内容。 如果事件跟踪日志文件为空，请查看标志和跟踪提供程序中的级别。

若要确保始终生成跟踪消息，请完成以下步骤：

1.  设置**标志**参数为 0xFFFFFFFF，若要启用所有标志设置。

2.  设置**级别**到 255 以启用所有级别设置的参数。

### <a name="span-idtheeflagparameterspanspan-idtheeflagparameterspanthe--eflag-parameter"></a><span id="the__eflag_parameter"></span><span id="THE__EFLAG_PARAMETER"></span>-Eflag 参数

具有 Tracelog **-eflag** （扩展的标志） 参数，用于启用附加标志[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)-最值得注意的是，若要启用的 DPC，ISR，跟踪标志和上下文切换事件。 因为**tracelog-开始**命令现在包括 **-执行 dpcisr**参数，使用 **-eflag**参数不再是必需的不建议。

### <a name="span-idoutdatedparametersspanspan-idoutdatedparametersspanoutdated-parameters"></a><span id="outdated_parameters"></span><span id="OUTDATED_PARAMETERS"></span>已过时的参数

在以前版本的跟踪日志， **tracelog-开始**支持的命令 **-rt b**参数组合。 已替换为此组合 **-缓冲**参数和它将不再有效。

**-X**参数已被删除，因为正在停止所有跟踪会话可能会导致系统不稳定。

**-Disableex**参数已被删除。 使用 **-禁用**相反。

### <a name="span-idntkernelloggerspanspan-idntkernelloggerspannt-kernel-logger"></a><span id="nt_kernel_logger"></span><span id="NT_KERNEL_LOGGER"></span>NT 内核记录器

若要使用 NT 内核记录器启动跟踪会话，请省略中的会话名称**tracelog-开始**命令，并不使用**guid**参数来指定提供程序 GUID 文件。 **"NT 内核记录器"** 是默认会话名称。

如果未指定会话名称，或为 **"NT 内核记录器"**，在系统启动的 NT 内核记录器跟踪会话，即使使用**guid**参数而不指定 GUID **SystemTraceControlGUID**，NT 内核记录器跟踪会话的控件的 GUID。 如果您指定不同的 GUID，则系统返回错误，（"系统记录器不接受应用程序 guid"），但仍能开始 NT 内核记录器跟踪会话。

默认情况下，当 Tracelog 启动的 NT 内核记录器跟踪会话，这样的进程、 线程、 物理磁盘 I/O、 跟踪和 TCP/IP 事件，但可以使用参数来禁用这些事件的跟踪和启用其他事件的跟踪。

### <a name="span-iddpcisreventsspanspan-iddpcisreventsspandpcisr-events"></a><span id="dpc_isr_events"></span><span id="DPC_ISR_EVENTS"></span>DPC/ISR 事件

由于 Tracerpt 预计的时间戳作为系统性能计数器时钟时间，因此使用 Tracelog **-UsePerfCounter**参数启动跟踪会话时。

因为 DPC 和 ISR 事件由特殊检测收集的它们不显示在**已启用跟踪**行的表的跟踪日志将显示确认命令。

有关详细信息，请参阅[示例 15:测量 DPC/ISR 时间](example-15--measuring-dpc-isr-time.md)。
