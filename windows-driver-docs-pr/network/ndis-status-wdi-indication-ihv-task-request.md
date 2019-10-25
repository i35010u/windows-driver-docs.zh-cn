---
title: NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 来请求 Microsoft 组件将 IHV 任务排队。ObjectPort .
ms.assetid: E123F957-574F-4C78-B366-76E886018503
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 151e2a75cca57edbde7a60a7149042d40bda910b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843462"
---
# <a name="ndis_status_wdi_indication_ihv_task_request"></a>NDIS\_状态\_WDI\_指示\_IHV\_TASK\_请求


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_IHV\_TASK\_请求，请求 Microsoft 组件将 IHV 任务排队。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 在任务栏的搜索框中键入                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_任务\_请求\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-request-parameters) |                                |          | IHV 请求此任务的优先级。 有关有效值，请参阅[**WDI\_IHV\_任务\_优先级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ihv_task_priority)枚举。 |
| [**WDI\_TLV\_IHV\_任务\_设备\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-device-context)         |                                | X        | 由 IHV 提供的上下文信息转发到[OID\_WDI\_TASK\_IHV](oid-wdi-task-ihv.md)。                                       |

 

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
<td><p>Windows 10</p></td>
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


[OID\_WDI\_任务\_IHV](oid-wdi-task-ihv.md)

 

 




