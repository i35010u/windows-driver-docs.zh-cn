---
title: NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES
description: NDIS 微型端口驱动程序和 MUX 中间驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 状态指示，通知 NDIS 和过量驱动程序已更改基础 NIC 的任务卸载硬件功能。
ms.assetid: 9ac8f4c9-66f4-4889-932b-a51381c54734
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b3f6a6d69cfd53cb06a526615391c6be89acb72e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843506"
---
# <a name="ndis_status_task_offload_hardware_capabilities"></a>\_任务\_卸载\_硬件\_功能的 NDIS\_状态


NDIS 微型端口驱动程序和 MUX 中间驱动程序使用**ndis\_状态\_任务\_卸载\_硬件\_功能**状态指示，通知 NDIS 和过量驱动程序已在任务中更改卸载基础 NIC 的硬件功能。

<a name="remarks"></a>备注
-------

如果添加或删除了基础 NIC，则与微型端口驱动程序或 MUX 中间驱动程序相关联的一组硬件功能可能会更改。 例如，如果微型端口驱动程序发出**NDIS\_状态\_任务\_卸载\_硬件\_功能**状态指示，将其指定为不支持大型发送卸载（LSO），则 NIC 将不再为配置为支持 LSO。

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。 此结构指定任务卸载硬件功能。

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
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[ **\_任务\_卸载\_当前\_配置的 NDIS\_状态**](ndis-status-task-offload-current-config.md)

[OID\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)

 

 




