---
title: 事件跟踪
description: 可以使用 Windows 的事件跟踪 (ETW) 或 Windows 软件跟踪预处理器 (WPP) 跟踪 HID over i2c 中的操作。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 688c366a076db892223db5d2017ccf213b552fd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828031"
---
# <a name="event-tracing"></a>事件跟踪


可以使用 Windows 的事件跟踪 (ETW) 或 Windows 软件跟踪预处理器 (WPP) 跟踪 HID over i2c 设备驱动程序中的操作。 有关 ETW 的详细信息，请参阅 Windows 开发参考中的 [事件跟踪](/windows/win32/etw/event-tracing-portal) 主题。 有关 WPP 的详细信息，请参阅 [Wpp Software](../devtest/wpp-software-tracing.md) [Trace 和即时 TRACE 录像机 (IFR) 用于日志记录跟踪](../devtest/using-wpp-recorder.md)。

## <a name="using-the-inflight-trace-recorder-ifr"></a>使用即时 Trace 录像机 (IFR) 


默认情况下，对于所有驱动程序都启用了即时 Trace 录像机 (IFR) ，可用于查看从 HIDI ²驱动程序到内核调试器的跟踪输出。 以下命令显示 HIDI ²的 WPP 跟踪消息。

``` syntax
!rcdrkd.rcdrlogdump hidi2c
```

即时 Trace 录像机 (IFR) 将这些跟踪消息存储为固定大小的循环缓冲区。 因此，输出可能不包含整个跟踪日志。

## <a name="using-logmanexe"></a>使用 logman.exe


若要获得更详细的可控制跟踪，可以使用 [logman.exe]( https://go.microsoft.com/fwlink/p/?linkid=256232) 来捕获跟踪。 以下命令将捕获 HIDI：

``` syntax
Logman create trace -n HIDI2C_WPP -o HIDI2C_WPP.etl -nb 128 640 -bs 128 
Logman update trace -n HIDI2C_WPP -p {E742C27D-29B1-4E4B-94EE-074D3AD72836} 0x7FFFFFFF 255
Logman start –n HIDI2C_WPP
 
<RUN your SCENARIO here>

Logman stop -n HIDI2C_WPP
Logman delete -n HIDI2C_WPP
```

您可以使用 HIDI ² C 的 PDB 或 TMF 文件将生成的跟踪日志文件分析为文本。

## <a name="enabling-etw-tracing"></a>启用 ETW 跟踪


HIDI ²驱动程序记录特定事件的 ETW 事件。 这些事件记录在事件查看器日志中。

你还可以使用以下 logman.exe 命令查看这些事件：

``` syntax
Logman create trace -n HIDI2C_ETW -o HIDI2C_ETW.etl -nb 128 640 -bs 128 
Logman update trace -n HIDI2C_ETW -p Microsoft-Windows-SPB-HIDI2C 
Logman start –n HIDI2C_ETW
 
<RUN your SCENARIO here>

Logman stop -n HIDI2C_ETW
Logman delete -n HIDI2C_ETW
```

生成的跟踪日志可以通过工具（如 **Xperf** 或 **Windows 性能分析器** (WPA) ）进行分析。

