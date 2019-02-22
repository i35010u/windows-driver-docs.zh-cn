---
title: 文件系统对象查询和 Set 例程
description: 文件系统对象查询和 Set 例程
ms.assetid: 34b97a6e-a155-443c-94dd-4d8f1fc4b430
keywords:
- 最小重定向程序 WDK，查询操作
- 最小重定向程序 WDK set 运算
- 查询操作 WDK 网络重定向程序
- 将操作设置 WDK 网络重定向程序
- 文件对象 WDK 微型-重定向程序
- 对象 WDK 微型-重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a85652432f7a6328ce169e8a0726bcfb4ce8d21d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554125"
---
# <a name="file-system-object-query-and-set-routines"></a>文件系统对象查询和 Set 例程


数可以通过网络微型重定向的例程用于查询和设置的系统对象的文件上的操作。 RDBSS 发出大部分这些调用以响应接收 IRP 查询或文件对象上设置的信息。 存在 RDBSS 接收 IRP 和 MRx 之间直接的对应关系查询或设置 RDBSS 调用的操作。

下表列出了可以由网络微型重定向文件系统对象查询和设置操作的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550696" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550696)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向指示路径是否是有效的目录。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550755" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550755)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS 文件目录系统对象上调用此例程以请求的网络微型重定向查询信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550759" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550759)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向查询扩展文件系统对象的属性信息。 RDBSS 发出响应接收 IRP_MJ_QUERY_EA 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550770" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550770)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS 对文件系统对象调用此例程以请求的网络微型重定向查询文件信息。 RDBSS 发出响应接收 IRP_MJ_QUERY_INFORMATION 此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550773" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550773)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 对文件系统对象调用此例程以请求的网络微型重定向查询配额信息。 RDBSS 发出响应接收 IRP_MJ_QUERY_QUOTA 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550776" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550776)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS 对文件系统对象调用此例程以请求的网络微型重定向查询安全描述符信息。 RDBSS 发出响应接收 IRP_MJ_QUERY_SECURITY 此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550782" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550782)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求的网络微型重定向查询卷信息。 RDBSS 发出响应接收 IRP_MJ_QUERY_VOLUME_INFORMATION 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550786" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550786)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向程序集扩展文件系统对象的属性信息。 RDBSS 发出响应接收 IRP_MJ_SET_EA 此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550790" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550790)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向设置文件系统对象上的文件信息。 RDBSS 发出响应接收 IRP_MJ_SET_INFORMATION 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550796" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550796)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求的网络微型-重定向程序处清理的文件系统对象上设置文件的信息。 在关闭句柄的应用程序时，清理期间但在关闭之前，RDBSS 发出此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550800" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550800)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，在文件系统对象设置的配额信息。 RDBSS 发出响应接收 IRP_MJ_SET_QUOTA 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550805" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550805)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，在文件系统对象设置安全描述符信息。 RDBSS 发出响应接收 IRP_MJ_SET_SECURITY 此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550810" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550810)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向设置卷信息。 RDBSS 发出响应接收 IRP_MJ_SET_VOLUME_INFORMATION 此调用。</p></td>
</tr>
</tbody>
</table>

 

 

 




