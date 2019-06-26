---
title: NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES
description: NDIS 微型端口驱动程序和 MUX 中间驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 状态指示通知 NDIS 和基础驱动程序已在任务中的更改卸载硬件功能的基础的 nic。
ms.assetid: 9ac8f4c9-66f4-4889-932b-a51381c54734
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ecbdd576b12ae9c111945905f1b5ce70a7788312
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372571"
---
# <a name="ndisstatustaskoffloadhardwarecapabilities"></a>NDIS\_状态\_任务\_卸载\_硬件\_功能


NDIS 微型端口驱动程序和 MUX 驱动程序使用的中间**NDIS\_状态\_任务\_卸载\_硬件\_功能**状态指示通知 NDIS和基础驱动程序已在任务中的更改卸载硬件功能的基础的 nic。

<a name="remarks"></a>备注
-------

如果在添加或删除基础 NIC，可以更改与微型端口驱动程序或 MUX 中间驱动程序相关联的总体硬件功能集。 例如，如果微型端口驱动程序将发出**NDIS\_状态\_任务\_卸载\_硬件\_功能**状态指示，它不能指定支持大量发送卸载 (LSO)，NIC 不再可配置为支持 LSO。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。 此结构指定任务卸载的硬件功能。

有关任务卸载硬件功能的详细信息，请参阅[OID\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状态\_任务\_卸载\_当前\_配置**](ndis-status-task-offload-current-config.md)

[OID\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)

 

 




