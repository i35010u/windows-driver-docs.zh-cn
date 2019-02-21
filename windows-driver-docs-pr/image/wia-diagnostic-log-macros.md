---
title: WIA 诊断日志宏
description: WIA 诊断日志宏
ms.assetid: 8b544045-e9d7-422b-825c-f1a5531e0e11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d6abf2ddb043b2890ad42cb98f2c74f93009dfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540402"
---
# <a name="wia-diagnostic-log-macros"></a>WIA 诊断日志宏





在 Windows Vista 和更高版本操作系统上处理的错误，请参阅[WIA 驱动程序错误恢复适用于 Windows Vista 的](wia-driver-error-recovery-for-windows-vista.md)。

[诊断日志宏](https://msdn.microsoft.com/library/windows/hardware/ff540599)启用为日志跟踪、 错误和警告消息的微型驱动程序*Wiaservc.log*诊断日志文件。

在 Windows Vista 和更高版本操作系统上的错误处理的详细信息，请参阅[WIA 驱动程序错误恢复适用于 Windows Vista 的](wia-driver-error-recovery-for-windows-vista.md)。

前三个宏可以用于分别写入具有指定类型的错误、 跟踪、 或警告的日志记录语句。 第四个宏可以用于将 HRESULT 转换为的描述性字符串。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>宏</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549580" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549580)"><strong>WIAS_LERROR</strong></a></p></td>
<td><p>写入的日志语句的键入错误<em>Wiaservc.log</em>诊断日志文件...</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549589" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549589)"><strong>WIAS_LHRESULT</strong></a></p></td>
<td><p>HRESULT 值转换为一个字符串，并写入到字符串<em>Wiaservc.log</em>诊断日志文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549600" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549600)"><strong>WIAS_LTRACE</strong></a></p></td>
<td><p>写入到跟踪类型的日志语句<em>Wiaservc.log</em>诊断日志文件...</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549610" data-raw-source="[&lt;strong&gt;WIAS_LWARNING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549610)"><strong>WIAS_LWARNING</strong></a></p></td>
<td><p>写入警告的类型的日志语句<em>Wiaservc.log</em>诊断日志文件...</p></td>
</tr>
<tr class="odd">
<td><p><strong>WIAS_ERROR</strong></p></td>
<td><p>此宏是在 Windows Vista 和更高版本操作系统中可用。</p>
<p>写入的日志语句的键入错误<em>Wiatrace.log</em>诊断日志文件。</p></td>
</tr>
<tr class="even">
<td><p><strong>WIAS_TRACE</strong></p></td>
<td><p>此宏是在 Windows Vista 和更高版本操作系统中可用。</p>
<p>写入到跟踪类型的日志语句<em>Wiatrace.log</em>诊断日志文件。</p></td>
</tr>
</tbody>
</table>

 

有关这些宏的详细信息，请参阅[IWiaLog 界面和诊断日志宏](https://msdn.microsoft.com/library/windows/hardware/ff543937)。

 

 




