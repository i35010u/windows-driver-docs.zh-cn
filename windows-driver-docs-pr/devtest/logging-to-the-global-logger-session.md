---
title: 到全局记录器会话日志记录
description: 到全局记录器会话日志记录
ms.assetid: 48dfe101-b083-4d70-b85f-2e115f7e1dfa
keywords:
- 在启动 WDK 期间跟踪，全局记录器跟踪会话
- 启动时跟踪 WDK 时，全局记录器跟踪会话
- 全局记录器跟踪会话 WDK，日志记录
- 启动时全局记录器跟踪会话 WDK，日志记录
- 启动过程中日志 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b9c5e05575b85cc4502697a4423e98cf51f092d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555862"
---
# <a name="logging-to-the-global-logger-session"></a>到全局记录器会话日志记录


你可以在系统启动期间由配置驱动程序以记录到跟踪驱动程序或其他跟踪提供程序的操作[全局记录器跟踪会话](global-logger-trace-session.md)，在系统启动期间运行的跟踪会话。 该驱动程序必须进行检测的软件跟踪。

尽管全局记录器跟踪会话不会发送使提供程序的通知，在本部分中所述的方法将代码添加到允许确定进行全局记录器会话的跟踪启用时，驱动程序的驱动程序。

在 Windows 2000 和更高版本的 Windows 支持此方法。 但是，在 Windows Vista 和更高版本的 Windows 中，启动跟踪的首选的方法是使用自动记录器专门设计用于启动的跟踪的新功能。 有关跟踪的活动的驱动程序有自动记录器的信息，请参阅[配置和启动自动记录器会话](https://go.microsoft.com/fwlink/p/?linkid=89723)。

本部分包括：

[如何登录到全局记录器会话](how-to-log-to-the-global-logger-session.md)

[示例：全局记录器提供程序](example--global-logger-provider.md)

 

 





