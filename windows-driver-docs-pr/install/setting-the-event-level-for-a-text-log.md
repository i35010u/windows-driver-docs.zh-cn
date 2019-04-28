---
title: 设置文本日志的事件级别
description: 设置文本日志的事件级别
ms.assetid: 3dfd2df3-179e-434c-97fb-fd8329198f8a
keywords:
- 事件级别 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，事件级别
- 日志级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5211e76e3837d4d52cdb7d99c5b7ba476444dd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348676"
---
# <a name="setting-the-event-level-for-a-text-log"></a>设置文本日志的事件级别


[SetupAPI](setupapi.md)写入日志项的文本日志仅当事件级别设置文本日志是大于或等于日志条目事件的事件级别和[事件类别](enabling-event-categories-for-a-text-log.md)日志条目启用文本日志。

下表列出了安装程序 Api 支持的事件级别和表示这些事件级别的清单常量。 TXTLOG_ERROR 是最低的事件级别后, 跟的下一步最高事件级别 TXTLOG_WARNING，依此类推。 TXTLOG_VERY_VERBOSE 是最高事件级别。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件级别</th>
<th align="left">事件级别的清单常量</th>
<th align="left">事件级别清单值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>编写仅限错误。</p></td>
<td align="left"><p>TXTLOG_ERROR</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>编写错误和警告的潜在问题。</p></td>
<td align="left"><p>TXTLOG_WARNING</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>编写错误、 警告和系统状态更改。</p></td>
<td align="left"><p>TXTLOG_SYSTEM_STATE_CHANGE</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>编写错误、 警告、 系统状态更改和相关联的状态更改的高级操作。</p></td>
<td align="left"><p>TXTLOG_SUMMARY</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>编写错误、 警告、 系统状态更改、 状态更改和最操作的详细信息与相关联的高级操作。</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>编写错误、 警告、 系统状态更改、 状态更改和所有操作的详细信息与相关联的高级操作。</p></td>
<td align="left"><p>TXTLOG_VERBOSE</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>写入所有日志项，包括那些可能会生成大量的是经常多余的信息。</p></td>
<td align="left"><p>TXTLOG_VERY_VERBOSE</p></td>
<td align="left"><p>7</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="to-set-the-event-level-for-the-setupapi-text-logs--create--or-modify--the-following-reg-dword-registry-value-"></a>若要设置 SetupAPI 文本日志事件的事件级别，创建 （或修改） 以下[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)注册表值：  
**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Setup\\LogLevel**

如果**LogLevel**注册表值不存在或值为零，SetupAPI 下表中所述的默认值设置为应用程序安装和设备安装的事件级别文本日志：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">文本日志</th>
<th align="left">默认值 （Windows 7 和更高版本）</th>
<th align="left">默认值 (Windows Vista SP2)</th>
<th align="left">默认值 （Windows Vista SP1 和早期版本）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>应用程序安装文本日志 (<em>SetupAPI.app.log</em>)</p></td>
<td align="left"><p>TXTLOG_SUMMARY</p></td>
<td align="left"><p>TXTLOG_WARNING</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
</tr>
<tr class="even">
<td align="left"><p>设备安装文本日志 (<em>SetupAPI.dev.log</em>)</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
</tr>
</tbody>
</table>

 

有关这些文本日志文件的详细信息，请参阅[SetupAPI 文本日志](setupapi-text-logs.md)。

**LogLevel**注册表值的格式设置为 0 x*UUUUGHVW，* 其中：

-   低序位八位，表示由掩码 0x000000*VW*，指定是否为应用程序安装日志启用日志记录并指定应用程序日志的事件级别。

-   下一步最高八位为单位表示的掩码 0x0000*GH*00，指定是否为设备安装文本日志启用了日志记录，并且可以指定设备安装文本日志事件的事件级别。

-   最高级别的位，表示由掩码 0x*UUUU*0000，不使用。

值 0x*VW*位控制日志记录下表中所示的应用程序安装日志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>0xVW</em>值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>零 （默认值）</p></td>
<td align="left"><p>启用日志记录和事件级别设置为默认值，如前面所述。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01 通过 0x0F</p></td>
<td align="left"><p>禁用日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>通过 0x7F 0x10</p></td>
<td align="left"><p>启用日志记录并设置为 0xV 的事件级别。</p></td>
</tr>
</tbody>
</table>

 

值 0x*GH*位控制设备安装文本日志下表中所示的日志记录。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>0xGH</em>值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>零 （默认值）</p></td>
<td align="left"><p>启用日志记录和事件级别设置为默认值，如前面所述。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01 通过 0x0F</p></td>
<td align="left"><p>禁用日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>通过 0x7F 0x10</p></td>
<td align="left"><p>启用日志记录并设置为 0xG 的事件级别。</p></td>
</tr>
</tbody>
</table>

 

下表提供了典型的示例**LogLevel**值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">日志级别值</th>
<th align="left">事件级别设置为文本日志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>默认情况下，将为应用程序安装日志和设备安装日志记录功能。 将日志记录级别设置为这两种日志的默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000101</p></td>
<td align="left"><p>禁用日志记录应用程序安装日志和设备安装日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00001010</p></td>
<td align="left"><p>将为应用程序安装日志和设备安装日志记录功能。 将日志记录级别设置为 TXTLOG_ERROR 这两种日志。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00002020</p></td>
<td align="left"><p>将为应用程序安装日志和设备安装日志记录功能。 将日志记录级别设置为 TXTLOG_WARNING 这两种日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00005050</p></td>
<td align="left"><p>将为应用程序安装日志和设备安装日志记录功能。 将日志记录级别设置为 TXTLOG_DETAILS 这两种日志。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00006060</p></td>
<td align="left"><p>将为应用程序安装日志和设备安装日志记录功能。 将日志记录级别设置为 TXTLOG_VERBOSE 这两种日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00007070</p></td>
<td align="left"><p>将为应用程序安装日志和设备安装日志记录功能。 将日志记录级别设置为 TXTLOG_VERY_VERBOSE 这两种日志。</p></td>
</tr>
</tbody>
</table>

 

 

 





