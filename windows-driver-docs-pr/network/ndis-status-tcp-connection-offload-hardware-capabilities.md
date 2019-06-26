---
title: NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: MUX 中间驱动程序使用 NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 功能状态指示通知 NDIS 和基础驱动程序已在连接中的更改将卸载的基础硬件特征.
ms.assetid: 694cc0c4-0987-4095-8490-14ddfc9eaedb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c68abc8dc96ea9b6a9e8337c025a17d9f58d1570
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372570"
---
# <a name="ndisstatustcpconnectionoffloadhardwarecapabilities"></a>NDIS\_状态\_TCP\_连接\_卸载\_硬件\_功能


MUX 中间驱动程序使用 NDIS\_状态\_TCP\_连接\_卸载\_硬件\_功能功能状态指示通知 NDIS 和基础驱动程序已在基础硬件连接卸载特征中的更改。

<a name="remarks"></a>备注
-------

如果在添加或删除基础 NIC，可以更改与 MUX 中间驱动程序相关联的总体硬件功能集。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含[ **NDIS\_TCP\_连接\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。 NDIS\_TCP\_连接\_卸载指定任务卸载的硬件功能。

有关任务卸载硬件功能的详细信息，请参阅[OID\_TCP\_连接\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)。

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


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_TCP\_连接\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

[OID\_TCP\_连接\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)

 

 




