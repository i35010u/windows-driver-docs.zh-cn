---
title: 用于软件跟踪的工具
description: WDK 包含的工具旨在支持 Windows (ETW) 的事件跟踪，并补充了 Windows 中包含的跟踪工具。
keywords:
- 工具 WDK，软件跟踪
- 驱动程序开发工具 WDK、软件跟踪
- 软件跟踪 WDK
- 跟踪 WDK
- 跟踪 WDK，关于软件跟踪
- 事件跟踪 WDK
- 跟踪工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a7576dc8b152b5df090ef8d49f1e58c43dbf06c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805647"
---
# <a name="tools-for-software-tracing"></a>用于软件跟踪的工具


Microsoft Windows 驱动程序工具包 (WDK) 包含一组用于软件跟踪的应用程序和命令行工具。 这些工具旨在支持 Windows (ETW) 的事件跟踪，并补充 Windows 中包含的跟踪工具。

- [跟踪工具是什么？](#what-are-the-tracing-tools)
- [何时应使用 WPP 软件跟踪或 Windows (ETW) API 的事件跟踪？](#when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api)
- [本节内容](#whats-in-this-section)

## <a name="what-are-the-tracing-tools"></a>跟踪工具是什么？

这些工具包括用于配置、启动、更新和停止跟踪会话的 [跟踪控制器](trace-controller.md) ，以及跟踪在会话过程中生成的跟踪消息的 [使用者](trace-consumer.md) ，以及将二进制数据转换为可读格式的文件或显示。

这些工具支持各种 [跟踪提供](trace-provider.md)程序，包括用户模式应用程序和内核模式驱动程序，这些提供程序通过使用 [WPP 软件跟踪](wpp-software-tracing.md) 或 ([Windows (ETW) 的事件跟踪 ](event-tracing-for-windows--etw-.md)来检测软件跟踪。 有关检测代码的两种方法的比较，请参阅 [何时使用 WPP 软件跟踪和 Windows (ETW 的事件跟踪) ](#when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api)。

这些工具还可以访问 Windows 中内置的保留[跟踪会话](trace-session.md)，例如[全局记录器跟踪会话](global-logger-trace-session.md)  /  [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

其中的某些工具位于 \\ &lt; *Platform* &gt; Windows 驱动程序工具包 (WDK) 的工具平台子目录中，其中 &lt; *平台* &gt; 为 x86 或 x64。 其他工具包括在 Windows 中，或者位于 WDK 的 bin \\ &lt; *平台* &gt; 子目录中。

## <a name="when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api"></a>何时应使用 WPP 软件跟踪或 Windows (ETW) API 的事件跟踪？

如果你有兴趣主要收集用于开发和调试目的的跟踪数据，请使用 [WPP 软件跟踪](wpp-software-tracing.md) 。 对于其他类型的跟踪，请使用 [Windows 事件跟踪 (ETW) ](event-tracing-for-windows--etw-.md) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 软件跟踪</th>
<th align="left">列入清单/TraceLogging ETW</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">在 Windows 2000 和更高版本上受支持。</td>
<td align="left">在 Windows Vista 和更高版本上受支持。</td>
</tr>
<tr class="even">
<td align="left">跟踪用于开发和调试的事件。 主要面向内部开发人员。</td>
<td align="left">跟踪事件以实现管理、操作、分析和调试目的。</td>
</tr>
<tr class="even">
<td align="left">需要 TMF 文件来解码事件，这些事件是从日志记录二进制 PDB 中提取的。</td>
<td align="left">用于对事件进行解码的元数据包含在本地二进制文件或事件负载中。</td>
</tr>
<tr class="odd">
<td align="left">对于每个跟踪提供程序，只能有一个活动会话。</td>
<td align="left">事件可复用到多个使用者。</td>
</tr>
<tr class="even">
<td align="left">消息字符串不能本地化。</td>
<td align="left">字符串可本地化。</td>
</tr>
<tr class="odd">
<td align="left">提供程序安全限制为不共享启用和解码事件所需的控件 GUID 或 TMF 文件。</td>
<td align="left">提供程序可以应用 Acl 来限制可以从中收集事件的用户。</td>
</tr>
</tbody>
</table> 

有关使用 Windows 软件跟踪预处理器 (WPP) 宏将软件跟踪添加到驱动程序或应用程序的信息，请参阅 [WPP 软件跟踪](wpp-software-tracing.md)。

有关对驱动程序使用内核模式 ETW API 的信息，请参阅 [Windows 事件跟踪 (ETW) ](event-tracing-for-windows--etw-.md)。

有关使用 Windows Management Instrumentation (WMI) 扩展添加到 Windows 驱动模型 (WDM) 以将软件跟踪添加到任何驱动程序的信息，请参阅 [Wmi 事件跟踪](../kernel/wmi-event-tracing.md)。

**注意**   ETW 和 WPP 支持大多数类型的内核模式驱动程序和用户模式应用程序。 但 ETW 和 WPP 使用某些类型的驱动程序（如微型端口驱动程序）不可用的类型。 若要确定是否支持某个特定的驱动程序类型，请将基本的 WPP 宏添加到该驱动程序，如 [WPP \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 和 [wpp \_ 清除](/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))。 如果代码由于未定义所使用的类型而不编译，则 ETW 和 WPP 不能支持驱动程序类型。 

## <a name="whats-in-this-section"></a>本节内容

本部分从软件跟踪工具的调查开始，讨论工具的基础概念，然后在 WDK 中包括软件跟踪工具的文档。

本节包括：

[软件跟踪工具调查](survey-of-software-tracing-tools.md)

[跟踪工具的概念](tracing-tool-concepts.md)

[TraceView](traceview.md)

[Tracelog](tracelog.md)

[Tracepdb](tracepdb.md)

[Tracefmt](tracefmt.md)

[在启动期间跟踪](tracing-during-boot.md)

[WPP 软件跟踪](wpp-software-tracing.md)

[软件跟踪常见问题解答](software-tracing-faq.md)

[Windows 事件跟踪 (ETW)](event-tracing-for-windows--etw-.md)

[内核模式性能监视](kernel-mode-performance-monitoring.md)

有关 [事件跟踪](/windows/desktop/ETW/about-event-tracing)的概念信息，请参阅 Microsoft Windows SDK 文档。 
