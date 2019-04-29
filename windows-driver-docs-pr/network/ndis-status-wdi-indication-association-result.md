---
title: NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT 指示关联结果。
ms.assetid: dc025aec-30f4-4a78-b449-acc49d13b507
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fb71ef33a3008a20e973dafcd59204b302088d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366409"
---
# <a name="ndisstatuswdiindicationassociationresult"></a>NDIS\_状态\_WDI\_指示\_关联\_结果


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_关联\_结果以指示关联结果。

| Object |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                     | 允许多个 TLV 实例 | 可选 | 描述                    |
|--------------------------------------------------------------------------|--------------------------------|----------|--------------------------------|
| [**WDI\_TLV\_ASSOCIATION\_RESULT**](https://msdn.microsoft.com/library/windows/hardware/dn926140) | X                              |          | 关联结果的列表。 |

 

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

## <a name="see-also"></a>请参阅


[OID\_WDI\_TASK\_CONNECT](oid-wdi-task-connect.md)

[OID\_WDI\_TASK\_ROAM](oid-wdi-task-roam.md)

 

 




