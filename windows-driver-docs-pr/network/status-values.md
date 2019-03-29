---
title: 状态值
description: 状态值
ms.assetid: 1d5cce4a-9830-4e2e-af90-fc1fecfb0fc9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60af504f094a74bee4c1a5b59f6235b6e5b9ecf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575790"
---
# <a name="status-values"></a>状态值





远程 NDIS 状态值是定义在 Microsoft Windows 2000 驱动程序开发工具包 (DDK) 的 32 位状态值通常等效的。 下面列出了此规范中使用的特定远程 NDIS 状态值，其他人可以从 Windows 2000 DDK 或联机文档推断出。 设备可能会返回任何语义正确中的远程 NDIS 状态值*状态*一条消息，它将生成的字段。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态标识符</th>
<th align="left">值</th>
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
<td align="left"><p>未指定的错误 （相当于 STATUS_UNSUCCESSFUL）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_INVALID_DATA</p></td>
<td align="left"><p>0xC0010015</p></td>
<td align="left"><p>无效的数据错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_NOT_SUPPORTED</p></td>
<td align="left"><p>0xC00000BB</p></td>
<td align="left"><p>不支持的请求错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_MEDIA_CONNECT</p></td>
<td align="left"><p>0x4001000B</p></td>
<td align="left"><p>设备连接到网络中 （相当于 NDIS_STATUS_MEDIA_CONNECT 从 Windows 2000 DDK）</p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_MEDIA_DISCONNECT</p></td>
<td align="left"><p>0x4001000C</p></td>
<td align="left"><p>设备已断开网络中 （相当于 NDIS_STATUS_MEDIA_DISCONNECT 从 Windows 2000 DDK）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_Xxx</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>为 Windows 2000 DDK 或联机文档中定义的 NDIS_STATUS_Xxx 值等于</p></td>
</tr>
</tbody>
</table>

 

 

 





