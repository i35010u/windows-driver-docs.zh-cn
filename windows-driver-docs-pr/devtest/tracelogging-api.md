---
title: TraceLogging API
description: TraceLogging API
ms.assetid: AE93DD45-05D7-4E7A-B086-B40A6FA0904B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9895c52486ed41a48d92da60a0053c3761696db5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369708"
---
# <a name="tracelogging-api"></a>TraceLogging API

新建适用于 Windows 10 TraceLogging 是用户模式应用程序和内核模式驱动程序的跟踪框架。 TraceLogging API 基于[事件跟踪 Windows (ETW)](event-tracing-for-windows--etw-.md) ，并提供检测代码的简化的方法来创建本机 C /C++ ETW 提供程序。 TraceLogging 检测可以根据需要，结构化，但不需要单独的检测清单 （XML 文件） 中定义事件和事件数据的开销。 此外，检测使用添加[TraceLogging](https://msdn.microsoft.com/library/windows/desktop/dn904636) API 可以轻松地扩展提供的性能度量和诊断遥测数据。

[TraceLogging](https://msdn.microsoft.com/library/windows/desktop/dn904636) API 的优势[WPP 软件跟踪](wpp-software-tracing.md)或 print 语句，，因为它是可以轻松编写代码，而且还提供了基于清单的 ETW 的优势，因为它是易于调试分析并关联来自收集的跟踪数据的事件。

TraceLogging 基于 ETW 和与现有工具兼容。 使用基于清单的 ETW 提供程序将继续受支持。 没有必要将清单的基于的 ETW 提供程序到 TraceLogging 提供商，除了在这些情况下，需要用遥测数据的事件。

[WPP 软件跟踪](wpp-software-tracing.md)仍受支持。 但是，TraceLogging 具有维护和可扩展性方面的更多好处，并且可以更轻松地在代码中使用。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="tracelogging-for-kernel-mode-drivers-and-components.md" data-raw-source="[TraceLogging for kernel-mode drivers and components](tracelogging-for-kernel-mode-drivers-and-components.md)">TraceLogging 内核模式驱动程序和组件</a></p></td>
<td align="left"><p>本主题介绍如何使用<a href="https://msdn.microsoft.com/library/windows/desktop/dn904636" data-raw-source="[TraceLogging](https://msdn.microsoft.com/library/windows/desktop/dn904636)">TraceLogging</a>从内核模式驱动程序和组件中的 API。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="tracelogging-examples.md" data-raw-source="[TraceLogging Examples](tracelogging-examples.md)">TraceLogging 示例</a></p></td>
<td align="left"><p>本主题中的源代码演示了如何使用 TraceLogging。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-fix-tracelogging-build-errors.md" data-raw-source="[How to fix TraceLogging build errors](how-to-fix-tracelogging-build-errors.md)">如何修复 TraceLogging 生成错误</a></p></td>
<td align="left"><p>本主题介绍一些常见的生成错误和如何解决这些问题。</p></td>
</tr>
</tbody>
</table>
