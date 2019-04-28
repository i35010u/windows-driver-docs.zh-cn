---
title: 用于软件跟踪的工具
description: WDK 包含旨在支持 Windows 事件跟踪 (ETW) 并补充在 Windows 中包含的跟踪工具的工具。
ms.assetid: 31056b02-378f-4756-b5a0-3d4cbbc6d3da
keywords:
- 工具 WDK，软件跟踪
- 驱动程序开发工具 WDK，软件跟踪
- 跟踪 WDK 的软件
- 跟踪 WDK
- 跟踪软件跟踪有关 WDK，
- 事件跟踪 WDK
- 跟踪工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ea87821206a6aba081bd95a836042b86c515328
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339731"
---
# <a name="tools-for-software-tracing"></a>用于软件跟踪的工具


Microsoft Windows Driver Kit (WDK) 包括一套应用程序和软件跟踪用于命令行工具。 这些工具旨在以支持 Windows 事件跟踪 (ETW) 并补充在 Windows 中包含的跟踪工具。

- [跟踪工具有哪些？](#what-are-the-tracing-tools)
- [何时应使用 WPP 软件跟踪或事件跟踪 Windows (ETW) API？](#when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api)
- [什么是在本部分中](#whats-in-this-section)

## <a name="what-are-the-tracing-tools"></a>跟踪工具有哪些？

这些工具包括[跟踪控制器](trace-controller.md)的配置、 启动、 更新和停止跟踪会话，并[跟踪使用者](trace-consumer.md)的接收在会话过程中生成的跟踪消息，并将二进制数据转换为文件或显示的用户可读格式。

这些工具所支持的各种[跟踪提供程序](trace-provider.md)，包括用户模式应用程序和内核模式驱动程序，它通过使用软件跟踪检测[WPP 软件跟踪](wpp-software-tracing.md)或 ([Windows (ETW) 事件跟踪](event-tracing-for-windows--etw-.md)。 比较两个方法检测代码，请参阅[何时使用 WPP 软件跟踪和事件跟踪 Windows (ETW)](#when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api)。

这些工具还可以访问保留[跟踪会话](trace-session.md)内置到 Windows，如[全局记录器跟踪会话](global-logger-trace-session.md) / [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md).

其中某些工具位于工具\\&lt;*平台*&gt;子目录的 Windows Driver Kit (WDK) 中，其中&lt;*平台*&gt;是 x86 或 x64。 其他工具是可以包含在 Windows 或位于 bin\\&lt;*平台*&gt; WDK 的子目录。

## <a name="when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api"></a>何时应使用 WPP 软件跟踪或事件跟踪 Windows (ETW) API？

使用[WPP 软件跟踪](wpp-software-tracing.md)如果您有兴趣主要收集跟踪数据，用于开发和调试目的。 使用[Windows 事件跟踪 (ETW)](event-tracing-for-windows--etw-.md)对于其他类型的跟踪。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 软件跟踪</th>
<th align="left">显示/TraceLogging ETW</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">支持 Windows 2000 及更高版本。</td>
<td align="left">支持 Windows Vista 及更高版本。</td>
</tr>
<tr class="even">
<td align="left">跟踪事件进行开发和调试。 主要是内部开发人员中心。</td>
<td align="left">管理、 操作、 分析和调试目的的跟踪事件。</td>
</tr>
<tr class="even">
<td align="left">需要 TMF 文件进行解码的事件，从该日志记录二进制文件的 PDB 提取。</td>
<td align="left">在本地的二进制文件中或在事件负载中包含要解码事件的元数据。</td>
</tr>
<tr class="odd">
<td align="left">可以为每个跟踪提供程序只有一个活动会话。</td>
<td align="left">事件可以进行多路复用到多个使用者。</td>
</tr>
<tr class="even">
<td align="left">不能本地化消息字符串。</td>
<td align="left">可本地化字符串。</td>
</tr>
<tr class="odd">
<td align="left">提供程序安全性被限制为不共享启用并分别对事件进行解码所需的控件的 GUID 或 TMF 文件。</td>
<td align="left">提供程序可以具有 Acl 应用于限制哪些用户可以从其收集事件。</td>
</tr>
</tbody>
</table> 

有关使用 Windows 软件跟踪预处理器 (WPP) 宏将软件跟踪添加到驱动程序或应用程序的信息，请参阅[WPP 软件跟踪](wpp-software-tracing.md)。

有关使用内核模式 ETW API 的驱动程序的信息，请参阅[事件跟踪 Windows (ETW)](event-tracing-for-windows--etw-.md)。

有关使用 Windows Management Instrumentation (WMI) 扩展对 Windows 驱动程序模型 (WDM) 添加到任何驱动程序软件跟踪的信息，请参阅[WMI 事件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff566350)。

**请注意**   ETW 和 WPP 支持大多数类型的内核模式驱动程序和用户模式应用程序。 但是，ETW 和 WPP 使用不适用于某些类型的驱动程序，例如微型端口驱动程序的类型。 若要确定是否支持特定驱动程序类型，基本 WPP 将宏添加到驱动程序，如[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)并[WPP\_清理](https://msdn.microsoft.com/library/windows/hardware/ff556179)。 如果由于未定义使用的类型，不会进行编译代码，ETW 和 WPP 都不能支持的驱动程序类型。 

## <a name="whats-in-this-section"></a>什么是在本部分中

本部分开头的软件跟踪工具的调查、 讨论基础工具、 概念和 WDK 中包括的软件跟踪工具的文档。

本部分包括：

[软件跟踪工具的调查](survey-of-software-tracing-tools.md)

[跟踪工具概念](tracing-tool-concepts.md)

[TraceView](traceview.md)

[Tracelog](tracelog.md)

[Tracepdb](tracepdb.md)

[Tracefmt](tracefmt.md)

[在启动期间跟踪](tracing-during-boot.md)

[WPP 软件跟踪](wpp-software-tracing.md)

[软件跟踪常见问题](software-tracing-faq.md)

[Windows 事件跟踪 (ETW)](event-tracing-for-windows--etw-.md)

[内核模式性能监视](kernel-mode-performance-monitoring.md)

有关概念性信息[关于事件跟踪](https://msdn.microsoft.com/library/windows/desktop/aa363668)，请参阅 Microsoft Windows SDK 文档。 
