---
title: 调试 Windows 驱动程序
ms.assetid: d2d168fe-8be2-4a3d-bc29-4ab3a306296e
description: 介绍了可用于 Windows 驱动程序的调试技术，特别是 Inflight Trace Recorder。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: e2d64d3c159659a5ddde611070192f5f23694704
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065194"
---
# <a name="debugging-a-windows-driver"></a>调试 Windows 驱动程序 

有关调试驱动程序的一般信息，请参阅 [Windows 调试入门](../debugger/getting-started-with-windows-debugging.md)。

## <a name="inflight-trace-recorder"></a>即时跟踪记录器

从 Windows 10 开始，可以生成 KMDF 或 UMDF 驱动程序二进制文件，这样它可以通过[即时跟踪记录器](../devtest/using-wpp-recorder.md)获取其他驱动程序调试信息。 Windows 驱动程序可以利用此功能。

此外，如果你使用了 Visual Studio KMDF 模板，驱动程序将使用 Windows 软件跟踪预处理器 (WPP) 写入跟踪消息。 驱动程序二进制文件是具有提供程序 GUID 的 ETW 提供程序。

若要从驱动程序二进制文件发送跟踪消息，请使用以下代码：

   ```cpp
   TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");
   ```

可以通过使用调试程序会话中的 [!wmitrace](../debugger/wmi-tracing-extensions--wmitrace-dll-.md) 来利用 Tracelog 访问 ETW 日志。