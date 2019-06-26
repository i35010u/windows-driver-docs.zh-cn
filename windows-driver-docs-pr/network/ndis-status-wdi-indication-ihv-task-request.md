---
title: NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 请求 Microsoft 组件队列 IHV 任务。ObjectPort。
ms.assetid: E123F957-574F-4C78-B366-76E886018503
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: de16d861a746c6f70b6102af966e7860baf1e822
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354940"
---
# <a name="ndisstatuswdiindicationihvtaskrequest"></a>NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求以请求 Microsoft 组件队列 IHV 任务。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_TASK\_REQUEST\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-request-parameters) |                                |          | 此任务 IHV 请求的优先级。 请参阅[ **WDI\_IHV\_任务\_优先级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ihv_task_priority)有效的值的枚举。 |
| [**WDI\_TLV\_IHV\_TASK\_DEVICE\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-device-context)         |                                | X        | IHV 提供上下文信息转发给[OID\_WDI\_任务\_IHV](oid-wdi-task-ihv.md)。                                       |

 

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

 

 




