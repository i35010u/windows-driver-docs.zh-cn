---
title: 启动时的全局记录器会话
description: 启动时的全局记录器会话
keywords:
- 启动时间跟踪 WDK，全局记录器跟踪会话
- 全局记录器跟踪会话 WDK
- 启动时间全局记录器跟踪会话 WDK
- 全局记录器跟踪会话 WDK，关于全局记录器会话
- 启动时间全局记录器跟踪会话 WDK，关于全局记录器会话
- 在启动过程中跟踪 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e5414b04071feb0926ec9bfb9ae0ddadd33e181
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791595"
---
# <a name="boot-time-global-logger-session"></a>启动时的全局记录器会话


你可以创建一个全局记录器跟踪会话，用于在系统启动期间跟踪 Windows 内核事件。 此方法将跟踪内核的 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)的功能与 [全局记录器跟踪会话](global-logger-trace-session.md)的功能组合在一起，这将跟踪系统启动期间发生的事件。

本节中所述的过程将创建一个全局记录器跟踪会话，然后添加一个特殊的注册表项 **EnableKernelFlags**。 存在具有有效值的 **EnableKernelFlags** 项后，会将全局记录器跟踪会话转换为 NT 内核记录器跟踪会话。 **EnableKernelFlags** 的有效值是从 [**事件 \_ 跟踪 \_ 属性**](/windows/desktop/ETW/event-trace-properties)结构的 **EnableFlags** 成员的值中获取的。 [如何创建 Boot-Time 全局记录器会话](how-to-create-a-boot-time-global-logger-session.md)中介绍了该过程。

跟踪提供程序（包括驱动程序）可以将跟踪消息记录到此类型的会话中。 [日志记录到全局记录器会话](logging-to-the-global-logger-session.md)中介绍了执行此操作的过程。

本节包括：

[如何创建启动时的全局记录器会话](how-to-create-a-boot-time-global-logger-session.md)

 

