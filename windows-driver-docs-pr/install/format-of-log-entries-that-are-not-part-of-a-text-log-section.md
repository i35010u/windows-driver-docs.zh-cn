---
title: 不是文本日志部分的日志条目的格式
description: 不是文本日志部分的日志条目的格式
ms.assetid: c2c7567e-dfb4-49d3-acc9-034f6544633e
keywords:
- 格式 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，项不属于部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8489381804a608883393c34c73ddd9a987b519af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377055"
---
# <a name="format-of-log-entries-that-are-not-part-of-a-text-log-section"></a>不是文本日志部分的日志条目的格式


文本日志可以包含不是文本日志标头或文本日志部分的一部分的日志条目。 此类条目不与任何节相关联，一般情况下，交错的各部分之间。 此类日志条目的格式组成*条目*_*前缀*字段中， *time_stamp*字段中， *event_category*字段，且*formatted_message*字段中，按如下所示：

*entry_prefix time_stamp event_category formatted_message*

以下列表介绍了日志条目的字段：

<a href="" id="entry-prefix-field"></a>*entry_prefix* field  
指示消息类型。 *Entry_prefix*字段将始终存在，其中包含下表中，该字符串的含义右侧列中的指示位置的左侧列中列出的字符串之一。

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
<td align="left"><p>文本日志中的一条警告消息</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"   . "</code></pre></td>
<td align="left"><p>文本日志 （而不是一条错误消息或警告消息） 中的信息消息</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"     "</code></pre></td>
<td align="left"><p>应用程序安装文本日志 （而不是一条错误消息或警告消息） 中的信息消息</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="time-stamp-field"></a>*time_stamp* field  
指示记录的事件发生时的系统时间。 *Time_stamp*字段是可选的将会显示仅当安装应用程序请求的时间戳是包含日志条目。 格式*time_stamp*字段是与中所述的相同[文本日志部分标头的格式](format-of-a-text-log-section-header.md)。

<a href="" id="event-category-field"></a>*event_category* field  
表示所做的日志条目的安装程序 Api 操作的类别。 *Event_category*字段通常存在，但不是必需的。 如果存在，请*event_category*字段包含字符串中列出的之一[文本日志部分正文的格式](format-of-a-text-log-section-body.md)。

<a href="" id="formatted-message"></a>*formatted_message*  
包含特定于日志条目的信息。 *Formatted_message*字段通常存在，但不是必需的。

**请注意**  以字符为单位的日志条目的最大长度为 336。

 

文本日志条目的下面的示例取自设备安装文本日志。 在示例中，第一个的两个日志条目不是文本日志部分的一部分。 用户模式下插 (PnP) 管理器中设备安装文本日志，以指示 PCI 设备的服务器端的安装开始编写了这些日志条目。 服务器端的安装过程中，依次创建文本日志部分标头后面的示例中的第一个两个日志条目指定的文本日志部分。

请注意， *event_category*字段为前两个日志条目指示在用户模式即插即用管理器，编写这些日志条目。

```cpp
   . ump: Start service install for: PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38
   . ump: Creating Install Process: rundll32.exe

>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
```

 

 





