---
title: wdfkd.wdflogdump
description: Wdfkd.wdflogdump 扩展显示 WDF 正在进行录制器日志记录，如果可用，KMDF 驱动程序或 UMDF 2 驱动程序。
ms.assetid: da03fafe-4cc8-4da6-9795-828e69e0df20
keywords:
- wdfkd.wdflogdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdflogdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbd8b3f6ac3bb3f83cc697bc8fb902a863670161
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362405"
---
# <a name="wdfkdwdflogdump"></a>!wdfkd.wdflogdump


**！ Wdfkd.wdflogdump**扩展显示 WDF 正在进行录制器日志记录，如果可用，KMDF 驱动程序或 UMDF 2 驱动程序。 你可以使用此命令与[完全内存转储](complete-memory-dump.md)即[内核内存转储](kernel-memory-dump.md)，或[实时内核模式目标](live-kernel-mode-targets.md)。

KMDF

```dbgcmd
!wdfkd.wdflogdump [DriverName][WdfDriverGlobals][-d | -f | -a LogAddress]
```

UMDF

```dbgcmd
!wdfkd.wdflogdump  [DriverName.dll][HostProcessId][-d | -f | -m]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
-   KMDF:KMDF 驱动程序的名称。 名称不得包含.sys 文件扩展名。
-   UMDF:UMDF 2 驱动程序的名称。 该名称必须包含.dll 文件扩展名。

<span id="_______Parameter2______"></span><span id="_______parameter2______"></span><span id="_______PARAMETER2______"></span> *Parameter2*   
-   KMDF:*WdfDriverGlobals* -地址*WdfDriverGlobals*结构。 您可以通过运行确定此地址[ **！ wdfkd.wdfldr** ](-wdfkd-wdfldr.md)和寻找标记为"WdfGlobals"的字段。 或者，可以提供 @@(Driver!WdfDriverGlobals) 作为地址值，其中*驱动程序*是驱动程序的名称。 如果有的话*WdfDriverGlobals*提供地址，则*DriverName* （尽管不过必须提供） 将被忽略。
-   UMDF:*HostProcessId* -wudfhost.exe 的实例的进程 ID。 如果提供的进程 ID，此命令将显示该进程的日志记录。 如果未提供的进程 ID，此命令将显示此窗体中的命令的列表：

    **!wdflogdump** *DriverName* **** *ProcessID*

    如果单个进程可将自动选择它来确定。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
KMDF:

**-d**显示仅的驱动程序日志。

**-f**显示仅的框架日志。

**-a** *LogAddress*显示特定驱动程序日志。 如果使用此选项，则必须提供 LogAddress。

UMDF:

**-d**显示仅的驱动程序日志。

**-f**显示仅的框架日志。

**-m**合并按照记录顺序的框架和驱动程序日志。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

<a name="remarks"></a>备注
-------

如果省略*DriverName*使用参数，默认驱动程序名称。 使用[ **！ wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)扩展来显示默认驱动程序名称，并使用[ **！ wdfkd.wdfsetdriver** ](-wdfkd-wdfsetdriver.md)扩展设置默认驱动程序名称。

若要显示来自框架的错误日志记录[很小的内存转储](small-memory-dump.md)，使用[ **！ wdfkd.wdfcrashdump** ](-wdfkd-wdfcrashdump.md)扩展。

有关设置调试器所需设置 WPP 跟踪消息的格式信息的信息，请参阅[ **！ wdfkd.wdftmffile** ](-wdfkd-wdftmffile.md)并[ **！ wdfkd.wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md).

**其他信息**

有关启用您的驱动程序的即时跟踪记录器的信息，请参阅[使用即时跟踪记录器 (IFR) KMDF 和 UMDF 2 驱动程序中](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers)。 有关调试 WDF 驱动程序的详细信息，请参阅[调试 WDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)。 有关 KMDF 调试信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[ **!wdfkd.wdfcrashdump**](-wdfkd-wdfcrashdump.md)

[ **!wdfkd.wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md)

 

 






