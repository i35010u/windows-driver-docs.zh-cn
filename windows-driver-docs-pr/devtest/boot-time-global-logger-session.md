---
title: 启动时全局记录器会话
description: 启动时全局记录器会话
ms.assetid: f1f5bbee-48bd-4e4d-8849-9d21a4f85d44
keywords:
- 启动时跟踪 WDK 时，全局记录器跟踪会话
- 全局记录器跟踪会话 WDK
- 启动时全局记录器跟踪会话 WDK
- 有关全局记录器会话全局记录器跟踪会话 WDK，
- 有关全局记录器会话的启动时间全局记录器跟踪会话 WDK，
- 在启动期间跟踪 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3843a428892e609e64c758f4d9d2d88785c0586
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540853"
---
# <a name="boot-time-global-logger-session"></a>启动时全局记录器会话


可以创建在系统启动期间跟踪 Windows 内核事件的全局记录器跟踪会话。 此方法的功能整合[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，其中跟踪了内核，与[全局记录器跟踪会话](global-logger-trace-session.md)，其中跟踪了在系统启动期间发生的事件。

在本部分中所述的过程创建全局记录器跟踪会话，并将特殊的注册表条目，然后添加**EnableKernelFlags**。 是否存在**EnableKernelFlags**条目，请使用有效的值，将转换为全局记录器跟踪会话 NT 内核记录器跟踪会话。 有效值**EnableKernelFlags**的值取自**EnableFlags**的成员[**事件\_跟踪\_属性** ](https://msdn.microsoft.com/library/windows/desktop/aa363784)结构。 中介绍的过程[如何创建启动时全局记录器会话](how-to-create-a-boot-time-global-logger-session.md)。

跟踪提供程序，包括驱动程序，可以将跟踪消息记录到此类型的会话。 因此，执行此操作的过程是中所述[记录到全局记录器会话](logging-to-the-global-logger-session.md)。

本部分包括：

[如何创建启动时全局记录器会话](how-to-create-a-boot-time-global-logger-session.md)

 

 





