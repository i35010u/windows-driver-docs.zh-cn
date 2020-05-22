---
title: Tracelog 命令语法
description: Tracelog 具有用于启动、停止和控制跟踪会话的命令（或操作）。
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
ms.openlocfilehash: db03eb5ca3e147095703fba8ec432b61d1bcabd1
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769701"
---
# <a name="tracelog-command-syntax"></a>Tracelog 命令语法


Tracelog 具有用于启动、停止和控制[跟踪会话](trace-session.md)的命令（或操作）。

> [!NOTE]
> 若要控制跟踪会话，您必须是计算机上 "Performance Log Users" 组或 "Administrators" 组的成员（以**管理员身份运行**）。

```
    tracelog [actions] [options] | [-h | -help | -?] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

有关 Tracelog 参数的详细信息，请参阅 \[ [*操作*](#actions) \] \[ [*选项*](#options) \] 。

### <a name="actions"></a>\[*执行*\]

<span id="_______-addautologger__LoggerName_"></span><span id="_______-addautologger__loggername_"></span><span id="_______-ADDAUTOLOGGER__LOGGERNAME_"></span>**-addautologger** \[*LoggerName*\]  
配置自动记录器会话的注册表项。 自动记录器会话是在系统启动期间跟踪驱动程序或其他跟踪提供程序的活动的首选方法。 必须使用 **-sessionguid**选项指定会话 GUID。 **Tracelog-addautologger**命令采用与**tracelog-start**命令相同的选项。

<span id="_______-capturestate__LoggerName_"></span><span id="_______-capturestate__loggername_"></span><span id="_______-CAPTURESTATE__LOGGERNAME_"></span>**-capturestate** \[*LoggerName*\]  
请求所有启用了*LoggerName*的提供程序记录状态信息。 启用关键字有助于确定所记录的信息的类型。

<span id="_______-disable__LoggerName_"></span><span id="_______-disable__loggername_"></span><span id="_______-DISABLE__LOGGERNAME_"></span>**-disable** \[*LoggerName*\]  
禁用指定的跟踪提供程序。 当提供程序处于禁用状态时，它将继续运行，但会停止生成跟踪消息。

**Tracelog**命令禁用跟踪提供程序，然后停止该会话。 停止跟踪会话之前，不需要禁用提供程序。 但是，可以使用**tracelog**命令禁用所选的提供程序，而无需停止跟踪会话。

禁用会阻止跟踪提供程序向跟踪会话缓冲区发送跟踪消息，但它不会刷新缓冲区或停止跟踪会话。 使用**tracelog**命令刷新缓冲区，并使用**tracelog**或**tracelog** （停止所有）命令停止跟踪会话。

Tracelog 使用**EnableTrace**函数实现**Tracelog**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

<span id="_______-enable__LoggerName_"></span><span id="_______-enable__loggername_"></span><span id="_______-ENABLE__LOGGERNAME_"></span>**-enable** \[*LoggerName*\]  
为*LoggerName*跟踪会话启用一个或多个跟踪提供程序。

启用提供程序时，提供程序会生成跟踪消息并将其发送到跟踪会话的缓冲区。 如果在启用该提供程序时，提供程序未运行（或未加载），则系统会*预先注册*该提供程序，也就是说，它在 ETW 注册数据库中保留提供程序的空间，并保存 enable 命令。 当提供程序启动并实际注册时，它将接收已保存的 enable 命令并开始向会话发送跟踪消息。

**Tracelog**命令启用由**tracelog-start**命令中的可选 **-guid**参数指定的任何提供程序。 不需要提交单独的**tracelog**命令。

您可以使用**tracelog**命令将提供程序添加到正在运行的跟踪会话，在跟踪时更改提供程序的标志和级别，或重新启用使用**tracelog**命令禁用的提供程序。

使用**tracelog**命令时，请先提交**tracelog-start**命令来启动跟踪会话，然后提交**tracelog**命令来启用提供程序。

可以重复启用正在运行的提供程序，而不会禁用它。 （您可以执行此操作来更改标志和级别。）

使用 **-标志**和**级别**参数指定的跟踪标志和跟踪级别将传递给由 **-guid**参数表示的所有跟踪提供程序。 若要为每个跟踪提供程序指定不同的标志和级别，请使用其自己的标志和级别设置为每个提供程序提交一个单独的**tracelog**命令。

如果在全局记录器跟踪会话正在运行时启用任何 NT 内核记录程序标志（例如 **-noprocess**、 **-nothread**、 **-fio**或 **-cm**），则全局记录器会话将转换为 NT 内核记录器跟踪会话。 此功能设计用于在启动过程中跟踪内核事件。

<span id="_______-enableex__LoggerName_"></span><span id="_______-enableex__loggername_"></span><span id="_______-ENABLEEX__LOGGERNAME_"></span>**-enableex** \[*LoggerName*\]  
完全相同 **。** 在 Tracelog 的未来版本中可能会删除此选项。

<span id="_______-enumguid______"></span><span id="_______-ENUMGUID______"></span>**-enumguid**   
枚举系统上向 Windows 事件跟踪（ETW）[注册](registered-provider.md)的提供程序。 有关 Enumguid 显示的说明，请参阅[Tracelog Enumguid 显示](tracelog-enumguid-display.md)。

Tracelog 使用**EnumerateTraceGuids**函数实现**Tracelog-enumguid**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

<span id="_______-enumguidex___guid_"></span><span id="_______-ENUMGUIDEX___GUID_"></span>**-enumguidex** \[ **\#**<em>guid</em>\]  
枚举系统上向 Windows 事件跟踪（ETW）[注册](registered-provider.md)的提供程序。 有关 EnumguidEx 显示的说明，请参阅[Tracelog Enumguid 显示](tracelog-enumguid-display.md)。

Tracelog 使用**EnumerateTraceGuidsEx**函数实现**Tracelog-enumguidex**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

<span id="_______-flush___LoggerName__"></span><span id="_______-flush___loggername__"></span><span id="_______-FLUSH___LOGGERNAME__"></span>**-flush** \[*LoggerName*\]   
刷新*LoggerName*跟踪会话的活动缓冲区。 如果未指定*LoggerName* ，则 Tracelog 将刷新[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)的缓冲区。

此强制刷新除了跟踪消息缓冲区已满和跟踪会话停止时以及刷新计时器（**-ft**）激活的刷新外，还会自动进行刷新。

刷新跟踪会话的缓冲区时，缓冲区中的事件会立即传递给跟踪日志或跟踪使用者。

刷新不会禁用跟踪提供程序或重定向跟踪消息。 刷新缓冲区后，跟踪提供程序会继续将事件写入缓冲区。

Tracelog 使用**FlushTrace**函数实现**Tracelog**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

您可以使用带有 **-f** *Logfile*选项的**tracelog**命令，将缓冲区中的当前跟踪消息刷新到指定的[跟踪日志](trace-log.md)（.etl）文件中。 此参数仅对缓冲跟踪会话（**-缓冲**）有效;对于其他跟踪会话类型，将忽略 **-f**参数。

此刷新仅影响缓冲区的当前内容。 它不会将以后的跟踪消息重定向到跟踪日志。

<span id="_______-l______"></span><span id="_______-L______"></span>**-l** \[*-lp*\]  
列出计算机上运行的所有跟踪会话的属性。

如果传递了 **-lp**选项，则 Tracelog 还会列出每个会话的所有启用的提供程序。

<span id="_______-q___LoggerName_"></span><span id="_______-q___loggername_"></span><span id="_______-Q___LOGGERNAME_"></span>**-q** \[*LoggerName* \]\[ *-lp*\]  
列出（查询）指定跟踪会话的属性。 如果未指定*LoggerName*，则 Tracelog 将查询[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

如果传递了 **-lp**选项，则 Tracelog 还会列出会话中启用的所有提供程序。

<span id="_______-remove_GlobalLogger______"></span><span id="_______-remove_globallogger______"></span><span id="_______-REMOVE_GLOBALLOGGER______"></span>**-Remove GlobalLogger**   
删除并重新初始化全局记录器跟踪会话的注册表值。 它将开始项的值设置为0（不启动），并删除其他注册表项。 **Tracelog**命令仅适用于全局记录器跟踪会话。 所有其他会话名称值都无效。

**Tracelog-remove**命令不是必需的。 但是，如果未将**开始**条目的值设置为0，则每次重新启动系统时，都会启动全局记录器会话。

如果不使用**tracelog**命令，则上一个会话中的选项仍在注册表中，并且它们将用于新的会话，除非你使用相同选项的不同值提交**tracelog**命令。

<span id="_______-start__LoggerName_"></span><span id="_______-start__loggername_"></span><span id="_______-START__LOGGERNAME_"></span>**-start** \[*LoggerName*\]  
使用你选择用于表示跟踪会话的*LoggerName*启动跟踪会话。

使用**GlobalLogger**作为*LoggerName*来指定[全局记录器跟踪会话](global-logger-trace-session.md)。 当你重新启动计算机时，会话启动。

*LoggerName*可以是任何符合 Windows 命名准则的名称，最多1024个字符。 如果名称包含空格，则用引号将该名称引起来。 Tracelog 不区分大小写。

默认值为 **"NT 内核记录器"**。 如果省略此参数，Tracelog 将启动[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，并在使用 **-guid**参数指定不同的跟踪提供程序时声明错误。

<span id="_______-stop__LoggerName_"></span><span id="_______-stop__loggername_"></span><span id="_______-STOP__LOGGERNAME_"></span>**-stop** \[*LoggerName*\]  
禁用指定跟踪会话中的提供程序，然后终止该会话。

**Tracelog**命令既禁用跟踪提供程序，也停止跟踪会话。 **Tracelog**命令仅禁用跟踪提供程序。

如果启动一个跟踪内核事件的[启动时全局记录器会话](boot-time-global-logger-session.md)，则需要使用命令**Tracelog "NT 内核记录器"** 或**tracelog-stop GlobalLogger**将其停止。 使用任一命令停止[全局记录器跟踪会话](global-logger-trace-session.md)跟踪会话时，Tracelog 将停止提供程序，但不会重置注册表项的值。 若要重置全局记录器注册表项的值，请使用**tracelog-remove**。

<span id="-systemrundown__LoggerName_"></span><span id="-systemrundown__loggername_"></span><span id="-SYSTEMRUNDOWN__LOGGERNAME_"></span>**-systemrundown** \[*LoggerName*\]  
请求 SystemTraceProvider 在*LoggerName*会话中记录断开事件。 有关启动跟踪会话的信息，请参阅[配置和启动 SystemTraceProvider 会话](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-a-systemtraceprovider-session)。

此命令仅在 Windows 8 及更高版本的 Windows 上可用。

<span id="_______-timeout_______value______"></span><span id="_______-TIMEOUT_______VALUE______"></span>**-超时***值*   
指定使用**tracelog**命令启用提供程序时要使用的超时值（以毫秒为单位）。 默认超时值为0。

如果超时值为0，则 Tracelog 将调用每个提供程序的启用回调并立即返回，而不等待回调完成。

若要同步启用提供程序，请指定超时值。 如果指定超时值，则 Tracelog 将等待，直到每个提供程序的启用回调退出或超时过期。

同时启用多个提供程序时，会按顺序对每个提供程序应用超时。

<span id="_______-update_____LoggerName__"></span><span id="_______-update_____loggername__"></span><span id="_______-UPDATE_____LOGGERNAME__"></span>**-更新** \[*LoggerName*\]   
**Tracelog**命令在跟踪会话正在运行时更改其属性。

在**tracelog**命令中，-**guid**参数仅在更新专用跟踪会话（**-um**）时有效。若要在会话运行时添加或删除标准跟踪会话中的提供程序，请使用**tracelog**和**tracelog**命令。

如果启动跟踪日志会话（**-f**），则可以更新到实时会话（**-rt**），但仍会将消息发送到跟踪使用者之外的跟踪日志。 你无法通过更新从会话中消除日志。 但是，必须先使用**tracelog-flush**命令刷新缓冲区，然后才能将实时消息传递添加到跟踪日志会话中。

如果启动实时会话（**-rt**），然后更新到跟踪日志会话（**-f**），则不再将新的跟踪消息直接发送到跟踪使用者;它们只发送到跟踪日志。 若要将跟踪日志添加到实时跟踪会话，请在**tracelog**命令中使用 **-rt**和 **-f** 。 在将实时消息传递添加到跟踪日志会话之前，必须先使用**tracelog**命令刷新缓冲区。

不能更新[全局记录器跟踪会话](global-logger-trace-session.md)。

对于专用（用户模式）跟踪会话，只能更新日志文件名（**-f**）和刷新计时器值（**-ft**）。

若要更新标志和级别，请使用**tracelog**命令通过新的标志或级别重新启用提供程序。

Tracelog 使用**ControlTrace**函数实现**Tracelog**命令。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

### <a name="options"></a>\[*选项*\]

<span id="_-addtotriagedump_______"></span><span id="_-ADDTOTRIAGEDUMP_______"></span>**-addtotriagedump**   
> [!NOTE]
> 不应使用此选项，除非可能需要使用调试器查看内核转储中的事件。

指定可将会话的任何活动缓冲区添加到 "会审内存转储"。 会审转储大小限制，如果会话的缓冲区导致转储超出其最大大小，则缓冲区将被省略。

<span id="_______-append______"></span><span id="_______-APPEND______"></span>**-append**   
将跟踪消息追加到由 **-f**参数指定的事件跟踪日志（.etl）文件中。 默认为创建新文件。

此参数仅在包含 **-f**的命令中有效，不包括 **-rt**或 **-cir**。

<span id="_______-b_______BufferSize______"></span><span id="_______-b_______buffersize______"></span><span id="_______-B_______BUFFERSIZE______"></span>**-b** *BufferSize*   
指定为跟踪会话分配的每个缓冲区的大小（以 KB 为单位）。 默认值由处理器数量、物理内存量和使用中的操作系统决定。

<span id="-bt_n"></span><span id="-BT_N"></span>**-bt** *n*  
指定开始刷新之前要填充的缓冲区数（*n*）。 从 Windows 8.1 开始可使用此选项。

<span id="_______-buffering______"></span><span id="_______-BUFFERING______"></span>**-缓冲**   
启动缓冲跟踪会话。

在缓冲跟踪会话中，跟踪消息将保留在跟踪缓冲区中。 它们不会发送到跟踪使用者或记录在跟踪日志中。

<span id="_______-cir_______MaxFileSize______"></span><span id="_______-cir_______maxfilesize______"></span><span id="_______-CIR_______MAXFILESIZE______"></span>**-cir** *MaxFileSize*   
指定事件跟踪日志（.etl）文件中的循环日志记录（文件末尾，记录最早的消息）。 *MaxFileSize*指定文件的最大大小（MB）。 如果没有*MaxFileSize*值，则忽略此参数。

默认值为顺序日志记录，没有文件大小限制。

<span id="_______-cm______"></span><span id="_______-CM______"></span>**-cm**   
启用对注册表（Configuration Manager）访问的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="_______-critsec______"></span><span id="_______-CRITSEC______"></span>**-critsec**   
跟踪专用跟踪会话中进程的关键部分事件。 您可以在任何用户模式进程（甚至是未检测跟踪的用户模式进程）上启动关键部分进程记录器。

使用 **-pid**指定进程。 不要将 **-guid**与 **-critsec**一起使用。 系统为临界区跟踪定义自定义 GUID （CritSecGuid）。 不能在同一命令中使用 **-堆**和 **-critsec** 。

<span id="_______-dpcisr______"></span><span id="_______-DPCISR______"></span>**-dpcisr**   
启用对内核中延迟的过程调用（Dpc）、中断服务请求（Isr）、图像加载事件（**-img**）和上下文切换的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

仅适用于 Windows Vista 和更高版本的 WDK 的 Windows 驱动程序工具包中包含的 Tracelog 版本支持此选项。 **– Dpcisr**选项不能与 **-eflag**选项一起使用。

将 **-UsePerfCounter**参数与 **-dpcisr**一起使用。 此参数为每个事件提供唯一的时间戳，Tracerpt 是用于格式化和解释 DPC/ISR 事件的工具。 有关解释并设置这些事件的格式的信息，请参阅下面的 "注释"。

<span id="_______-eflag________n_________flag..._"></span><span id="_______-EFLAG________N_________FLAG..._"></span>**-eflag** *n* \[ *标志*.。。\]  
使用其他标志为[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)启用内核事件，最值得注意的是启用对 DPC、ISR 和上下文切换事件的跟踪的标志。 **-Eflag**选项不能与 **– dpcisr**选项一起使用。

<span id="_______-enableproperty________n______"></span><span id="_______-ENABLEPROPERTY________N______"></span>**-enableproperty** *n*   
请参阅作为参数传递给[EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)的*EnableParameters*结构中的*EnabledProperties*的说明和支持的值。

<span id="-EventIdFilter_____-in-out_n_id1_id2_..."></span><span id="-eventidfilter_____-in-out_n_id1_id2_..."></span><span id="-EVENTIDFILTER_____-IN-OUT_N_ID1_ID2_..."></span>**-EventIdFilter** {**-** | **out**} * * * * *n*  ****  *id1 id2 ...*  
指定包含*n*个事件 id 的事件 id 筛选器（允许的最大64事件 id）。 从 Windows 8.1 开始可使用此选项。

<span id="___-ExeFilter____Executable_file____Executable_file_...__"></span><span id="___-exefilter____executable_file____executable_file_...__"></span><span id="___-EXEFILTER____EXECUTABLE_FILE____EXECUTABLE_FILE_...__"></span>**-ExeFilter** *可执行 \_ 文件* \[ **;** *可执行 \_ 文件*.。。\]   
指定要筛选的可执行文件的名称。 您可以指定文件的列表。 使用分号分隔文件的名称。 排除未列出的文件。 从 Windows 8.1 开始可使用此选项。

<span id="_______-f___LogFile_"></span><span id="_______-f___logfile_"></span><span id="_______-F___LOGFILE_"></span>**-f** \[*日志文件*\]  
启动跟踪日志会话。 *LogFile*指定事件跟踪日志（.etl）文件的路径（可选）和文件名。 默认值为 C： \\ LogFile。 若要将文件置于远程计算机上，请在路径中包括计算机名称或 IP 地址。

如果将 **-rt**与 **-f**一起使用，则会将跟踪消息发送到使用者，并发送到事件跟踪日志文件。 不能使用 **-rt**或 **-f**和 **-缓冲**。

<span id="_______-fio______"></span><span id="_______-FIO______"></span>**-fio**   
启用文件 i/o 事件的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="_______-flag_______Flag______"></span><span id="_______-flag_______flag______"></span><span id="_______-FLAG_______FLAG______"></span>**-标志***标志*   
> [!NOTE]
> 标志已由关键字取代。 使用 **-matchanykw** ，除非要启用 WPP 提供程序。

指定跟踪会话中[提供程序](trace-provider.md)的[跟踪标志](trace-flags.md)。 标志值确定跟踪提供程序生成的事件。

*标志*表示在跟踪提供程序中定义的标志值（采用十进制或十六进制格式）。 默认值为 0。 0x01000000 到0xFF000000 的值保留供将来使用。

标志值的含义由每个跟踪提供程序单独定义。 通常，标志表示越来越详细的报表级别。

在**tracelog**命令中指定的标志值适用于跟踪会话中的所有跟踪提供程序。 若要为每个跟踪提供程序设置不同的标志，请使用**tracelog**。

<span id="_______-ft_______FlushTime______"></span><span id="_______-ft_______flushtime______"></span><span id="_______-FT_______FLUSHTIME______"></span>**-ft** *FlushTime*   
指定刷新跟踪消息缓冲区的频率（以秒为单位）。 最小刷新时间为1秒。 默认值为0（无强制刷新）。

此强制刷新除了跟踪消息缓冲区已满和跟踪会话停止时自动发生的刷新之外。

请参阅**tracelog-flush 命令**。

<span id="_______-guid___GUID___GUIDFile_"></span><span id="_______-guid___guid___guidfile_"></span><span id="_______-GUID___GUID___GUIDFILE_"></span>**-guid** {* \# guid*  |  *文件名*  |  * \* *}  
启用指定的跟踪提供程序。

如果指定文件，Tracelog 将为文件中指定的所有提供程序启用跟踪。 该文件的格式必须为：

```text
; comment line
guid1;matchanykeyword;level
guid2;matchanykeyword;level
```

如果指定了提供程序 GUID，则必须使用数字符号（）前面 GUID *\#* 。

如果指定了提供程序名称，则该名称必须为前面（ *\** ）。 然后，将使用与相同的算法将该名称转换为 GUID。NET 的事件源。 此 GUID 随后将用于启用提供程序。

如果省略此参数，则任何跟踪提供程序都不会向跟踪会话发送消息。 但是，在启动跟踪会话后，可以使用**tracelog**命令为会话启用一个或多个跟踪提供程序。

<span id="_______-gs______"></span><span id="_______-GS______"></span>**-gs**   
为每个跟踪消息生成全局序列号。

全局序列号对于计算机上的所有跟踪会话都是唯一的。 默认情况下，没有序列号。

此参数对于 NT 内核记录器跟踪会话无效。

<span id="_______-heap______"></span><span id="_______-HEAP______"></span>**-堆**   
跟踪用户模式进程的堆内存事件。 您可以在任何用户模式进程（甚至是未检测跟踪的进程）上启动堆进程记录器。

使用 **-pid**指定进程。 不要将 **-guid**与 **-堆**一起使用。 系统为堆内存跟踪定义自定义 GUID （HeapGuid）。 不能在同一命令中使用 **-堆**和 **-critsec** 。

<span id="_______-hf______"></span><span id="_______-HF______"></span>**-hf**   
启用对硬页面错误（需要访问磁盘的页错误）的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="-hybridshutdown_stoppersist"></span><span id="-HYBRIDSHUTDOWN_STOPPERSIST"></span>**-hybridshutdown** {**stop** | **持久**}  
控制混合关闭记录器的行为。 从 Windows 8 开始可以使用此选项。

如果系统执行混合关闭，*停止*将导致会话停止。
*持久性*将导致在系统重新启动混合关闭后会话继续进行。

<span id="_______-img______"></span><span id="_______-IMG______"></span>**-m g**   
启用对图像加载事件的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="___-independent___"></span><span id="___-INDEPENDENT___"></span>**独立**   
> [!NOTE]
> 应在每个跟踪会话上启用独立模式。

启用跟踪会话上的独立模式。 独立模式允许会话收集其他非独立模式会话已删除的事件。 从 Windows 8.1 开始可使用此选项。

<span id="_______-kb______"></span><span id="_______-KB______"></span>**-kb**   
对于日志文件大小，请使用 kb。 默认值为兆字节（MB）。

<span id="_______-kd______"></span><span id="_______-KD______"></span>**-kd**   
将跟踪消息重定向到 KD 或 Windbg，无论附加哪个。 此参数还将跟踪缓冲区大小设置为 3 KB，为调试器设置最大缓冲区大小，并忽略命令中的任何 **-b**参数。

使用 **-kd**提交 Tracelog 命令时，调试器必须运行。 否则，Tracelog 将停止响应。

有关在内核调试器中显示跟踪消息的信息，请参阅注释。

**-Lbr** *事件 \[ **+** 名称： + ... \] ： filter \[ **、** filter,... \] *  
在内核事件上配置 LBR 跟踪。

有关内核事件的列表，请使用 **-Eflag 帮助**。

<span id="_______-level________n______"></span><span id="_______-LEVEL________N______"></span>**-级别** *n*   
指定跟踪会话中提供程序的[跟踪级别](trace-level.md)。 级别确定跟踪提供程序生成的事件。

*Level*表示以十进制或十六进制格式表示的级别值。 默认值为 0。

级别值的含义由每个跟踪提供程序单独定义。 通常，跟踪级别表示事件的严重级别（信息、警告或错误）。

在**tracelog**命令中指定的级别值适用于跟踪会话中的所有跟踪提供程序。 若要为每个跟踪提供程序设置不同的级别，请使用**tracelog**。

<span id="_______-lowcapacity______"></span><span id="_______-LOWCAPACITY______"></span>**-lowcapacity**   
> [!NOTE]
> 除非有必要，否则不应使用此选项以降低内存开销。 使用此选项可以使每个事件的日志速度较慢。

一次使用单个缓冲区收集在多个处理器上生成的事件。 此选项选择 \_ \_ \_ 每个 \_ 处理器 \_ 缓冲日志记录模式下的事件跟踪。 有关详细信息，请参阅 Windows SDK。

<span id="_______-ls______"></span><span id="_______-LS______"></span>**-ls**   
为每个跟踪消息生成本地序列号。

本地序列号在跟踪会话中是唯一的。 默认情况下，没有序列号。

此参数对于 NT 内核记录器跟踪会话无效。

<span id="_______-max_______NumberOfBuffers______"></span><span id="_______-max_______numberofbuffers______"></span><span id="_______-MAX_______NUMBEROFBUFFERS______"></span>**-最大** *NumberOfBuffers*   
指定 Tracelog 为跟踪会话分配的最大缓冲区数。 默认值由处理器数量、物理内存量和使用中的操作系统决定。

<span id="_______-matchallkw________n______"></span><span id="_______-MATCHALLKW________N______"></span>**-matchallkw** *n*   
指定*MatchAllKeyWord*位掩码，该位掩码限制提供程序写入的事件的类别，并与 **-matchanykw**选项一起使用。

此位掩码是可选的。 如果事件的关键字满足-**matchanykw**选项中指定的条件，则只有在此掩码中的所有位都存在于事件的关键字中时，提供程序才会编写事件。 如果 **-matchanykw**为零，则不使用此掩码。

Tracelog 传递[EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)函数调用的*MatchAllKeyWord*参数中的值*n* 。 有关详细信息，请参阅 Windows SDK。

<span id="_______-matchanykw________n______"></span><span id="_______-MATCHANYKW________N______"></span>**-matchanykw** *n*   
指定*MatchAnyKeyword*位掩码，该位掩码确定提供程序写入的事件的类别。

如果任何事件的关键字位与此掩码中设置的任何位均匹配，则提供程序将写入事件。 Tracelog 传递[EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)函数调用的*MatchAnyKeyWord*参数中的值*n* 。 有关详细信息，请参阅 Windows SDK。

<span id="_______-min_______NumberOfBuffers______"></span><span id="_______-min_______numberofbuffers______"></span><span id="_______-MIN_______NUMBEROFBUFFERS______"></span>**-最小** *NumberOfBuffers*   
指定最初为存储跟踪消息分配的缓冲区数。 当缓冲区已满时，Tracelog 将分配更多的缓冲区，直到达到最大值。 默认值由处理器数量、物理内存量和使用中的操作系统决定。

<span id="_______-newfile_______MaxFileSize______"></span><span id="_______-newfile_______maxfilesize______"></span><span id="_______-NEWFILE_______MAXFILESIZE______"></span>**-newfile** *MaxFileSize*   
每当现有文件到达*MaxFileSize*时，创建新的事件跟踪日志（.etl）文件。 *MaxFileSize*指定每个日志文件的最大大小（MB）。 如果没有*MaxFileSize*值，则忽略此参数。

使用 **-newfile**时，还必须使用 **-f** *logfile*参数，而*LogFile*的值必须是包含字符 **% d**的名称，以指示小数模式，例如，trace% d. .etl。 否则，该命令将失败并返回 \_ 无效 \_ 名称。 每次创建新文件时，Windows 都会递增文件名中的十进制值。

此参数对于预先分配（**-prealloc**）、循环日志记录（**-CIR**）、NT 内核记录器会话或专用跟踪会话无效。

<span id="_______-nodisk______"></span><span id="_______-NODISK______"></span>**-nodisk**   
禁用物理磁盘 i/o 事件的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="_______-nonet______"></span><span id="_______-NONET______"></span>**-nonet**   
禁用对 TCP/IP 和用户数据报协议（UDP）事件的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="_______-noprocess______"></span><span id="_______-NOPROCESS______"></span>**-noprocess**   
禁止跟踪每个进程的开始和结束。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="_______-nothread______"></span><span id="_______-NOTHREAD______"></span>**-nothread**   
禁止跟踪每个线程的开始和结束。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="_______-paged______"></span><span id="_______-PAGED______"></span>**-分页**   
为跟踪消息缓冲区使用可分页内存。 默认情况下，事件跟踪使用不可分页 memory 作为缓冲区。

需要不可分页内存的提供程序将不能将事件记录到使用可分页内存的会话中。

<span id="_______-pids________PIDs_PID__PID..._"></span><span id="_______-pids________pids_pid__pid..._"></span><span id="_______-PIDS________PIDS_PID__PID..._"></span>**-pid** * \# pid pid* \[ *pid*.。。\]  
指定运行堆内存或临界区跟踪会话的用户模式进程。 仅对**堆**或 **-critsec**有效。

* \# Pid*指定与此参数一起列出的进程 id 的数量。 *PID*表示进程标识符。 可以通过此参数最多指定10个 Pid。

当提供程序在多个进程中运行时（例如，当一个程序创建多个进程时），列出多个 Pid。

<span id="___-PidFilter____n_pid1_pid2_..."></span><span id="___-pidfilter____n_pid1_pid2_..."></span><span id="___-PIDFILTER____N_PID1_PID2_..."></span>**-PidFilter** *n* *pid1 pid2 ...*  
指定包含*n* Pid 的 Pid 筛选器（允许最多8个）。 从 Windows 8.1 开始可使用此选项。

<span id="_______-pf______"></span><span id="_______-PF______"></span>**-pf**   
启用对所有页面错误的跟踪。 此参数仅对 NT 内核记录器跟踪会话有效。

<span id="___________________-PkgIdFilter____Package_Full_Name____Package_Full_Name..._"></span><span id="___________________-pkgidfilter____package_full_name____package_full_name..._"></span><span id="___________________-PKGIDFILTER____PACKAGE_FULL_NAME____PACKAGE_FULL_NAME..._"></span>**-PkgIdFilter** *包的完整名称* \[  * *; * * * 包的完整名称*.。。\]  
指定包 ID 筛选器。 可以指定包文件的列表。 使用分号分隔文件的名称。

<span id="___-PkgAppIdFilter_____PRAID____PRAID..._"></span><span id="___-pkgappidfilter_____praid____praid..._"></span><span id="___-PKGAPPIDFILTER_____PRAID____PRAID..._"></span>**-PkgAppIdFilter** *PRAID* \[ * *; * * * PRAID*.。。\]  
指定包相对应用标识符（PRAID）筛选器。 PRAID 是包中的应用程序的唯一标识符。 可以指定多个*PRAID*。 使用分号分隔 Id。 此选项可用于从 Windows 8.1 开始的 UWP 应用。

<span id="-Pmc_Ctrs_Events"></span><span id="-pmc_ctrs_events"></span><span id="-PMC_CTRS_EVENTS"></span>**-Pmc** *Ctr1，Ctr2,...： name + name + ...*  
在指定的内核事件上配置性能监视器计数器（PMC）采样。 从 Windows 8 开始可以使用此选项。

使用 **-ProfileSource Help**获取计数器列表。
有关内核事件的列表，请使用 **-Eflag 帮助**。

<span id="_______-prealloc______"></span><span id="_______-PREALLOC______"></span>**-prealloc**   
在启动会话之前，为 .etl 文件预留空间。

此参数需要 **-seq**或 **-cir** with *MaxFileSize*。 它对于 **-newfile**无效。

<span id="-ProfileSource_src"></span><span id="-profilesource_src"></span><span id="-PROFILESOURCE_SRC"></span>**-ProfileSource** *src*  
配置要使用的分析源。 对于源列表，请使用命令**tracelog-ProfileSource Help**。 从 Windows 8 开始可以使用此选项。

此选项仅在 Windows 8 及更高版本的 Windows 上可用。

<span id="_______-rt______"></span><span id="_______-RT______"></span>**-rt**   
启动实时跟踪会话。 （跟踪日志会话（**-f**）是默认值。）

如果使用 **-rt**和 **-f**，则跟踪消息将发送到跟踪使用者，并发送到事件跟踪日志文件。 不能使用 **-rt**或 **-f**和 **-缓冲**。 有关详细信息，请参阅[Trace Session](trace-session.md)。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span>**-secure**   
在安全模式下启用跟踪。 此选项选择事件 \_ 跟踪 \_ 安全 \_ 模式日志记录模式。 限制可将事件记录到会话中的用户和具有 TRACELOG \_ 日志 \_ 事件权限的用户。

<span id="_______-sessionguid______"></span><span id="_______-SESSIONGUID______"></span>**-sessionguid**   
指定自动记录器会话 GUID 注册表值。

<span id="-SetProfInt_n_src"></span><span id="-setprofint_n_src"></span><span id="-SETPROFINT_N_SRC"></span>**-SetProfInt** *n*  ****  *src*  
> [!IMPORTANT]
> 不建议更改分析时间间隔。

为指定的源配置分析间隔（*n*），其中*n*以100ns 为单位。 默认值为10000（等效于1ms）。 从 Windows 8 开始可以使用此选项。

<span id="_______-seq_______MaxFileSize______"></span><span id="_______-seq_______maxfilesize______"></span><span id="_______-SEQ_______MAXFILESIZE______"></span>**-seq** *MaxFileSize*   
指定事件跟踪日志（.etl）文件的顺序日志记录（文件结尾、停止记录事件）。 *MaxFileSize*指定文件的最大大小（MB）。 如果没有*MaxFileSize*值，则忽略此参数。

顺序日志记录是默认值，但你可以使用此参数设置最大文件大小或使用 **-prealloc**。 如果没有此参数，则没有文件大小限制。

<span id="_______-sourceguid________SourceGuid______"></span><span id="_______-sourceguid________sourceguid______"></span><span id="_______-SOURCEGUID________SOURCEGUID______"></span>**-sourceguid** *sourceguid*   
将作为*SourceId*参数传递的 GUID 指定给[EnableTraceEx](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex)或[EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)函数。 *SourceId*标识启用了提供程序的会话。

**-stackwalk** \[*事件*\]  
指定要在其上收集堆栈的内核事件。 有关内核事件的列表，请使用 **-Eflag 帮助**。 此参数仅对 NT 内核记录器或系统记录器跟踪会话有效。

<span id="________________-StackWalkFilter_-in-outnid1_id2_..."></span><span id="________________-stackwalkfilter_-in-outnid1_id2_..."></span><span id="________________-STACKWALKFILTER_-IN-OUTNID1_ID2_..."></span>**-StackWalkFilter** {**-** | **out**}*nid1 id2 ...*  
指定包含*n*个事件 id 的事件 id 筛选器（允许的最大64事件 id）。 从 Windows 8.1 开始可使用此选项。

<span id="-systemlogger"></span><span id="-SYSTEMLOGGER"></span>**-systemlogger**  
记录器可以接收 SystemTraceProvider 事件。 请参阅[配置和启动 SystemTraceProvider 会话](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-a-systemtraceprovider-session)。 从 Windows 8 开始可以使用此选项。

<span id="_______-um______"></span><span id="_______-UM______"></span>**-um**   
指定专用跟踪会话此参数对于专用跟踪会话是必需的。

<span id="_______-UseCPUCycle______"></span><span id="_______-usecpucycle______"></span><span id="_______-USECPUCYCLE______"></span>**-UseCPUCycle**   
使用处理器频率（也称为 "CPU 刻度"）来度量每个跟踪消息的时间。

此计时器提供可能的最高分辨率，但很容易出错，尤其是在电源管理系统和多处理器计算机上。 例如，如果在具有 ARM 处理器的计算机上指定此计时器，则可能会导致无序事件。 相反，建议使用 **-UsePerfCounter**进行高分辨率跟踪。

**-UsePerfCounter**是事件跟踪的默认计时器。

<span id="_______-UsePerfCounter______"></span><span id="_______-useperfcounter______"></span><span id="_______-USEPERFCOUNTER______"></span>**-UsePerfCounter**   
记录高分辨率性能计数器时钟的值，而不是每个跟踪消息。

由于性能计数器时钟的计数大约为100毫微秒，因此它为每个事件提供唯一的时间戳。

**-UsePerfCounter**是事件跟踪的默认计时器。

<span id="_______-UseSystemTime______"></span><span id="_______-usesystemtime______"></span><span id="_______-USESYSTEMTIME______"></span>**-UseSystemTime**   
记录每个跟踪消息的系统时间，而不是高分辨率性能计数器时钟时间。 由于系统计时器的分辨率为10毫秒（与性能计数器时钟相比，100毫微秒），因此多个事件可能具有相同的系统时间。

**-UsePerfCounter**是事件跟踪的默认计时器。

<span id="_______-_____help___-_______"></span><span id="_______-_____HELP___-_______"></span>**-？ | help |-？**   
显示用法信息。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

以下注释适用于多个 Tracelog 命令。

### <a name="span-idsyntax_errorsspanspan-idsyntax_errorsspansyntax-errors"></a><span id="syntax_errors"></span><span id="SYNTAX_ERRORS"></span>语法错误

Tracelog 不会显示所有错误语法组合的错误，例如当你尝试更新不能更改的设置时。 相反，它将忽略命令的无效部分并显示成功消息。

### <a name="span-idsystem_loggersspanspan-idsystem_loggersspansystem-loggers"></a><span id="system_loggers"></span><span id="SYSTEM_LOGGERS"></span>系统记录器

Windows 出于多种目的使用跟踪会话，其中一些操作对于正常操作至关重要。 请勿停止未启动的任何跟踪会话。

### <a name="span-idenumguidspanspan-idenumguidspanenumguid"></a><span id="enumguid"></span><span id="ENUMGUID"></span>Enumguid

若要确定**tracelog**或**tracelog**命令是否成功，请使用**tracelog-enumguid**命令确定是否启用了提供程序，然后使用**tracelog-l （List）** 命令检查跟踪会话的属性。

### <a name="span-idreal_time_and_log_sessionsspanspan-idreal_time_and_log_sessionsspanreal-time-and-log-sessions"></a><span id="real_time_and_log_sessions"></span><span id="REAL_TIME_AND_LOG_SESSIONS"></span>实时和日志会话

跟踪会话既可以是实时跟踪会话，也可以是跟踪日志会话。 如果在同一命令中包括 **-rt** （实时）和 **-f** （日志会话）参数，系统会将缓冲区内容同时发送到日志和跟踪使用者。 但是，必须先使用**tracelog**命令刷新缓冲区，然后才能将实时消息传递添加到跟踪日志会话中。

如果启动实时会话（**-rt**），然后更新到日志会话（**-f**），则任何新的跟踪消息只发送到日志文件。 若要将日志文件添加到实时会话，请在**tracelog**命令中使用 **-rt**和 **-f** 。

如果启动一个日志会话（**-f**），则可以更新为实时会话（**-rt**），但仍会将消息继续发送到跟踪使用者之外的日志。 你无法通过更新从会话中消除日志。

若要显示或保存实时会话中的跟踪消息，还可以使用跟踪使用者（如[Tracefmt](tracefmt.md)）或使用[TraceView](traceview.md)，这是跟踪控制器（如 Tracelog）和跟踪使用者。 当使用 Tracefmt 时，请确保在 Tracefmt 命令中包含 **-rt**参数。

### <a name="span-idflags_and_levelsspanspan-idflags_and_levelsspanflags-and-levels"></a><span id="flags_and_levels"></span><span id="FLAGS_AND_LEVELS"></span>标志和级别

大多数跟踪提供程序不会生成任何跟踪消息，除非将标志或级别设置为特定值。 提供程序使用标志或级别来控制正在跟踪的内容。 如果事件跟踪日志文件为空，请在跟踪提供程序中查看标志和级别。

若要确保始终生成跟踪消息，请完成以下步骤：

1.  将**flags**参数设置为0xffffffff 即可启用所有标志设置。

2.  将**色阶**参数设置为255可启用所有级别设置。

### <a name="span-idthe__eflag_parameterspanspan-idthe__eflag_parameterspanthe--eflag-parameter"></a><span id="the__eflag_parameter"></span><span id="THE__EFLAG_PARAMETER"></span>-Eflag 参数

Tracelog 具有一个 **-eflag** （扩展标志）参数，该参数旨在为[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)启用其他标志-最值得注意的是启用对 DPC、ISR 和上下文切换事件的跟踪的标志。 由于**tracelog**命令现在包含 **-dpcisr**参数，因此不再需要使用 **-eflag**参数，因此不建议使用。

### <a name="span-idoutdated_parametersspanspan-idoutdated_parametersspanoutdated-parameters"></a><span id="outdated_parameters"></span><span id="OUTDATED_PARAMETERS"></span>过期参数

在以前版本的 Tracelog 中， **Tracelog**命令支持 **-rt b**参数组合。 此组合已被 **-缓冲**参数替换，它不再有效。

已删除 **-x**参数，因为停止所有跟踪会话可能会导致系统不稳定。

已删除 **-disableex**参数。 改用 **-disable** 。

### <a name="span-idnt_kernel_loggerspanspan-idnt_kernel_loggerspannt-kernel-logger"></a><span id="nt_kernel_logger"></span><span id="NT_KERNEL_LOGGER"></span>NT 内核记录器

若要使用 NT 内核记录器启动跟踪会话，请从**tracelog**命令中省略会话名称，并且不要使用 **-guid**参数指定提供程序 guid 文件。 **"NT 内核记录器"** 是默认的会话名称。

如果会话名称被省略或为 **"NT 内核记录器"**，则系统会启动一个 NT 内核记录器跟踪会话，即使您使用 **-Guid**参数指定**SYSTEMTRACECONTROLGUID**之外的 guid （NT 内核记录器跟踪会话的控件 guid）也是如此。 如果指定一个不同的 GUID，系统将返回错误（"系统记录器不接受应用程序 guid"），但仍会启动 NT 内核记录器跟踪会话。

默认情况下，当 Tracelog 启动 NT 内核记录器跟踪会话时，它将启用对进程、线程、物理磁盘 i/o 和 TCP/IP 事件的跟踪，但你可以使用参数禁用对这些事件的跟踪，并启用跟踪其他事件。

### <a name="span-iddpc_isr_eventsspanspan-iddpc_isr_eventsspandpcisr-events"></a><span id="dpc_isr_events"></span><span id="DPC_ISR_EVENTS"></span>DPC/ISR 事件

由于 Tracerpt 需要系统性能计数器时钟时间作为时间戳，因此在启动跟踪会话时，请使用 Tracelog **-UsePerfCounter**参数。

由于 DPC 和 ISR 事件是通过特殊检测收集的，因此它们不会出现在 Tracelog 显示的表的**启用跟踪**行中以确认命令。

有关详细信息，请参阅[示例15：测量 DPC/ISR Time](example-15--measuring-dpc-isr-time.md)。
