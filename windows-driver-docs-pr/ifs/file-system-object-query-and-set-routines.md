---
title: 文件系统对象查询和设置例程
description: 文件系统对象查询和设置例程
ms.assetid: 34b97a6e-a155-443c-94dd-4d8f1fc4b430
keywords:
- 小型重定向程序 WDK，查询操作
- 小型重定向程序 WDK，设置操作
- 查询操作 WDK 网络重定向器
- 设置操作 WDK 网络重定向器
- 文件对象 WDK 微型重定向程序
- 对象 WDK 微型重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe14a4cbd3a8186b7678fbd0f3ba57233d49f1b6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104488"
---
# <a name="file-system-object-query-and-set-routines"></a>文件系统对象查询和设置例程


可由网络小型重定向程序实现的许多例程用于对文件系统对象执行查询和设置操作。 RDBSS 在响应接收 IRP 以查询或设置文件对象的信息时，会发出大部分调用。 因此，RDBSS 接收的 IRP 与 RDBSS 调用的 MRx 查询或设置操作之间有直接的对应关系。

下表列出了可由用于文件系统对象查询和设置操作的网络微重定向程序实现的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序指出路径是否为有效的目录。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxquerydirectory" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](./mrxquerydirectory.md)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求一个有关文件目录系统对象的网络微重定向程序查询信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxqueryeainfo" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](./mrxqueryeainfo.md)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向器查询文件系统对象上的扩展属性信息。 RDBSS 发出此调用以响应接收 IRP_MJ_QUERY_EA。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxqueryfileinfo" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](./mrxqueryfileinfo.md)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求一个有关文件系统对象的网络微型重定向程序查询文件信息。 RDBSS 发出此调用以响应接收 IRP_MJ_QUERY_INFORMATION。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxqueryquotainfo" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](./mrxqueryquotainfo.md)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序查询有关文件系统对象的配额信息。 RDBSS 发出此调用以响应接收 IRP_MJ_QUERY_QUOTA。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxquerysdinfo" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](./mrxquerysdinfo.md)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序查询有关文件系统对象的安全描述符信息。 RDBSS 发出此调用以响应接收 IRP_MJ_QUERY_SECURITY。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxqueryvolumeinfo" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](./mrxqueryvolumeinfo.md)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络最小化重定向器查询卷信息。 RDBSS 发出此调用以响应接收 IRP_MJ_QUERY_VOLUME_INFORMATION。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxseteainfo" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](./mrxseteainfo.md)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序设置文件系统对象的扩展属性信息。 RDBSS 发出此调用以响应接收 IRP_MJ_SET_EA。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxsetfileinfo" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](./mrxsetfileinfo.md)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序在文件系统对象上设置文件信息。 RDBSS 发出此调用以响应接收 IRP_MJ_SET_INFORMATION。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](./mrxsetfileinfoatcleanup.md)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序在清理时设置文件系统对象的文件信息。 当应用程序关闭句柄时，但在关闭之前，RDBSS 将在清理过程中发出此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxsetquotainfo" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](./mrxsetquotainfo.md)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器在文件系统对象上设置配额信息。 RDBSS 发出此调用以响应接收 IRP_MJ_SET_QUOTA。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxsetsdinfo" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](./mrxsetsdinfo.md)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序设置文件系统对象的安全描述符信息。 RDBSS 发出此调用以响应接收 IRP_MJ_SET_SECURITY。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxsetvolumeinfo" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](./mrxsetvolumeinfo.md)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序设置卷信息。 RDBSS 发出此调用以响应接收 IRP_MJ_SET_VOLUME_INFORMATION。</p></td>
</tr>
</tbody>
</table>

 

