---
title: 关于驱动程序的事件跟踪
description: 关于驱动程序的事件跟踪
keywords:
- Windows WDK 事件跟踪，关于 Windows 的事件跟踪
- ETW WDK，关于 Windows 的事件跟踪
- Windows WDK 事件跟踪，内核模式
- ETW WDK，内核模式
- 内核模式 ETW WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4197de9ec46c1f0a1bc4bf705db8c38bc06335d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795153"
---
# <a name="about-event-tracing-for-drivers"></a>关于驱动程序的事件跟踪

## <a name="event-tracing-defined"></a>已定义事件跟踪

Windows (ETW) 的事件跟踪是一种高效而有效的机制，用于跟踪和记录用户模式应用程序和内核模式驱动程序引发的事件。 ETW 包含三个组件：

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
<td align="left"><p>引发事件跟踪检测的应用程序或组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Controllers</p></td>
<td align="left"><p>启动、停止和配置事件跟踪会话的应用程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>使用者</p></td>
<td align="left"><p>接收事件跟踪会话的应用程序将实时 () 或文件。</p></td>
</tr>
</tbody>
</table>

## <a name="the-etw-kernel-mode-api"></a>ETW Kernel-Mode API

ETW 应用程序编程接口 (API) 提供一组可用于内核模式组件和驱动程序的函数。 [WMI 事件跟踪](../kernel/wmi-event-tracing.md) 和 [WPP 软件跟踪](wpp-software-tracing.md) 均使用 ETW。 驱动程序开发人员可以使用这些函数将驱动程序注册为 ETW 提供程序。 ETW 提供程序可以引发事件，并可以将其发布到 Windows 事件日志，也可以将其事件写入 ETW 会话，后者会写入跟踪文件或传递给实时使用者。 事件是描述系统中感兴趣的事件的实体，由 ETW 提供程序确定的一组属性进行定义。

ETW 是在 Windows 操作系统中实现的，它为开发人员提供了一组快速、可靠且丰富的事件跟踪功能，对性能的影响非常小。 你可以在不重新启动计算机或重新加载应用程序或驱动程序的情况下动态启用或禁用跟踪。 与在开发过程中添加到代码中的调试语句不同，您可以在生产代码中使用 ETW。

## <a name="when-to-use-event-tracing"></a>何时使用事件跟踪

如果希望发布可由对管理、操作和分析事件感兴趣的应用程序使用的事件，以及在开发过程中可能需要的详细跟踪，请使用 ETW 内核模式 API。 如果你有兴趣主要收集用于开发和调试目的的跟踪数据，请使用 WPP 软件跟踪。
