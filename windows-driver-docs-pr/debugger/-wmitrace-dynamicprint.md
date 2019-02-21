---
title: wmitrace.dynamicprint
description: Wmitrace.dynamicprint 扩展控制调试器是否显示由运行在 KD_FILTER_MODE 会话生成的跟踪消息。
ms.assetid: 458a9dfa-e3cc-4652-a9e5-5098a962f1c7
keywords:
- wmitrace.dynamicprint Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dynamicprint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e7cb0158b16894603df4abf156196fd179904eab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520433"
---
# <a name="wmitracedynamicprint"></a>!wmitrace.dynamicprint


**！ Wmitrace.dynamicprint**扩展控制调试器是否显示由运行在 KD 会话生成的跟踪消息\_筛选器\_模式。

```dbgcmd
!wmitrace.dynamicprint {0 | 1}
```

## <a name="span-idddkwmitracedynamicprintdbgspanspan-idddkwmitracedynamicprintdbgspanparameters"></a><span id="ddk__wmitrace_dynamicprint_dbg"></span><span id="DDK__WMITRACE_DYNAMICPRINT_DBG"></span>参数


<span id="_______0______"></span> **0**   
关闭跟踪消息显示。

<span id="_______1______"></span> **1**   
打开跟踪消息显示。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 在启动跟踪会话的帮助，请参阅"Tracelog"Windows Driver Kit (WDK) 中。

<a name="remarks"></a>备注
-------

使用此扩展插件之前，启动跟踪会话，并指定应将跟踪消息发送到调试器。 例如，如果您使用[ **！ wmitrace.start** ](-wmitrace-start.md)若要启动会话，请使用 **-kd**参数。 如果使用 Tracelog 来启动跟踪会话，使用其 **-kd**参数。 跟踪日志 (tracelog.exe) 是 Windows 驱动程序工具包中包含的跟踪控制器。

跟踪消息保存在目标计算机上缓冲区中。 这些缓冲区刷新，并发送到调试器，按固定间隔在主计算机上。 可以通过使用指定的刷新计时器间隔 **-kd**的参数[ **！ wmitrace.start** ](-wmitrace-start.md)命令或 **-kd**参数跟踪日志工具中。 从开始 Windows 8 中，您可以指定刷新计时器值以毫秒为单位通过追加**ms**为刷新计时器值。

默认情况下，ETW 会维护目标计算机上的每个处理器跟踪缓冲区。 当跟踪缓冲区会刷新，然后发送到主机计算机上的调试器时，没有将缓冲区合并到的事件按时间顺序的机制。 因此可能不按顺序显示的事件。 从 Windows 7 中，您可以通过设置来解决此问题 **-lowcapacity**参数时使用的跟踪日志工具以启动跟踪会话。

**Tracelog** *MySession* **-kd lowcapacity**

当启动会话 **-lowcapacity**设置，所有事件的目标计算机上，都转到一个缓冲区和主机计算机上的调试器中正确的顺序显示的事件。

此外，在使用此扩展之前, 使用[ **！ wmitrace.searchpath** ](-wmitrace-searchpath.md)或[ **！ wmitrace.tmffile** ](-wmitrace-tmffile.md)指定跟踪消息格式文件。 系统使用跟踪消息格式文件，以便它们可以显示为用户可读文本设置格式的二进制跟踪消息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!wmitrace.start**](-wmitrace-start.md)

 

 






