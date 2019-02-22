---
title: wdfkd.wdftmffile
description: Wdfkd.wdftmffile 扩展设置调试器格式为 wdfkd.wdflogdump 或 wdfkd.wdfcrashdump KMDF 错误日志时要使用的跟踪消息格式 (.tmf) 文件。
ms.assetid: 7099440c-bfea-472f-b9ee-943026afdb81
keywords:
- wdfkd.wdftmffile Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftmffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 700bbd5720637a79d596cbdd8c44e2bb364b27e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520192"
---
# <a name="wdfkdwdftmffile"></a>!wdfkd.wdftmffile


**！ Wdfkd.wdftmffile**扩展插件设置调试器格式化的内核模式驱动程序框架 (KMDF) 错误日志记录时使用的跟踪消息格式 (.tmf) 文件[ **！ wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md)或[ **！ wdfkd.wdfcrashdump** ](-wdfkd-wdfcrashdump.md)扩展。

```dbgcmd
!wdfkd.wdftmffile TMFpath
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______TMFpath______"></span><span id="_______tmfpath______"></span><span id="_______TMFPATH______"></span> *TMFpath*   
包含.tmf 文件的路径。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果您的驱动程序使用早于 1.11 KMDF 版本，则必须使用 **！ wdfkd.wdftmffile**扩展可以使用之前[ **！ wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md)或[**！ wdfkd.wdfcrashdump** ](-wdfkd-wdfcrashdump.md)扩展。

框架库的符号文件 (例如 wdf01000.pdb) 从 KMDF 1.11 版开始，包含跟踪消息格式 (TMF) 条目。 在 Windows 8 版本的内核调试程序，启动[内核模式驱动程序框架扩展 (Wdfkd.dll)](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)从.pdb 文件中读取的项。 因此，如果您的驱动程序使用 KMDF 版本 1.11 或更高版本，并且使用内核调试程序从 Windows 8 或更高版本，您不需要使用 **！ wdfkd.wdftmffile**。 需要包括包含在调试器中的符号文件的目录[符号路径](symbol-path.md)。 调试目标计算机可以运行任何操作系统支持 KMDF。

下面的示例演示如何使用 **！ wdfkd.wdftmffile** WDK 根目录中，对于 KMDF 1.5 版的扩展。

```dbgcmd
kd> !wdftmffile tools\tracing\<platform>\wdf1005.tmf
```

请注意，其路径可能为不同的使用 Windows Driver Kit (WDK) 的版本。 此外请注意.tmf 文件的名称，表示使用 KMDF 的版本。 例如，Wdf1005.tmf 是 KMDF 版本 1.5 的.tmf 文件。

有关如何在调试会话期间查看 KMDF 日志的信息，请参阅[使用框架的事件记录器](https://msdn.microsoft.com/library/windows/hardware/ff545531)。

 

 





