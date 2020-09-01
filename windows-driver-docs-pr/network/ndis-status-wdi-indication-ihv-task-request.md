---
title: NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 来请求 Microsoft 组件将 IHV 任务排队。ObjectPort .
ms.assetid: E123F957-574F-4C78-B366-76E886018503
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2321d0cd404099cc4b24449dbcc89e83e53b59b0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217021"
---
# <a name="ndis_status_wdi_indication_ihv_task_request"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ IHV \_ 任务 \_ 请求


微型端口驱动程序使用 NDIS \_ STATUS \_ WDI \_ 指示 \_ ihv \_ 任务 \_ 请求来请求 Microsoft 组件将 IHV 任务排队。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                                         | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ IHV \_ 任务 \_ 请求 \_ 参数**](./wdi-tlv-ihv-task-request-parameters.md) |                                |          | IHV 请求此任务的优先级。 有关有效值，请参阅 [**WDI \_ IHV \_ 任务 \_ 优先级**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ihv_task_priority) 枚举。 |
| [**WDI \_ TLV \_ IHV \_ 任务 \_ 设备 \_ 上下文**](./wdi-tlv-ihv-task-device-context.md)         |                                | X        | IHV 提供的、转发到 [OID \_ WDI \_ 任务 \_ IHV](oid-wdi-task-ihv.md)的上下文信息。                                       |

 

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 任务 \_ IHV](oid-wdi-task-ihv.md)

 

