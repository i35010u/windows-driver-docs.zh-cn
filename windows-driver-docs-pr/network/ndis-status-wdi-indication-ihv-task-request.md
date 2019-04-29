---
title: NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 请求 Microsoft 组件队列 IHV 任务。ObjectPort。
ms.assetid: E123F957-574F-4C78-B366-76E886018503
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 40b321c1a34360d07cb14e660c2dc31c32e4cbc0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390681"
---
# <a name="ndisstatuswdiindicationihvtaskrequest"></a>NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求以请求 Microsoft 组件队列 IHV 任务。

| Object |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_TASK\_REQUEST\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn926314) |                                |          | 此任务 IHV 请求的优先级。 请参阅[ **WDI\_IHV\_任务\_优先级**](https://msdn.microsoft.com/library/windows/hardware/dn926064)有效的值的枚举。 |
| [**WDI\_TLV\_IHV\_TASK\_DEVICE\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/dn926313)         |                                | X        | IHV 提供上下文信息转发给[OID\_WDI\_任务\_IHV](oid-wdi-task-ihv.md)。                                       |

 

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


[OID\_WDI\_TASK\_IHV](oid-wdi-task-ihv.md)

 

 




