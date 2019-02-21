---
title: 示例全局记录器提供程序
description: 示例全局记录器提供程序
ms.assetid: 06de4d6f-747c-4cf9-a325-2b697b72a1e9
keywords:
- 全局记录器跟踪会话 WDK，日志记录
- 启动时全局记录器跟踪会话 WDK，日志记录
- 启动过程中日志 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0da3421309af849261e51f07ac3f77c518ad13bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554110"
---
# <a name="example-global-logger-provider"></a>示例：全局记录器提供程序


下面的屏幕截图所示**GlobalLogger**子项，其中包含配置条目[全局记录器跟踪会话](global-logger-trace-session.md)。 下**GlobalLogger**子项**ControlGUID**表示记录到全局记录器跟踪会话的跟踪提供程序的子项。 **ControlGUID**子项已选中，然后在右窗格中显示子项中的项。

![记录到 windows xp 上的全局记录器跟踪会话的跟踪提供程序的子项的屏幕截图](images/globallogger.png)

在此示例中， **ControlGUID**子项表示 TraceDrv 示例驱动程序。 子项命名的 Tracedrv[控制 GUID](control-guid.md)，d58c126f-b309-11 d 1 969e 0000f875a5bc。 跟踪会话正在 Windows XP 上运行，因为 GUID 不括在大括号中。

[TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)示例驱动程序现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上提供的存储库。

这**ControlGUID**子项包含**标志**条目和一个**级别**条目。 这些条目是可选的其值由提供程序定义。

 

 





