---
title: wdfkd.wdftmffile
description: Wdftmffile 扩展将 ( tmf) 文件设置为在调试器为 wdfkd 或 wdflogdump 的错误日志设置格式时使用的跟踪消息格式。
keywords:
- wdfkd wdftmffile Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftmffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f882fd0b8d0f1c4acebb7417f33147e1b112bb04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785301"
---
# <a name="wdfkdwdftmffile"></a>!wdfkd.wdftmffile


当调试器 Kernel-Mode Driver Framework (KMDF) 错误日志记录 [**时，**](-wdfkd-wdflogdump.md) **wdftmffile** [**扩展将**](-wdfkd-wdfcrashdump.md) ( tmf) 文件设置为要使用的文件的跟踪消息格式。

```dbgcmd
!wdfkd.wdftmffile TMFpath
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______TMFpath______"></span><span id="_______tmfpath______"></span><span id="_______TMFPATH______"></span>*TMFpath*   
包含 tmf 文件的路径。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果驱动程序使用早于1.11 的 KMDF 版本，则必须先使用 **！ wdfkd** 扩展名，然后才能使用 [**！ wdfkd**](-wdfkd-wdflogdump.md) [**或 wdflogdump**](-wdfkd-wdfcrashdump.md) 扩展。

从 KMDF 版本1.11 开始，framework 库的符号文件 (例如 wdf01000) 包含跟踪消息格式 (TMF) 条目。 从内核调试器的 Windows 8 版本开始， [内核模式驱动程序框架扩展 ( # A0) ](kernel-mode-driver-framework-extensions--wdfkd-dll-.md) 读取 .pdb 文件中的条目。 因此，如果你的驱动程序使用 KMDF 版本1.11 或更高版本，并且你在 Windows 8 或更高版本中使用内核调试器，则不需要使用 **！ wdfkd. wdftmffile**。 你需要在调试器的 [符号路径](symbol-path.md)中包含包含符号文件的目录。 调试目标计算机可以运行任何支持 KMDF 的操作系统。

下面的示例演示如何在 KMDF 版本1.5 的 wdfkd 中使用 **wdftmffile** 扩展。

```dbgcmd
kd> !wdftmffile tools\tracing\<platform>\wdf1005.tmf
```

请注意，该路径可能不同于你正在使用的 Windows 驱动程序工具包)  (的 Windows 驱动程序工具包版本。 另请注意，tmf 文件的名称表示所使用的 KMDF 的版本。 例如，Wdf1005. tmf 是 KMDF 版本1.5 的 tmf 文件。

有关如何在调试会话期间查看 KMDF 日志的信息，请参阅 [使用框架的事件记录器](../wdf/using-the-framework-s-event-logger.md)。

 

