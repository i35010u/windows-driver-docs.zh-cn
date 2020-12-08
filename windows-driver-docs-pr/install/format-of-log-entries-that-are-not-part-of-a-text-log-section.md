---
title: 不是文本日志部分的日志条目的格式
description: 不是文本日志部分的日志条目的格式
keywords:
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，项不属于部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 157dc0a184e2e887f675fcfd5f8118b8617e6050
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820161"
---
# <a name="format-of-log-entries-that-are-not-part-of-a-text-log-section"></a>不是文本日志部分的日志条目的格式


文本日志可以包含不属于文本日志标头或文本日志部分的日志项。 此类项并不与任何部分关联，通常情况下，在各节之间交错。 此类日志条目的格式由 *条目* _ *前缀* 字段、 *time_stamp* 字段、 *event_category* 字段和 *formatted_message* 字段组成，如下所示：

*entry_prefix time_stamp event_category formatted_message*

以下列表描述了日志条目的字段：

<a href="" id="entry-prefix-field"></a>*entry_prefix* 字段  
指示消息类型： " *Entry_prefix* " 字段始终存在，其中包含下表的左侧列中列出的字符串之一，其中字符串的含义显示在右侧列中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Entry_prefix 字段</th>
<th align="left">消息类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"!!!  "</code></pre></td>
<td align="left"><p>文本日志中的错误消息</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"!    "</code></pre></td>
<td align="left"><p>文本日志中的警告消息</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"   . "</code></pre></td>
<td align="left"><p>文本日志中的信息消息 (不是错误消息或警告消息) </p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"     "</code></pre></td>
<td align="left"><p>应用程序安装文本日志中的信息消息 (不是错误消息或警告消息) </p></td>
</tr>
</tbody>
</table>

 

<a href="" id="time-stamp-field"></a>*time_stamp* 字段  
指示发生日志事件的系统时间。 *Time_stamp* 字段是可选的，仅当安装应用程序请求为日志条目包含时间戳时，此字段才会出现。 *Time_stamp* 字段的格式与 [文本日志节标头格式](format-of-a-text-log-section-header.md)中所述的格式相同。

<a href="" id="event-category-field"></a>*event_category* 字段  
指示执行日志条目的 Setupapi.log 操作的类别。 *Event_category* 字段通常存在，但不是必需的。 如果存在，则 " *event_category* " 字段包含一个字符串，这些字符串以 [文本日志节正文的格式](format-of-a-text-log-section-body.md)列出。

<a href="" id="formatted-message"></a>*formatted_message*  
包含特定于日志项的信息。 *Formatted_message* 字段通常存在，但不是必需的。

**注意**  日志条目的最大长度，以字符为336。

 

下面是从设备安装文本日志获取文本日志条目的示例。 在此示例中，前两个日志项不是文本日志节的一部分。 用户模式即插即用 (PnP) manager 在设备安装文本日志中写入这些日志条目，以指示开始安装 PCI 设备的服务器端。 服务器端安装又创建了文本日志部分，该部分由该示例中的前两个日志条目后面的文本日志节标头指示。

请注意，前两个日志条目的 " *event_category* " 字段指示用户模式 PnP 管理器编写了这些日志条目。

```cpp
   . ump: Start service install for: PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38
   . ump: Creating Install Process: rundll32.exe

>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
```

 

 





