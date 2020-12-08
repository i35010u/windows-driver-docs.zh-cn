---
title: wmitrace.dynamicprint
description: Wmitrace. dynamicprint 扩展控制调试器是否显示 KD_FILTER_MODE 中运行的会话生成的跟踪消息。
keywords:
- wmitrace dynamicprint Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.dynamicprint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2995bbb29b282f4b22825a108f5e1a2db989bf0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823545"
---
# <a name="wmitracedynamicprint"></a>!wmitrace.dynamicprint


**！ Wmitrace dynamicprint** 扩展控制调试器是否显示由在 KD \_ FILTER 模式下运行的会话生成的跟踪消息 \_ 。

```dbgcmd
!wmitrace.dynamicprint {0 | 1}
```

## <a name="span-idddk__wmitrace_dynamicprint_dbgspanspan-idddk__wmitrace_dynamicprint_dbgspanparameters"></a><span id="ddk__wmitrace_dynamicprint_dbg"></span><span id="DDK__WMITRACE_DYNAMICPRINT_DBG"></span>参数


<span id="_______0______"></span>**0**   
关闭跟踪消息显示。

<span id="_______1______"></span>**1**   
启用跟踪消息显示。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace.dll 文件从 Windows 的调试工具安装目录的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关启动跟踪会话的帮助，请参阅 Windows 驱动程序工具包 (WDK) 中的 "Tracelog"。

<a name="remarks"></a>备注
-------

使用此扩展之前，请启动跟踪会话，并指定应将跟踪消息发送到调试器。 例如，如果使用 [**！ wmitrace**](-wmitrace-start.md) 启动会话，请使用 **-kd** 参数。 如果使用 Tracelog 启动跟踪会话，请使用其 **-kd** 参数。 Tracelog ( # A0) 是 Windows 驱动程序工具包中包含的跟踪控制器。

跟踪消息保存在目标计算机上的缓冲区中。 这些缓冲区会定期刷新并发送到主计算机上的调试器。 您可以使用 [**！ wmitrace**](-wmitrace-start.md)命令的 **-Kd** 参数或 Tracelog 工具的 **-kd** 参数指定刷新计时器间隔。 从 Windows 8 开始，可以通过将 **ms** 追加到刷新计时器值来指定刷新计时器的值（以毫秒为单位）。

默认情况下，ETW 维护目标计算机上的每处理器跟踪缓冲区。 在主计算机上刷新跟踪缓冲区并将其发送到调试器时，没有用于将缓冲区合并为按时间排序的事件序列的机制。 因此，事件可能以不按顺序显示。 从 Windows 7 开始，当你使用 Tracelog 工具启动跟踪会话时，可以通过设置 **-lowcapacity** 参数来解决此问题。

**Tracelog** *MySession* **-kd-lowcapacity**

当你使用 **-lowcapacity** 设置启动会话时，所有事件将在目标计算机上转向单个缓冲区，事件在主计算机上的调试器中以正确的顺序显示。

此外，在使用此扩展之前，请使用 [**！ wmitrace; searchpath**](-wmitrace-searchpath.md) 或 [**！ wmitrace**](-wmitrace-tmffile.md) 来指定跟踪消息格式的文件。 系统使用跟踪消息格式文件设置二进制跟踪消息的格式，以便可以将它们显示为可读文本。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!wmitrace.start**](-wmitrace-start.md)

 

 






