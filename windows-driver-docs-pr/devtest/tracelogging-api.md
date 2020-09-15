---
title: TraceLogging API
description: TraceLogging API
ms.assetid: AE93DD45-05D7-4E7A-B086-B40A6FA0904B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 668478a4b4f72c32fe6f290634b1478cc666e682
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106630"
---
# <a name="tracelogging-api"></a>TraceLogging API

Windows 10 的新功能 TraceLogging 是用户模式应用程序和内核模式驱动程序的跟踪框架。 TraceLogging API 基于 [Windows (ETW) 的事件跟踪 ](event-tracing-for-windows--etw-.md) ，并提供一种简化代码来创建本机 C/c + + ETW 提供程序的方法。 TraceLogging 规范可以根据需要进行构造，但不需要在单独的检测清单中定义事件和事件数据的开销)  (的 XML 文件。 此外，通过 [TraceLogging](/windows/desktop/tracelogging/trace-logging-portal) API 添加的检测可以轻松地进行扩展，以便为性能度量和诊断提供遥测数据。

[TraceLogging](/windows/desktop/tracelogging/trace-logging-portal) API 提供了[WPP 软件跟踪](wpp-software-tracing.md)或调试 print 语句的优点，因为它易于编写代码，并且还提供了基于清单的 ETW 的优点，因为这样可以轻松地分析和关联所收集的跟踪数据中的事件。

TraceLogging 构建于 ETW 上，并与现有工具兼容。 将继续支持使用基于清单的 ETW 的提供程序。 无需将基于清单的 ETW 提供程序转换为 TraceLogging 提供程序，在需要遥测数据的事件的情况下除外。

仍支持[WPP 软件跟踪](wpp-software-tracing.md)。 但是，TraceLogging 在维护和扩展性方面提供了许多优势，并且在代码中更易于使用。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="tracelogging-for-kernel-mode-drivers-and-components.md" data-raw-source="[TraceLogging for kernel-mode drivers and components](tracelogging-for-kernel-mode-drivers-and-components.md)">内核模式驱动程序和组件的 TraceLogging</a></p></td>
<td align="left"><p>本主题介绍如何使用内核模式驱动程序和组件中的 <a href="/windows/desktop/tracelogging/trace-logging-portal" data-raw-source="[TraceLogging](/windows/desktop/tracelogging/trace-logging-portal)">TraceLogging</a> API。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="tracelogging-examples.md" data-raw-source="[TraceLogging Examples](tracelogging-examples.md)">TraceLogging 示例</a></p></td>
<td align="left"><p>本主题中的源代码演示了如何使用 TraceLogging。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-fix-tracelogging-build-errors.md" data-raw-source="[How to fix TraceLogging build errors](how-to-fix-tracelogging-build-errors.md)">如何修复 TraceLogging 生成错误</a></p></td>
<td align="left"><p>本主题介绍一些常见的生成错误以及如何解决这些错误。</p></td>
</tr>
</tbody>
</table>