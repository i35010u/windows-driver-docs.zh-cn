---
title: 设置文本日志的事件级别
description: 设置文本日志的事件级别
keywords:
- 事件级别 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，事件级别
- LogLevel
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a9c353e4631a46b67986cefe7ba0b26ea634950
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816651"
---
# <a name="setting-the-event-level-for-a-text-log"></a>设置文本日志的事件级别


仅当为文本日志设置的事件级别大于或等于日志条目的事件级别，并且为文本日志启用了日志条目的[事件类别](enabling-event-categories-for-a-text-log.md)时， [setupapi.log](setupapi.md)才会将日志条目写入文本日志。

下表列出了 Setupapi.log 支持的事件级别以及表示这些事件级别的清单常量。 TXTLOG_ERROR 是最低的事件级别，接下来的下一个最高事件级别 TXTLOG_WARNING，依此类推。 TXTLOG_VERY_VERBOSE 是最高的事件级别。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件级别</th>
<th align="left">事件级别清单常量</th>
<th align="left">事件级别清单值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>仅写错误。</p></td>
<td align="left"><p>TXTLOG_ERROR</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>写入潜在问题的错误和警告。</p></td>
<td align="left"><p>TXTLOG_WARNING</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>写入错误、警告和系统状态更改。</p></td>
<td align="left"><p>TXTLOG_SYSTEM_STATE_CHANGE</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>写入与状态更改关联的错误、警告、系统状态更改和高级操作。</p></td>
<td align="left"><p>TXTLOG_SUMMARY</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>写入错误、警告、系统状态更改、与状态更改关联的高级操作和大部分操作的详细信息。</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>写入错误、警告、系统状态更改、与状态更改关联的高级操作以及所有操作的详细信息。</p></td>
<td align="left"><p>TXTLOG_VERBOSE</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>写入所有日志条目，其中包括可能会生成大量不太多的信息的日志条目。</p></td>
<td align="left"><p>TXTLOG_VERY_VERBOSE</p></td>
<td align="left"><p>7</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="to-set-the-event-level-for-the-setupapi-text-logs--create--or-modify--the-following-reg-dword-registry-value-"></a>若要设置 Setupapi.log 文本日志的事件级别，请创建 (或修改) 以下 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types) 注册表值：  
**HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ Windows \\ CurrentVersion \\ 安装程序 \\ LogLevel**

如果 **LogLevel** 注册表值不存在或其值为零，则 setupapi.log 将应用程序安装和设备安装文本日志的事件级别设置为下表中所述的默认值：

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
<th align="left">Windows 7 和更高版本 (默认值) </th>
<th align="left">Windows Vista SP2 (默认值) </th>
<th align="left">默认值 (Windows Vista SP1 和早期版本) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>应用程序安装文本日志 (<em>setupapi.log</em>) </p></td>
<td align="left"><p>TXTLOG_SUMMARY</p></td>
<td align="left"><p>TXTLOG_WARNING</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
</tr>
<tr class="even">
<td align="left"><p>设备安装文本日志 (<em>setupapi.log</em>) </p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
</tr>
</tbody>
</table>

 

有关这些文本日志文件的详细信息，请参阅 [Setupapi.log 文本日志](setupapi-text-logs.md)。

**LogLevel** 注册表值的格式为 0x *UUUUGHVW，* 其中：

-   由掩码 0x000000 *VW* 表示的低序位8位指定是否为应用程序安装日志启用日志记录，并指定应用程序日志的事件级别。

-   下一个最高八位（由掩码 0x0000 *GH* 00 表示）指定是否为设备安装文本日志启用日志记录，并指定设备安装文本日志的事件级别。

-   不使用掩码 0x *UUUU* 0000 表示的最高级别的位。

0x *VW* bits 的值控制应用程序安装日志的日志记录，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>0xVW</em> 值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>零 (默认值) </p></td>
<td align="left"><p>启用日志记录后，事件级别将设置为默认值，如前面所述。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01 到0x0F</p></td>
<td align="left"><p>禁用日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10 到0x7F</p></td>
<td align="left"><p>启用日志记录，并将事件级别设置为0xV。</p></td>
</tr>
</tbody>
</table>

 

0x *GH* bits 的值控制设备安装文本日志的日志记录，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>0xGH</em> 值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>零 (默认值) </p></td>
<td align="left"><p>启用日志记录后，事件级别将设置为默认值，如前面所述。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01 到0x0F</p></td>
<td align="left"><p>禁用日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10 到0x7F</p></td>
<td align="left"><p>启用日志记录，并将事件级别设置为0xG。</p></td>
</tr>
</tbody>
</table>

 

下表提供了典型的 **LogLevel** 值的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">LogLevel 值</th>
<th align="left">为文本日志设置的事件级别</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>默认情况下，将为应用程序安装日志和设备安装日志启用日志记录。 将日志记录级别设置为两个日志的默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000101</p></td>
<td align="left"><p>为应用程序安装日志和设备安装日志禁用日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00001010</p></td>
<td align="left"><p>为应用程序安装日志和设备安装日志启用日志记录。 将这两个日志的日志记录级别设置为 TXTLOG_ERROR。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00002020</p></td>
<td align="left"><p>为应用程序安装日志和设备安装日志启用日志记录。 将这两个日志的日志记录级别设置为 TXTLOG_WARNING。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00005050</p></td>
<td align="left"><p>为应用程序安装日志和设备安装日志启用日志记录。 将这两个日志的日志记录级别设置为 TXTLOG_DETAILS。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00006060</p></td>
<td align="left"><p>为应用程序安装日志和设备安装日志启用日志记录。 将这两个日志的日志记录级别设置为 TXTLOG_VERBOSE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00007070</p></td>
<td align="left"><p>为应用程序安装日志和设备安装日志启用日志记录。 将这两个日志的日志记录级别设置为 TXTLOG_VERY_VERBOSE。</p></td>
</tr>
</tbody>
</table>

 

 

