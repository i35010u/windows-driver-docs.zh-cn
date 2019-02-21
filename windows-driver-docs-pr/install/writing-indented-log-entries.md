---
title: 写入缩进日志条目
description: 写入缩进日志条目
ms.assetid: 8ce6b433-a004-43f6-9481-9c23c5e7e8da
keywords:
- 缩进的日志条目 WDK SetupAPI
- 格式 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，缩进的日志条目
- SetupWriteTextLog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b40ef65859e8919d115c1da2922c9807e860908e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543923"
---
# <a name="writing-indented-log-entries"></a>写入缩进日志条目


中所述[格式的文本日志部分正文](format-of-a-text-log-section-body.md)，在正文部分的日志条目的格式[SetupAPI 文本日志](setupapi-text-logs.md)包含以下字段：

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

可以使用*缩进*字段中日志条目以缩进*formatted_message*以便轻松地阅读和理解的日志条目的字段。 缩进字段中的缩进量取决于为部分中设置的缩进深度。 缩进深度是缩进单位，其中缩进单位可以是五个等宽字体文本空格数。 例如，缩进深度为 1 会导致的 5 个空格，缩进缩进深度为 2 会导致 10 个空格和等等的缩进。 最小的缩进深度为 0，最大的缩进深度为 16。

默认情况下，一个部分的缩进深度为零。 如果缩进深度为零， *formatted_message*字段将不会进行缩进。 如果应用程序增加缩进深度编写一系列缩进的节条目，该应用程序还必须编写一组对应的节条目重置为零的缩进深度，随后可以编写应用程序之前不缩进的其他节条目。

若要更改某个部分的缩进深度，请调用 SetupAPI 日志记录函数，并使用以下系统定义的清单常量之一提供给 SetupAPI 日志记录函数的标志参数之间的按位 OR。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">清单常量</th>
<th align="left">更改缩进深度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>TXTLOG_DEPTH_INCR</p></td>
<td align="left"><p>缩进深度增加 1 表示当前的日志条目，所有后续的日志条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TXTLOG_DEPTH_DECR</p></td>
<td align="left"><p>缩进深度减少了 1 表示当前的日志条目，所有后续的日志条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TXTLOG_TAB_1</p></td>
<td align="left"><p>缩进深度增加 1 仅为当前的日志条目。</p></td>
</tr>
</tbody>
</table>

 

例如，下面的调用序列[ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)将序列的缩进的日志条目写入部分标头之后其*section_title*字段"缩进示例"且*instance_identifier*字段是"实例 0"。

```cpp
// The LogToken value was previously returned by a call to 
// SetupGetThreadLogToken.
// The LogToken value specifies a section in one of the text logs.

DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_DETAILS;

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Subsection A"));

// Additional SetupWriteTextLog calls that write entries at Subsection A indentation level

SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_INCR, TEXT("Subsection A.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A.1 indentation level

SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_INCR, TEXT("Subsection A.1.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A.1.1 indentation level

SetupWriteTextLog(LogToken, Category, Flags, TEXT("End of Subsection A.1.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A.1 indentation level

SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_DECR, TEXT("End of Subsection A.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A indentation level
SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_DECR, TEXT("End of Subsection A"));
```

如果文本日志事件的事件级别是大于或等于 TXTLOG_DETAILS 和文本日志启用了事件类别 TXTLOG_VENDOR，上面的代码将部分标头之后编写以下日志条目。

在下面的示例中，省略号 （...） 表示在相同级别的缩进与先前的日志条目的零个或多个其他日志项。 时间戳将替换为实际的时间戳。

```cpp
>>>  [Indentation Example - Instance 0]
>>>  2005/02/13 22:06:28.109: Section start
        : Subsection A
...
        :      Subsection A.1
...
        :           Subsection A.1.1
...
        :           End Subsection A.1.1
...
        :      End of Subsection A.1
...
        : End of Subsection A
```

另一个示例中的缩进的节条目拍摄从实际文本日志，请参阅[格式的文本日志部分正文](format-of-a-text-log-section-body.md)。

 

 





