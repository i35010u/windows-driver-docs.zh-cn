---
title: 在启动期间跟踪
description: 在启动期间跟踪
ms.assetid: 79594c33-5755-4484-aaf5-ac409b05ddcc
keywords:
- 在启动过程中进行软件跟踪 WDK
- 在启动过程中跟踪 WDK
- 启动时跟踪 WDK
- 内核模式软件跟踪 WDK
- 启动时间跟踪 WDK，关于引导时跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c19c8d78a14fab707314827b84dae96937304e0f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381629"
---
# <a name="tracing-during-boot"></a>在启动期间跟踪


在 Windows 启动过程中，您可以使用 Microsoft Windows 中的软件跟踪组件的功能来跟踪 Windows 内核的活动，以及驱动程序和其他跟踪提供程序的活动。

本部分不介绍新的工具。 相反，它描述使用现有软件跟踪工具和 Windows (ETW) 功能的事件跟踪来执行此重要任务的方法。

本部分介绍了在启动过程中的以下跟踪方法：

-   [启动时的全局记录器会话](boot-time-global-logger-session.md)

    在启动过程中通过将 [全局记录器跟踪会话](global-logger-trace-session.md) 转换为 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)来跟踪 Windows 内核活动。

-   [记录到全局记录器会话](logging-to-the-global-logger-session.md)

    在启动过程中跟踪驱动程序或其他跟踪提供程序的活动。 必须检测提供程序以进行跟踪。 一次只能运行一个全局记录器会话。 此功能在 windows 2000 和更高版本的 Windows 中可用。

-   **自动**

    这是在启动过程中跟踪驱动程序或其他跟踪提供程序的活动的首选方法。 必须检测提供程序以进行跟踪。 自动记录器向驱动程序提供回调通知。 多个 AutoLoggers 可以并发运行。 此功能在 Windows Vista 和更高版本的 Windows 中可用。 有关使用自动记录器跟踪驱动程序的活动的信息，请参阅 [配置和启动自动记录器会话](/windows/win32/etw/configuring-and-starting-an-autologger-session)。

使用全局记录器跟踪会话时，请确保你了解其限制。 有关信息，请参阅全局记录器跟踪会话的限制。

 

