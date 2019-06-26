---
title: 什么是 WPP 扩展格式规范字符串
description: 什么是 WPP 扩展格式规范字符串
ms.assetid: f05117c0-cb4b-483a-a141-08423555170a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb74648fffb386f818651f74b102fd130ed111e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371369"
---
# <a name="what-are-the-wpp-extended-format-specification-strings"></a>什么是 WPP 扩展格式规范字符串？


WPP 跟踪消息的费用为定义的标准格式字符串中包含可以使用的预定义的格式规范字符串**printf**。

可以使用 **%！标志 ！** , **%!FUNC ！** 和 **%！级别 ！** 中字符串[跟踪消息前缀](trace-message-prefix.md)，然后在任何跟踪函数或宏，如[ **DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))。

跟踪的任何函数中，可以使用其他扩展的字符串。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">格式字符串</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">软件跟踪</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>%!FILE!</p></td>
<td align="left"><p>显示从其生成的跟踪消息的源文件的名称。 此外可以在使用此变量<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">跟踪消息前缀</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!标志 ！</p></td>
<td align="left"><p>显示的值<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">跟踪标志</a>启用跟踪消息。 此外可以在使用此变量<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">跟踪消息前缀</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!FUNC!</p></td>
<td align="left"><p>显示生成的跟踪消息的函数。 此外可以在使用此变量<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">跟踪消息前缀</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!级别 ！</p></td>
<td align="left"><p>显示的名称<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a>这样的跟踪消息。 此外可以在使用此变量<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">跟踪消息前缀</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!LINE!</p></td>
<td align="left"><p>在生成的跟踪前缀的代码中显示行的行数。 此外可以在使用此变量<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">跟踪消息前缀</a>。</p></td>
</tr>
<tr class="odd">
<td align="left">常规使用</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>%！ bool ！</p></td>
<td align="left"><p>显示 TRUE 或 FALSE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%！ irql ！</p></td>
<td align="left"><p>显示当前 IRQL 的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%！ sid ！</p></td>
<td align="left"><p>为安全标识符 (pSID) 表示的指针。 显示 SID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!SRB!</p></td>
<td align="left"><p>表示到 SCSI 请求块的指针。 显示程序块内容。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!SENSEDATA!</p></td>
<td align="left"><p>表示指向 SCSI SENSE_DATA 的指针。 显示检测数据。</p></td>
</tr>
<tr class="odd">
<td align="left">GUID</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>%!GUID!</p></td>
<td align="left"><p>表示指向 GUID (pGUID) 的指针。 显示所指向的 GUID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!CLSID!</p></td>
<td align="left"><p>类 id。 表示指向类 ID GUID 的指针。 显示与 GUID 关联的字符串。 当设置格式的跟踪消息时，WPP 在注册表中查找字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!IID!</p></td>
<td align="left"><p>接口 id。 向接口 ID GUID 表示的指针。 显示与 GUID 关联的字符串。 当设置格式的跟踪消息时，WPP 在注册表中查找字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!LIBID ！</p></td>
<td align="left"><p>类型库。 表示 COM 类型库的 GUID。 显示与 GUID 关联的字符串。 当设置格式的跟踪消息时，WPP 在注册表中查找字符串。</p></td>
</tr>
<tr class="even">
<td align="left">Time</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>%!delta!</p></td>
<td align="left"><p>显示两个时间值，以毫秒为单位之间的差异。 它是显示在一个 LONGLONG 值<strong>天 ~ h<span class="emoji" shortCode="m">Ⓜ️</span>s</strong>格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!WAITTIME!</p></td>
<td align="left"><p>显示等待要完成，以毫秒为单位的内容所用的时间。 它是显示在一个 LONGLONG 值<strong>天 ~ h<span class="emoji" shortCode="m">Ⓜ️</span>s</strong>格式。</p>
<p>设计用于与<strong>%！ 到期 ！</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%！ 到期 ！</p></td>
<td align="left"><p>显示的内容应完成，以毫秒为单位的时间。 它是显示在一个 LONGLONG 值<strong>天 ~ h<span class="emoji" shortCode="m">Ⓜ️</span>s</strong>格式。</p>
<p>设计用于与<strong>%！等待时间 ！</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!TIMESTAMP!</p>
<p>%！ datetime ！</p>
<p>%！ 时间 ！</p></td>
<td align="left"><p>在特定时间点显示的系统时间的值。 这些是 LARGE_INTEGER SYSTEMTIME 格式显示的值。</p>
<p>若要在程序中的不同的时间值表示和来区分它们，可以使用这些变量。</p></td>
</tr>
<tr class="odd">
<td align="left">返回代码</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>%!STATUS!</p></td>
<td align="left"><p>表示将 status 值并显示状态代码与关联的字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!WINERROR!</p></td>
<td align="left"><p>表示一个 Windows 错误代码，并显示与错误关联的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!HRESULT ！</p></td>
<td align="left"><p>表示错误或警告和 HRESULT 格式显示的代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!没有成功 ！</p></td>
<td align="left"><p>表示 Windows 错误，并显示错误消息字符串。</p></td>
</tr>
<tr class="even">
<td align="left">网络</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>%!IPADDR!</p></td>
<td align="left"><p>表示为 IP 地址的指针。 显示的 IP 地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!PORT!</p></td>
<td align="left"><p>显示端口号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!NETEVENT ！</p></td>
<td align="left"><p>显示网络事件。</p></td>
</tr>
</tbody>
</table>

 

 

 





