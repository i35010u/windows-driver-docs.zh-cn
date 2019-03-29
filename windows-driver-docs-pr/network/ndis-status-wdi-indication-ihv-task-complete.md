---
title: NDIS_STATUS_WDI_INDICATION_IHV_TASK_COMPLETE
description: NDIS_STATUS_WDI_INDICATION_IHV_TASK_COMPLETE 指示 OID_WDI_TASK_IHV 完成。
ms.assetid: 03EA1580-110D-483B-BD4D-9275A7AC18A8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_IHV_TASK_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 01103caf1cfb5b576ee47556ae64447d94c0a118
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577350"
---
# <a name="ndisstatuswdiindicationihvtaskcomplete"></a>NDIS\_状态\_WDI\_指示\_IHV\_任务\_完成


NDIS\_状态\_WDI\_指示\_IHV\_任务\_完成指示完成[OID\_WDI\_任务\_IHV](oid-wdi-task-ihv.md)。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


此指示不包含任何其他数据。 标头中的数据就足够了。 从消息的完成状态不转发到的任何人。

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

 

 




