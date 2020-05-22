---
title: 记录到全局记录器会话
description: 记录到全局记录器会话
ms.assetid: 48dfe101-b083-4d70-b85f-2e115f7e1dfa
keywords:
- 在启动 WDK 期间进行跟踪，全局记录器跟踪会话
- 启动时间跟踪 WDK，全局记录器跟踪会话
- 全局记录器跟踪会话 WDK，日志记录
- 启动时全局记录器跟踪会话 WDK，日志记录
- 在启动过程中记录 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfc2d5eb9506e2c3ce21775f917837a295f9b939
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769635"
---
# <a name="logging-to-the-global-logger-session"></a>记录到全局记录器会话


您可以通过将驱动程序配置为记录到[全局记录器跟踪会话](global-logger-trace-session.md)（在系统启动期间运行的跟踪会话），在系统启动期间跟踪驱动程序或其他跟踪提供程序的操作。 必须检测驱动程序的软件跟踪。

尽管全局记录器跟踪会话不会将启用通知发送到提供程序，但本部分中所述的方法会将代码添加到驱动程序中，以便驱动程序可以确定何时为全局记录器会话启用跟踪。

Windows 2000 和更高版本的 Windows 支持此方法。 但是，在 Windows Vista 和更高版本的 Windows 中，引导跟踪的首选方法是将自动记录器用于专用于启动跟踪的新功能。 有关使用自动记录器跟踪驱动程序的活动的信息，请参阅[配置和启动自动记录器会话](https://docs.microsoft.com/windows/win32/etw/configuring-and-starting-an-autologger-session)。

本节包括：

[如何记录到全局记录器会话](how-to-log-to-the-global-logger-session.md)

[示例：全局记录器提供程序](example--global-logger-provider.md)

 

 





