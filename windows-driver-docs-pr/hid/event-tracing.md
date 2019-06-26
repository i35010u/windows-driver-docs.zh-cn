---
title: 事件跟踪
description: 您可以使用事件跟踪 Windows (ETW) 或 Windows 软件跟踪预处理器 (WPP) 若要通过 I²C 你 HID 中跟踪操作。
ms.assetid: F23E5516-36B9-478E-90D3-54D1C52CB467
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc5df2a5de31ff882eb0b3bf32fd68cfd5f884de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375730"
---
# <a name="event-tracing"></a>事件跟踪


您可以使用事件跟踪 Windows (ETW) 或 Windows 软件跟踪预处理器 (WPP) 若要通过 I²C 设备驱动程序在你 HID 跟踪操作。 有关 ETW 的详细信息，请参阅[事件跟踪](https://go.microsoft.com/fwlink/p/?linkid=256040)Windows 开发参考中的主题。 有关 WPP 详细信息，请参阅[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)并[即时跟踪记录器 (IFR) 的日志中记录跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)。

## <a name="using-the-inflight-trace-recorder-ifr"></a>使用即时跟踪记录器 (IFR)


即时跟踪记录器 (IFR)，启用所有驱动程序的默认情况下，可以查看跟踪输出从 HIDI²C 驱动程序发送到内核调试程序。 下面的命令显示有关 HIDI²C WPP 跟踪消息。

``` syntax
!rcdrkd.rcdrlogdump hidi2c
```

即时跟踪记录器 (IFR) 的固定大小循环缓冲区中存储这些跟踪消息。 因此，输出可能不包含整个跟踪日志。

## <a name="using-logmanexe"></a>使用 logman.exe


有关更详细，而且可控制跟踪，可以使用[logman.exe]( https://go.microsoft.com/fwlink/p/?linkid=256232)捕获跟踪。 以下命令为 HIDI²C 捕获 WPP 跟踪：

``` syntax
Logman create trace -n HIDI2C_WPP -o HIDI2C_WPP.etl -nb 128 640 -bs 128 
Logman update trace -n HIDI2C_WPP -p {E742C27D-29B1-4E4B-94EE-074D3AD72836} 0x7FFFFFFF 255
Logman start –n HIDI2C_WPP
 
<RUN your SCENARIO here>

Logman stop -n HIDI2C_WPP
Logman delete -n HIDI2C_WPP
```

可以将生成的跟踪日志文件分析为 HIDI²C 使用 PDB 或 TMF 文件的文本。

## <a name="enabling-etw-tracing"></a>启用 ETW 跟踪


HIDI²C 驱动程序记录特定事件的 ETW 事件。 这些事件会记录在事件查看器日志中。

你还可以查看这些事件使用以下 logman.exe 命令：

``` syntax
Logman create trace -n HIDI2C_ETW -o HIDI2C_ETW.etl -nb 128 640 -bs 128 
Logman update trace -n HIDI2C_ETW -p Microsoft-Windows-SPB-HIDI2C 
Logman start –n HIDI2C_ETW
 
<RUN your SCENARIO here>

Logman stop -n HIDI2C_ETW
Logman delete -n HIDI2C_ETW
```

使用等工具可分析生成的跟踪日志**Xperf**或**Windows Performance Analyzer** (WPA)。

 

 




