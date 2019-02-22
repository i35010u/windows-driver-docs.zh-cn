---
title: 在启动期间跟踪
description: 在启动期间跟踪
ms.assetid: 79594c33-5755-4484-aaf5-ac409b05ddcc
keywords:
- 在启动期间跟踪 WDK，软件
- 在启动期间跟踪 WDK，
- 启动时跟踪 WDK
- 内核模式软件跟踪 WDK
- 有关启动时间跟踪的启动时间跟踪 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9997e3cf374f3f79b81525e550c7243f5bea42d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541721"
---
# <a name="tracing-during-boot"></a>在启动期间跟踪


可以使用在 Microsoft Windows 软件跟踪组件的功能以在 Windows 启动过程中将跟踪活动的 Windows 内核和驱动程序和其他跟踪提供程序的活动。

本部分不会介绍新的工具。 相反，它描述了使用现有软件跟踪工具和 Windows 事件跟踪 (ETW) 功能来执行此任务中有价值的方法。

本部分介绍了启动过程中跟踪以下方法：

-   [启动时全局记录器会话](boot-time-global-logger-session.md)

    通过转换启动过程中跟踪 Windows 内核活动[全局记录器跟踪会话](global-logger-trace-session.md)到[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

-   [到全局记录器会话日志记录](logging-to-the-global-logger-session.md)

    在启动期间跟踪驱动程序或其他跟踪提供程序的活动。 提供程序必须进行检测的跟踪。 只有一个全局记录器会话可以运行一次。 此功能是在 Windows 2000 和更高版本的 Windows 中可用。

-   **AutoLogger**

    这是用于在启动期间跟踪驱动程序或其他跟踪提供程序的活动的首选的方法。 提供程序必须进行检测的跟踪。 记录器提供给驱动程序的回调通知。 可以同时运行多个 AutoLoggers。 此功能是在 Windows Vista 和更高版本的 Windows 中可用。 有关跟踪的活动的驱动程序有自动记录器的信息，请参阅[配置和启动自动记录器会话](https://go.microsoft.com/fwlink/p/?linkid=89723)。

时使用的全局记录器跟踪会话，请确保您已了解其限制。 有关信息，请参阅全局记录器跟踪会话的限制。

 

 





