---
title: 有关驱动程序的事件跟踪
description: 有关驱动程序的事件跟踪
ms.assetid: 1b5c85b1-5b7a-48bc-bdd4-356316d4467f
keywords:
- Windows WDK，有关 Windows 事件跟踪的事件跟踪
- ETW WDK，有关 Windows 事件跟踪
- 事件跟踪的 Windows WDK，内核模式
- ETW WDK 内核模式
- 内核模式 ETW WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23fee31ba48a8afb8f50a267438e5524e9b70faf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547357"
---
# <a name="about-event-tracing-for-drivers"></a>有关驱动程序的事件跟踪


## <a name="what-is-event-tracing"></a>什么是事件跟踪？

Windows 事件跟踪 (ETW) 是一种有效和高效的机制，用于跟踪和日志记录由用户模式应用程序和内核模式驱动程序引发的事件。 ETW 包括三个组件：

<table>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>提供程序</p></td>
<td align="left"><p>应用程序或引发事件跟踪检测的组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>控制器</p></td>
<td align="left"><p>启动、 停止和配置事件跟踪会话的应用程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>使用者</p></td>
<td align="left"><p>接收事件跟踪会话 （在真实时间） 的应用程序或文件。</p></td>
</tr>
</tbody>
</table>

 

## <a name="the-etw-kernel-mode-api"></a>ETW 内核模式 API

ETW 应用程序编程接口 (API) 提供了一组适用于内核模式组件和驱动程序的函数。 [WMI 事件跟踪](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)并[WPP 软件跟踪](wpp-software-tracing.md)都使用 ETW。 驱动程序开发人员可以使用这些函数的 ETW 提供程序作为注册驱动程序。 ETW 提供程序可以引发事件并将其发布到 Windows 事件日志或可以将其事件写入 ETW 会话，用于获取写入到跟踪文件或传递到实时的使用者。 事件是用于描述系统中有趣的匹配项，并由一组由 ETW 提供程序的属性定义的实体。

ETW 在 Windows 操作系统中实现，并为开发人员快速、 可靠且用途广泛的一组事件跟踪功能提供对性能的影响非常小。 您可以动态启用或禁用跟踪而无需重新启动计算机，或重新加载应用程序或驱动程序。 与不同的调试在开发期间添加到你的代码的语句，可以在生产代码中使用 ETW。

## <a name="when-to-use-event-tracing"></a>何时使用事件跟踪

如果你想要发布的应用程序感兴趣管理、 操作和分析事件，除了详细的跟踪可能需要在开发过程中可以使用事件，请使用 ETW 内核模式 API。 如果您有兴趣主要收集跟踪数据，用于开发和调试目的，请使用 WPP 软件跟踪。

 

 





