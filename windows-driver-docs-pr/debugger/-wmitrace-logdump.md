---
title: wmitrace.logdump
description: Wmitrace.logdump 扩展显示为跟踪会话跟踪缓冲区的内容。 您可以从指定的提供程序将显示限定为跟踪消息。
ms.assetid: 073338c6-68c4-4ae0-b69e-392256277236
keywords:
- wmitrace.logdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d9896a368c1369327762f48d5dfeefb3de69e91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346357"
---
# <a name="wmitracelogdump"></a>!wmitrace.logdump


**！ Wmitrace.logdump**扩展显示为跟踪会话跟踪缓冲区的内容。 您可以从指定的提供程序将显示限定为跟踪消息。

```dbgcmd
!wmitrace.logdump [-t Count] [{LoggerID|LoggerName} [GUIDFile]] 
```

## <a name="span-idddkwmitracelogdumpdbgspanspan-idddkwmitracelogdumpdbgspanparameters"></a><span id="ddk__wmitrace_logdump_dbg"></span><span id="DDK__WMITRACE_LOGDUMP_DBG"></span>参数


<span id="_______-t_______Count______"></span><span id="_______-t_______count______"></span><span id="_______-T_______COUNT______"></span> **-t** *Count*   
将输出限制为最新的消息。 *计数*指定要显示的消息数。

<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span> *LoggerID*   
指定跟踪会话。 *LoggerID*是一个系统将分配到计算机上每个跟踪会话的序号。 如果未不指定任何参数，则使用跟踪会话 id 等于 1。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span> *LoggerName*   
指定跟踪会话。 *LoggerName*时的文本名称为指定开始跟踪会话时。

<span id="_______GUIDFile______"></span><span id="_______guidfile______"></span><span id="_______GUIDFILE______"></span> *GUIDFile*   
显示仅跟踪消息中指定的提供程序从*GUIDFile*文件。 *GUIDFile*表示的路径 （可选） 和包含该控件的一个或多个跟踪提供程序，例如.guid 或.ctl 文件的 Guid 的文本文件的文件名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪日志的信息，请参阅"Tracelog"Windows Driver Kit (WDK) 中。

<a name="remarks"></a>备注
-------

Windows 软件跟踪预处理器 (WPP) 软件在跟踪过程中，跟踪会话缓冲区用于存储跟踪消息，直到它们被刷新到日志文件或实时显示的跟踪使用者。 **！ Wmitrace.logdump**扩展插件都会显示在物理内存缓冲区的内容。 显示调试器命令窗口中显示。

此扩展在崩溃时，恢复最新的跟踪并显示故障转储文件中存储的跟踪尤其有用。

使用此扩展插件之前，请使用[ **！ wmitrace.searchpath** ](-wmitrace-searchpath.md)或[ **！ wmitrace.tmffile** ](-wmitrace-tmffile.md)指定跟踪消息格式文件。 系统使用跟踪消息格式文件，以便它们可以显示为用户可读文本设置格式的缓冲区中的二进制跟踪消息。

**请注意**  如果您的驱动程序使用 UMDF 版本 1.11 或更高版本，不需要使用[ **！ wmitrace.searchpath** ](-wmitrace-searchpath.md)或者[ **！ wmitrace.tmffile**](-wmitrace-tmffile.md).

 

当您使用 Tracelog 循环缓冲启动跟踪会话 (-缓冲)，使用此扩展显示缓冲区内容。

若要查找的跟踪会话的记录器 ID，请使用[ **！ wmitrace.strdump** ](-wmitrace-strdump.md)扩展。 或者，您可以使用 Tracelog 命令 tracelog-l 列出跟踪会话及其基本属性，包括记录器 id。

此扩展在 WPP 软件跟踪和早期的 Windows 事件跟踪 （旧版） 方法期间才有用。 其他清单表示提供程序生成的跟踪事件不使用跟踪消息格式 (TMF) 文件，并因此此扩展不会显示其内容。

此扩展是类似于[ **！ wmitrace.eventlogdump** ](-wmitrace-eventlogdump.md)扩展，不同之处在于的输出 **！ wmitrace.logdump** WPP 样式，和输出格式 **！ wmitrace.eventlogdump**格式化为事件日志样式。 应选择其格式是适用于想要显示的数据的扩展。

有关如何查看 UMDF 跟踪日志的信息，请参阅[基于 UMDF 驱动程序中使用 WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff561391#viewing-the-umdf-trace-log)。

 

 





