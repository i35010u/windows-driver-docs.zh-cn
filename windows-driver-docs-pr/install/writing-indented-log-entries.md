---
title: 写入缩进日志条目
description: 写入缩进日志条目
keywords:
- 缩进日志条目 WDK Setupapi.log
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，缩进的日志条目
- SetupWriteTextLog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6069209ab49d7f271d481017dbbfaa9d487eb4d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840919"
---
# <a name="writing-indented-log-entries"></a>写入缩进日志条目


如 [文本日志节正文的格式](format-of-a-text-log-section-body.md)中所述， [setupapi.log 文本日志](setupapi-text-logs.md) 中节正文日志条目的格式由以下字段组成：

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

您可以使用日志条目中的 " *缩进* " 字段缩进 *formatted_message* 字段，以使日志条目更易于阅读和理解。 缩进字段中的缩进量取决于为节设置的缩进深度。 缩进深度是缩进单位数，其中缩进单位为5个等宽文本空间。 例如，缩进深度为1将产生5个空格的缩进，缩进深度为2将导致缩进10个空格，依此类推。 最小缩进深度为零，最大缩进深度为16。

默认情况下，节的缩进深度为零。 如果缩进深度为零，则不会缩进 *formatted_message* 字段。 如果应用程序增加缩进深度以写入缩进节条目的序列，则该应用程序还必须编写相应的节条目集，以将缩进深度重置为零，然后应用程序才能写入未缩进的其他节条目。

若要更改某一节的缩进深度，请调用 Setupapi.log 日志记录函数并在以下系统定义的清单常量和提供给 Setupapi.log 日志记录函数的 flags 参数之间使用按位 "或"。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">清单常量</th>
<th align="left">缩进深度更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>TXTLOG_DEPTH_INCR</p></td>
<td align="left"><p>对于当前日志条目和所有后续日志条目，缩进深度将增加1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TXTLOG_DEPTH_DECR</p></td>
<td align="left"><p>对于当前日志条目和所有后续日志条目，缩进深度将减少1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TXTLOG_TAB_1</p></td>
<td align="left"><p>对于当前日志项，缩进深度仅增加1。</p></td>
</tr>
</tbody>
</table>

 

例如，以下对 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) 的调用序列会在节标头后写入一系列缩进的日志条目，其 *section_title* 字段为 "缩进示例"，其 *instance_identifier* 字段为 "instance 0"。

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

如果文本日志的事件级别大于或等于 TXTLOG_DETAILS 并且为文本日志启用了事件类别 TXTLOG_VENDOR，则前面的代码会在节标头后写入以下日志项。

在下面的示例中，省略号 ( ... ) 表示与前一个日志条目处于相同缩进级别的零个或多个附加日志条目。 时间戳将替换为实际时间戳。

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

有关从实际文本日志中提取的缩进节条目的另一个示例，请参阅 [文本日志节正文的格式](format-of-a-text-log-section-body.md)。

 

