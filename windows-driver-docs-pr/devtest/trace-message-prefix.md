---
title: 跟踪消息前缀
description: 跟踪消息前缀
ms.assetid: ab400174-cc2a-4cb8-9b7b-390af6464a2e
keywords:
- Tracefmt WDK，跟踪消息前缀
- Tracefmt 的前缀
- 跟踪消息前缀 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4509b06b3d25f4a804014cdcacce703b51367a0b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107310"
---
# <a name="trace-message-prefix"></a>跟踪消息前缀

Tracefmt 向每个跟踪消息添加一个前缀，其中包含存储在 [事件跟踪日志 ( .etl) 文件](trace-log.md) 和 [跟踪消息格式 () 文件](trace-message-format-file.md)中的数据。

默认情况下，Tracefmt 包含特定数据元素，但用户可以通过更改% TRACE \_ FORMAT \_ PREFIX% 环境变量（指定与 **FormatMessage**兼容的消息定义的字符串）来添加和删除元素。

默认跟踪消息前缀的格式如下所示：

```command
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

这会生成以下前缀：

```command
[CPUNumber]ProcessID.ThreadID :: SystemTime [MessageGUIDFriendlyName]
```

每个%*n* 变量都表示一个参数，下表对此进行了说明。

<table>
<thead>
<tr>
<th>前缀变量标识符</th>
<th>变量类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td><p>%1</p></td>
<td><p>字符串</p></td>
<td><p>跟踪消息的 <a href="message-guid.md" data-raw-source="[message GUID](message-guid.md)">消息 GUID</a> 的友好名称。 默认情况下，消息 GUID 的友好名称是在其中生成 <a href="trace-provider.md" data-raw-source="[trace provider](trace-provider.md)">跟踪提供程序</a> 的目录的名称。</p>
<p>若要更改消息 GUID 的友好名称，请将 <strong>-p</strong> 参数与 Tracewpp 或 RUN_WPP 宏一起使用。 有关详细信息，请参阅 Run_WPP 选项。</p></td>
</tr>
<tr class="even">
<td><p>%2</p></td>
<td><p>字符串</p></td>
<td><p>源文件和行号。</p>
<p>此变量表示跟踪消息的友好名称。 默认情况下，跟踪消息的友好名称是源文件的名称和生成跟踪消息的代码的行号。</p></td>
</tr>
<tr>
<td><p>%3</p></td>
<td><p>ULONG</p></td>
<td><p>线程 ID。</p>
<p>标识生成跟踪消息的线程。</p></td>
</tr>
<tr class="even">
<td><p>%4</p></td>
<td><p>字符串</p></td>
<td><p>生成跟踪消息的时间的时间戳。</p></td>
</tr>
<tr>
<td><p>%5</p></td>
<td><p>字符串</p></td>
<td><p>内核时间。</p>
<p>显示生成跟踪消息时内核模式指令的已用执行时间（以 CPU 刻度为单位）。</p></td>
</tr>
<tr class="even">
<td><p>%6</p></td>
<td><p>字符串</p></td>
<td><p>用户时间。</p>
<p>显示生成跟踪消息时用户模式指令的已用执行时间（以 CPU 刻度为单位）。</p></td>
</tr>
<tr>
<td><p>%7</p></td>
<td><p>LONG</p></td>
<td><p>序列号。</p>
<p>显示跟踪消息的本地序列号或全局序列号。 默认情况下，仅在此跟踪会话中唯一的本地序列号为默认值。</p></td>
</tr>
<tr class="even">
<td><p>%8</p></td>
<td><p>ULONG</p></td>
<td><p>进程 ID。</p>
<p>标识生成跟踪消息的进程。</p></td>
</tr>
<tr>
<td><p>%9</p></td>
<td><p>ULONG</p></td>
<td><p>CPU 号。</p>
<p>标识生成跟踪消息的 CPU。</p></td>
</tr>
<tr class="even">
<td><p>%!求!</p></td>
<td><p>字符串</p></td>
<td><p>函数名称。</p>
<p>显示生成跟踪消息的函数的名称。</p></td>
</tr>
<tr>
<td><p>%!随意!</p></td>
<td><p>字符串</p></td>
<td><p>显示启用跟踪消息的 <a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">跟踪标志</a> 的名称。</p>
<p> (因为 <a href="/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"><strong>DoTraceMessage</strong></a> 宏会反转 flags 和 level 参数，DoTraceMessage 生成的消息将在此字段中显示 <a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a> 的值。 ) </p></td>
</tr>
<tr class="even">
<td><p>%!调配!</p></td>
<td><p>字符串</p></td>
<td><p>显示启用跟踪消息的 <a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a> 的值。</p>
<p> (因为 <a href="/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"><strong>DoTraceMessage</strong></a> 宏会反转标志和级别参数，所以由 DoTraceMessage 生成的消息将在该字段中显示 <a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">跟踪标志</a> 的名称。 ) </p></td>
</tr>
<tr>
<td><p>%!COMPNAME!</p></td>
<td><p>字符串</p></td>
<td><p>组件名称。</p>
<p>显示生成跟踪消息的提供程序组件的名称。 仅当在跟踪代码中指定组件名称时，才会显示该组件名称。</p></td>
</tr>
<tr class="even">
<td><p>%!SUBCOMP!</p></td>
<td><p>字符串</p></td>
<td><p>子组件名称。</p>
<p>显示生成跟踪消息的提供程序的子组件的名称。 仅当在跟踪代码中指定组件名称时，才会显示该组件名称。</p></td>
</tr>
</tbody>
</table>

 

感叹号内的符号是一个转换字符，用于指定变量的格式和精度。 例如，%8！04X！ 指定表示为四位无符号十六进制数的进程 ID。 必须包含这些转换字符。

若要更改跟踪消息前缀的元素、顺序或格式，请使用% TRACE \_ FORMAT \_ prefix% 环境变量。 有关示例，请参阅 [示例7：自定义跟踪消息前缀](example-7--customizing-the-trace-message-prefix.md)。

有关 TMF 文件内容的示例，请参阅 tracedrv 示例中的格式跟踪消息。

此外， **-csv** 参数在标准 Tracefmt 前缀之前向每个跟踪消息添加不可配置的详细前缀。 有关 CSV 前缀中的字段的说明，请使用 **-csvheader** 参数。

