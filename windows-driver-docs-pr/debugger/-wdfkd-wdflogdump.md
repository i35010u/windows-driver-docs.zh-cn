---
title: wdfkd.wdflogdump
description: Wdfkd. wdflogdump 扩展显示 KMDF 驱动程序或 UMDF 2 驱动程序的项中的网络内记录器日志记录（如果有）。
keywords:
- wdfkd wdflogdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdflogdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2221781a3691f20fb877df62c4d4795921b26413
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833723"
---
# <a name="wdfkdwdflogdump"></a>!wdfkd.wdflogdump


**！ Wdfkd wdflogdump** 扩展显示 KMDF 驱动程序或 UMDF 2 驱动程序的项中的 "网络中" 记录记录器日志记录（如果有）。 可以将此命令与 [完整内存转储](complete-memory-dump.md)、 [内核内存转储](kernel-memory-dump.md)或 [实时内核模式目标](live-kernel-mode-targets.md)结合使用。

KMDF

```dbgcmd
!wdfkd.wdflogdump [DriverName][WdfDriverGlobals][-d | -f | -a LogAddress]
```

UMDF

```dbgcmd
!wdfkd.wdflogdump  [DriverName.dll][HostProcessId][-d | -f | -m]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
-   KMDF： KMDF 驱动程序的名称。 名称不能包含 .sys 文件扩展名。
-   UMDF： UMDF 2 驱动程序的名称。 名称必须包含 .dll 文件扩展名。

<span id="_______Parameter2______"></span><span id="_______parameter2______"></span><span id="_______PARAMETER2______"></span>*Parameter2*   
-   KMDF： *WdfDriverGlobals* - *WdfDriverGlobals* 结构的地址。 可以通过运行 [**！ wdfkd**](-wdfkd-wdfldr.md) 并查找标签为 "WdfGlobals" 的字段来确定此地址。 或者，你可以提供 @ @ (Driver！WdfDriverGlobals) 作为 address 值，其中 *driver* 是驱动程序的名称。 如果提供了任何 *WdfDriverGlobals* 地址，则将忽略 *DriverName* (但仍必须) 提供。
-   UMDF： *HostProcessId* -wudfhost.exe 实例的进程 ID。 如果提供进程 ID，此命令将显示该进程的日志记录。 如果未提供进程 ID，则此命令将显示此窗体中的命令列表：

    **！ wdflogdump** *DriverName*  ****  *ProcessID*

    如果可以确定单个进程，则会自动选择它。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
KMDF

**-d** 仅显示驱动程序日志。

**-f** 只显示框架日志。

**-** *LogAddress* 显示特定的驱动程序日志。 如果使用此选项，则必须提供 LogAddress。

UMDF

**-d** 仅显示驱动程序日志。

**-f** 只显示框架日志。

**-m** 将框架和驱动程序日志合并为其记录的顺序。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

<a name="remarks"></a>备注
-------

如果省略 *DriverName* 参数，则使用默认的驱动程序名称。 使用 [**！ wdfkd wdfgetdriver**](-wdfkd-wdfgetdriver.md) 扩展显示默认的驱动程序名称，并使用 [**！ wdfkd**](-wdfkd-wdfsetdriver.md) 扩展名设置默认驱动程序名称。

若要显示 [小型内存转储](small-memory-dump.md)中框架的错误日志记录，请使用 [**！ wdfkd**](-wdfkd-wdfcrashdump.md) 扩展名。

有关调试器需要设置 WPP 跟踪消息格式的信息，请参阅 [**！ wdfkd. wdftmffile**](-wdfkd-wdftmffile.md) and [**！ wdfkd. wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md)。

**其他信息**

有关为驱动程序启用即时跟踪记录器的信息，请参阅 [使用即时 Trace 录像机 (IFR) 在 KMDF 和 UMDF 2 驱动程序中](../wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)。 有关调试 WDF 驱动程序的详细信息，请参阅 [调试 Wdf 驱动程序](./debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。 有关 KMDF 调试的信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!wdfkd.wdfcrashdump**](-wdfkd-wdfcrashdump.md)

[**!wdfkd.wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md)

