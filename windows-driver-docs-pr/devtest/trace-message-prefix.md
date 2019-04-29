---
title: 跟踪消息前缀
description: 跟踪消息前缀
ms.assetid: ab400174-cc2a-4cb8-9b7b-390af6464a2e
keywords:
- Tracefmt WDK，跟踪消息前缀
- 前缀 WDK Tracefmt
- 跟踪消息前缀 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95228298ec048e0753e108691eed2546cdfadc52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354641"
---
# <a name="trace-message-prefix"></a>跟踪消息前缀

Tracefmt 将前缀添加到包含的数据存储在每条跟踪消息[事件跟踪日志 (.etl) 文件](trace-log.md)并[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)。

Tracefmt 默认情况下，包括特定的数据元素，但用户可以添加和删除元素通过更改跟踪的 %\_格式\_前缀 %环境变量，一个字符串，指定与兼容的消息定义**FormatMessage**。

默认跟踪消息前缀的格式如下所示：

```command
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

这会生成以下前缀：

```command
[CPUNumber]ProcessID.ThreadID :: SystemTime [MessageGUIDFriendlyName]
```

每个 %*n*变量表示下表中描述的参数。

<table>
<thead>
<tr>
<th>前缀变量标识符</th>
<th>变量类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><p>%1</p></td>
<td><p>string</p></td>
<td><p>友好名称<a href="message-guid.md" data-raw-source="[message GUID](message-guid.md)">消息 GUID</a>的跟踪消息。 默认情况下，一条消息的 GUID 的友好名称是在其中的目录名称<a href="trace-provider.md" data-raw-source="[trace provider](trace-provider.md)">跟踪提供程序</a>生成。</p>
<p>若要更改消息的 GUID 的友好名称，请使用<strong>-p</strong>参数与 Tracewpp 或 RUN_WPP 宏。 有关详细信息，请参阅 Run_WPP 选项。</p></td>
</tr>
<tr class="even">
<td><p>%2</p></td>
<td><p>string</p></td>
<td><p>源文件和行号。</p>
<p>此变量表示的跟踪消息的友好名称。 默认情况下，跟踪消息的友好名称为源文件和生成的跟踪消息的代码的行号的名称。</p></td>
</tr>
<tr>
<td><p>%3</p></td>
<td><p>ULONG</p></td>
<td><p>线程 id。</p>
<p>标识生成的跟踪消息的线程。</p></td>
</tr>
<tr class="even">
<td><p>%4</p></td>
<td><p>string</p></td>
<td><p>生成的跟踪消息的时间的时间戳。</p></td>
</tr>
<tr>
<td><p>%5</p></td>
<td><p>string</p></td>
<td><p>内核时间。</p>
<p>在生成的跟踪消息的时间中 CPU 时钟周期数，显示内核模式的说明，已用的执行时间。</p></td>
</tr>
<tr class="even">
<td><p>%6</p></td>
<td><p>string</p></td>
<td><p>用户时间。</p>
<p>在生成的跟踪消息的时间中 CPU 时钟周期数，显示用户模式下的说明，已用的执行时间。</p></td>
</tr>
<tr>
<td><p>%7</p></td>
<td><p>长</p></td>
<td><p>序列号。</p>
<p>显示跟踪消息的本地或全局序列号。 本地序列号，是仅对此跟踪会话唯一的这是默认值。</p></td>
</tr>
<tr class="even">
<td><p>%8</p></td>
<td><p>ULONG</p></td>
<td><p>进程 id。</p>
<p>标识生成的跟踪消息的进程。</p></td>
</tr>
<tr>
<td><p>%9</p></td>
<td><p>ULONG</p></td>
<td><p>CPU 数。</p>
<p>标识在其生成的跟踪消息的 CPU。</p></td>
</tr>
<tr class="even">
<td><p>%!FUNC!</p></td>
<td><p>string</p></td>
<td><p>函数名称。</p>
<p>显示生成的跟踪消息的函数的名称。</p></td>
</tr>
<tr>
<td><p>%!标志 ！</p></td>
<td><p>string</p></td>
<td><p>显示的名称<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">跟踪标志</a>启用跟踪消息。</p>
<p>(因为<a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"> <strong>DoTraceMessage</strong> </a>宏反转的标志和级别的参数，生成的 DoTraceMessage 消息显示的值<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a>此字段中.)</p></td>
</tr>
<tr class="even">
<td><p>%!级别 ！</p></td>
<td><p>string</p></td>
<td><p>显示的值<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a>这样的跟踪消息。</p>
<p>(因为<a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"> <strong>DoTraceMessage</strong> </a>宏反转的标志和级别的参数，生成的 DoTraceMessage 消息显示的名称<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">跟踪标志</a>此字段中。)</p></td>
</tr>
<tr>
<td><p>%!COMPNAME!</p></td>
<td><p>string</p></td>
<td><p>组件名称。</p>
<p>显示生成的跟踪消息的提供程序的组件的名称。 仅当指定的跟踪代码中，将显示该组件名称。</p></td>
</tr>
<tr class="even">
<td><p>%!SUBCOMP!</p></td>
<td><p>string</p></td>
<td><p>子组件名称。</p>
<p>显示生成的跟踪消息的提供程序的子组件名称。 仅当指定的跟踪代码中，将显示该组件名称。</p></td>
</tr>
</tbody>
</table>

 

在感叹号符号是指定的格式设置和变量的精度的转换字符。 例如，%8 ！ 04x ！ 指定的进程 ID 表示为一个四位数字的、 无符号十六进制数字。 必须包含这些转换字符。

若要更改的元素，顺序，或格式设置的跟踪消息前缀，使用 %跟踪\_格式\_前缀 %环境变量。 有关示例，请参阅[示例 7:自定义跟踪消息前缀](example-7--customizing-the-trace-message-prefix.md)。

TMF 文件中的内容的示例，请参阅从 tracedrv 示例的格式化跟踪消息。

此外， **csv**参数将不可配置的详细前缀添加到之前的标准 Tracefmt 前缀每条跟踪消息。 对于 CSV 前缀中的字段的说明，请使用 **-csvheader**参数。

 

 





