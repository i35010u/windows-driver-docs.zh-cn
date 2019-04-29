---
title: NDIS_STATUS_WDI_INDICATION_CONNECT_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_CONNECT_COMPLETE 指示 OID_WDI_TASK_CONNECT 完成。
ms.assetid: f181f3e4-310f-4346-a6aa-f10398027194
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CONNECT_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 387ec12d8e6dab07694db096425d7e131c16c7b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366397"
---
# <a name="ndisstatuswdiindicationconnectcomplete"></a>NDIS\_状态\_WDI\_指示\_CONNECT\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_CONNECT\_完成，以指示完成[OID\_WDI\_任务\_CONNECT](oid-wdi-task-connect.md)。

| Object |
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
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




