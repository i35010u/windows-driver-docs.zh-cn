---
title: 状态值
description: 状态值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 956bb7b491b21ba06442c33b3241af702126b376
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818333"
---
# <a name="status-values"></a>状态值





远程 NDIS 状态值通常等效于 Microsoft Windows 2000 驱动程序开发工具包 (DDK) 中定义的32位状态值。 下面列出了本规范中使用的特定远程 NDIS 状态值，可以从 Windows 2000 DDK 或联机文档中推断出其他值。 设备可能会在生成的消息的 *状态* 字段中返回任何语义正确的远程 NDIS 状态值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态标识符</th>
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_SUCCESS</p></td>
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>成功</p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_FAILURE</p></td>
<td align="left"><p>0xC00000001</p></td>
<td align="left"><p> (等效于 STATUS_UNSUCCESSFUL 的未指定错误) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_INVALID_DATA</p></td>
<td align="left"><p>0xC0010015</p></td>
<td align="left"><p>数据无效错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_NOT_SUPPORTED</p></td>
<td align="left"><p>0xC00000BB</p></td>
<td align="left"><p>不支持的请求错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_MEDIA_CONNECT</p></td>
<td align="left"><p>0x4001000B</p></td>
<td align="left"><p>设备连接到与 Windows 2000 DDK 中 NDIS_STATUS_MEDIA_CONNECT 等效的 network medium () </p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_MEDIA_DISCONNECT</p></td>
<td align="left"><p>0x4001000C</p></td>
<td align="left"><p>设备与网络媒体断开连接 (等效于 Windows 2000 DDK 中的 NDIS_STATUS_MEDIA_DISCONNECT) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_Xxx</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>等于在 Windows 2000 DDK 或联机文档中定义 NDIS_STATUS_Xxx 值</p></td>
</tr>
</tbody>
</table>

 

 

 





