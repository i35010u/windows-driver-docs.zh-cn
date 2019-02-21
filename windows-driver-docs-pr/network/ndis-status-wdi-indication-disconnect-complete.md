---
title: NDIS_STATUS_WDI_INDICATION_DISCONNECT_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DISCONNECT_COMPLETE 指示 OID_WDI_TASK_DISCONNECT 完成。
ms.assetid: 07f14f77-04e9-4991-9a50-9e2d13afcfe9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_DISCONNECT_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 329daf40c8c6410dfafcaee5e59812ec629f9885
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523539"
---
# <a name="ndisstatuswdiindicationdisconnectcomplete"></a>NDIS\_状态\_WDI\_指示\_断开连接\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_断开连接\_完成，以指示完成[OID\_WDI\_任务\_断开连接](oid-wdi-task-disconnect.md)。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


此指示不包含任何其他数据。 标头中的数据就足够了。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




