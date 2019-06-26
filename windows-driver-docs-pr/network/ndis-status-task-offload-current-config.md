---
title: NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 状态指示通知发生了更改任务卸载的 NIC 配置 NDIS 和基础驱动程序
ms.assetid: 8a098dff-409e-4168-a3aa-372851aa999d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d496e929fabc15bba6621f9092c8b348aea7c3d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372577"
---
# <a name="ndisstatustaskoffloadcurrentconfig"></a>NDIS\_状态\_任务\_卸载\_当前\_配置


微型端口驱动程序使用**NDIS\_状态\_任务\_卸载\_当前\_配置**状态指示通知 NDIS 和已有的基础驱动程序更改任务卸载配置中的 nic。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须报告与当前 capabilities **NDIS\_状态\_任务\_卸载\_当前\_配置**状态指示当前记录功能更改。 此状态指示可确保所有基础协议驱动程序使用新的功能信息更新。 微型端口驱动程序需要发出此状态指示在以下情况下：

1.  当微型端口驱动程序收到[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)集请求，它必须使用的内容[ **NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构，以更新当前已启用任务卸载功能。
2.  当微型端口驱动程序收到[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)集请求，它必须使用的内容[ **NDIS\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)结构，以更新当前已启用任务卸载功能。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。 在发出**NDIS\_状态\_任务\_卸载\_当前\_配置**微型端口驱动程序必须使用状态指示**NDIS\_卸载**到当前任务卸载的 NIC 配置的报表的结构

**请注意**  的内容[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构反映仅 NIC 的当前任务卸载配置中，不是其实际硬件功能。

 

有关当前任务卸载配置的详细信息，请参阅[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)。

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

[**NDIS\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)

[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状态\_任务\_卸载\_硬件\_功能**](ndis-status-task-offload-hardware-capabilities.md)

[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)

[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)

[OID\_TCP\_OFFLOAD\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)

 

 




