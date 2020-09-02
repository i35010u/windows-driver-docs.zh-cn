---
title: 启动时的全局记录器会话
description: 启动时的全局记录器会话
ms.assetid: f1f5bbee-48bd-4e4d-8849-9d21a4f85d44
keywords:
- 启动时间跟踪 WDK，全局记录器跟踪会话
- 全局记录器跟踪会话 WDK
- 启动时间全局记录器跟踪会话 WDK
- 全局记录器跟踪会话 WDK，关于全局记录器会话
- 启动时间全局记录器跟踪会话 WDK，关于全局记录器会话
- 在启动过程中跟踪 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d731d30437a39b2c0de3fb27d17ffa1f893ed4f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381473"
---
# <a name="boot-time-global-logger-session"></a>启动时的全局记录器会话


你可以创建一个全局记录器跟踪会话，用于在系统启动期间跟踪 Windows 内核事件。 此方法将跟踪内核的 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)的功能与 [全局记录器跟踪会话](global-logger-trace-session.md)的功能组合在一起，这将跟踪系统启动期间发生的事件。

本节中所述的过程将创建一个全局记录器跟踪会话，然后添加一个特殊的注册表项 **EnableKernelFlags**。 存在具有有效值的 **EnableKernelFlags** 项后，会将全局记录器跟踪会话转换为 NT 内核记录器跟踪会话。 **EnableKernelFlags**的有效值是从[**事件 \_ 跟踪 \_ 属性**](/windows/desktop/ETW/event-trace-properties)结构的**EnableFlags**成员的值中获取的。 [如何创建启动时全局记录器会话](how-to-create-a-boot-time-global-logger-session.md)中介绍了该过程。

跟踪提供程序（包括驱动程序）可以将跟踪消息记录到此类型的会话中。 [日志记录到全局记录器会话](logging-to-the-global-logger-session.md)中介绍了执行此操作的过程。

本节包括：

[如何创建启动时的全局记录器会话](how-to-create-a-boot-time-global-logger-session.md)

 

