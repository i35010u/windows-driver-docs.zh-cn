---
title: wmitrace 记录器
description: Wmitrace 扩展显示有关跟踪会话的数据，包括会话配置数据。 此扩展不显示在会话过程中生成的跟踪消息。
keywords:
- wmitrace Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.logger
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c6e67ed767f79980883b73218fb75981918e3768
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823535"
---
# <a name="wmitracelogger"></a>!wmitrace.logger


**！ Wmitrace** 扩展显示有关跟踪会话的数据，包括会话配置数据。 此扩展不显示在会话过程中生成的跟踪消息。

```dbgcmd
!wmitrace.logger [ LoggerID | LoggerName ]
```

## <a name="span-idddk__wmittrace_logger_dbgspanspan-idddk__wmittrace_logger_dbgspanparameters"></a><span id="ddk__wmittrace_logger_dbg"></span><span id="DDK__WMITTRACE_LOGGER_DBG"></span>参数


<span id="_______LoggerID______"></span><span id="_______loggerid______"></span><span id="_______LOGGERID______"></span>*LoggerID*   
指定跟踪会话。 *LoggerID* 是系统分配给计算机上每个跟踪会话的序号。 如果未指定参数，则使用 ID 等于1的跟踪会话。

<span id="_______LoggerName______"></span><span id="_______loggername______"></span><span id="_______LOGGERNAME______"></span>*LoggerName*   
指定跟踪会话。 *LoggerName* 是启动跟踪会话时指定的文本名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace.dll 文件从 Windows 的调试工具安装目录的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。

<a name="remarks"></a>备注
-------

此扩展是为性能日志和事件而设计的，不能在用户可读的显示中对其进行格式化。 若要在跟踪会话缓冲区中显示跟踪消息以及标头数据，请使用 [**！ wmitrace. logdump**](-wmitrace-logdump.md)。

若要查找跟踪会话的记录器 ID，请使用 [**！ wmitrace**](-wmitrace-strdump.md) 扩展名。 另外，还可以使用 Tracelog 命令 Tracelog-l 来列出跟踪会话及其基本属性，其中包括记录器 ID。

 

 





