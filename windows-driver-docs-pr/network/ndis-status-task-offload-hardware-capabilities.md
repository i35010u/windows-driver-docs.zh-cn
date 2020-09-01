---
title: NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES
description: NDIS 微型端口驱动程序和 MUX 中间驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 状态指示，通知 NDIS 和过量驱动程序已更改基础 NIC 的任务卸载硬件功能。
ms.assetid: 9ac8f4c9-66f4-4889-932b-a51381c54734
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f699ee40b02a110112a7210d6496827a3ec4dd31
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215518"
---
# <a name="ndis_status_task_offload_hardware_capabilities"></a>NDIS \_ 状态 \_ 任务 \_ 卸载 \_ 硬件 \_ 功能


NDIS 微型端口驱动程序和 MUX 中间驱动程序使用 **ndis \_ 状态 \_ 任务 " \_ 卸载 \_ 硬件 \_ 功能** " 状态指示通知 NDIS 和过量驱动程序已更改基础 NIC 的任务卸载硬件功能。

<a name="remarks"></a>备注
-------

如果添加或删除了基础 NIC，则与微型端口驱动程序或 MUX 中间驱动程序相关联的一组硬件功能可能会更改。 例如，如果微型端口驱动程序发出 **NDIS \_ 状态任务 \_ " \_ 卸载 \_ 硬件 \_ 功能** 状态指示"，指定它不能支持 (LSO) 的大规模发送卸载，则无法再将 NIC 配置为支持 lso。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。 此结构指定任务卸载硬件功能。

有关任务卸载硬件功能的详细信息，请参阅 [OID \_ TCP \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-offload-hardware-capabilities.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ 状态 \_ 任务 \_ 卸载 \_ 当前 \_ 配置**](ndis-status-task-offload-current-config.md)

[OID \_ TCP \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-offload-hardware-capabilities.md)

 

