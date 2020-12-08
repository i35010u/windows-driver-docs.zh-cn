---
title: wmitrace.logdump
description: Wmitrace. logdump 扩展显示跟踪会话的跟踪缓冲区的内容。 可以限制显示以跟踪来自指定提供程序的消息。
keywords:
- wmitrace logdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a58411c8e59f23cc1bb89e07f171d18622b7314f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823533"
---
# <a name="wmitracelogdump"></a>!wmitrace.logdump


**！ Wmitrace logdump** 扩展显示跟踪会话的跟踪缓冲区的内容。 可以限制显示以跟踪来自指定提供程序的消息。

```dbgcmd
!wmitrace.logdump [-t Count] [{LoggerID|LoggerName} [GUIDFile]] 
```

## <a name="span-idddk__wmitrace_logdump_dbgspanspan-idddk__wmitrace_logdump_dbgspanparameters"></a><span id="ddk__wmitrace_logdump_dbg"></span><span id="DDK__WMITRACE_LOGDUMP_DBG"></span>参数


<span id="_______-t_______Count______"></span><span id="_______-t_______count______"></span><span id="_______-T_______COUNT______"></span>**-t** *计数*   
将输出限制为最近的消息。 *Count* 指定要显示的消息数。

<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span>*LoggerID*   
指定跟踪会话。 *LoggerID* 是系统分配给计算机上每个跟踪会话的序号。 如果未指定参数，则使用 ID 等于1的跟踪会话。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
指定跟踪会话。 *LoggerName* 是启动跟踪会话时指定的文本名称。

<span id="_______GUIDFile______"></span><span id="_______guidfile______"></span><span id="_______GUIDFILE______"></span>*GUIDFile*   
仅显示 *GUIDFile* 文件中指定的提供程序中的跟踪消息。 *GUIDFile* 表示包含一个或多个跟踪提供程序（如 guid 或 ctl 文件）的控件 guid 的文本文件 (可选) 和文件名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace.dll 文件从 Windows 的调试工具安装目录的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关 Tracelog 的信息，请参阅 Windows 驱动程序工具包中的 "Tracelog" (WDK) 。

<a name="remarks"></a>备注
-------

在 Windows 软件跟踪预处理器 (WPP) 软件跟踪时，跟踪会话缓冲区用于存储跟踪消息，直到它们被刷新到日志文件或跟踪使用者实时显示。 **！ Wmitrace logdump** 扩展显示物理内存中缓冲区的内容。 显示将显示在调试器命令窗口中。

此扩展在发生崩溃时恢复最新的跟踪特别有用，并显示崩溃转储文件中存储的跟踪。

使用此扩展之前，请使用 [**！ wmitrace; searchpath**](-wmitrace-searchpath.md) 或 [**！ wmitrace**](-wmitrace-tmffile.md) 来指定跟踪消息格式的文件。 系统使用跟踪消息格式文件来设置缓冲区中的二进制跟踪消息的格式，以便可以将它们显示为可读文本。

**注意**  如果驱动程序使用的是 UMDF 1.11 版或更高版本，则不需要使用 [**！ wmitrace**](-wmitrace-searchpath.md) 或 [**tmffile**](-wmitrace-tmffile.md)。

 

如果使用 Tracelog 启动具有循环缓冲的跟踪会话 ( 缓冲) ，请使用此扩展显示缓冲区内容。

若要查找跟踪会话的记录器 ID，请使用 [**！ wmitrace**](-wmitrace-strdump.md) 扩展名。 另外，还可以使用 Tracelog 命令 Tracelog-l 来列出跟踪会话及其基本属性，其中包括记录器 ID。

此扩展仅在 WPP 软件跟踪过程中有用，更早 (适用于 Windows 的事件跟踪的旧) 方法。 其他显示的提供程序生成的跟踪事件不会使用跟踪消息格式 (TMF) 文件，因此此扩展不显示其内容。

此扩展类似于 [**！ wmitrace eventlogdump**](-wmitrace-eventlogdump.md) 扩展，只不过 **！ wmitrace** 的输出格式为 WPP 样式，而 **！ wmitrace** 的输出格式设置为事件日志样式。 应选择其格式适合于要显示的数据的扩展。

有关如何查看 UMDF 跟踪日志的信息，请参阅 [在基于 UMDF 的驱动程序中使用 WPP 软件跟踪](../wdf/using-wpp-software-tracing-in-umdf-drivers.md#viewing-the-umdf-trace-log)。

 

