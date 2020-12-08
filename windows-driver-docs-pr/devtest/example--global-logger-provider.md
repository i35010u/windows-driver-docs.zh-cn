---
title: 全局记录器提供程序示例
description: 全局记录器提供程序示例
keywords:
- 全局记录器跟踪会话 WDK，日志记录
- 启动时全局记录器跟踪会话 WDK，日志记录
- 在启动过程中记录 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95880f38e8b15fb422346751b797edf8031a6ac6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784045"
---
# <a name="example-global-logger-provider"></a>例如：全局记录器提供程序


以下屏幕截图显示了 **GlobalLogger** 子项，其中包含配置 [全局记录器跟踪会话](global-logger-trace-session.md)的条目。 **GlobalLogger** 子项下是一个 **ControlGUID** 子项，表示日志记录到全局记录器跟踪会话的跟踪提供程序。 **ControlGUID** 子项已选中，并且子项中的条目显示在右窗格中。

![在 windows xp 上记录到全局记录器跟踪会话的跟踪提供程序子项的屏幕截图](images/globallogger.png)

在此示例中， **ControlGUID** 子项表示 TraceDrv 示例驱动程序。 为 Tracedrv [控件 GUID](control-guid.md)d58c126f-b309-11d1-969e-0000f875a5bc 指定子项。 由于跟踪会话正在 Windows XP 上运行，因此 GUID 不会括在大括号中。

[TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)示例驱动程序在 GitHub 上提供的[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)存储库中提供。

此 **ControlGUID** 子项包含 **标志** 条目和 **级别** 条目。 这些条目是可选的，其值由提供程序定义。

 

 





