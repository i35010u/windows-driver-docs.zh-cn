---
title: NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: MUX 中间驱动程序使用 NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 功能状态指示通知 NDIS 和过量驱动程序，基础硬件的连接卸载特性发生了变化.
ms.assetid: 694cc0c4-0987-4095-8490-14ddfc9eaedb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fb3399d76ad54d860701a07ea1427e507fa538e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843508"
---
# <a name="ndis_status_tcp_connection_offload_hardware_capabilities"></a>\_TCP\_连接\_卸载\_硬件\_功能的 NDIS\_状态


MUX 中间驱动程序使用 NDIS\_状态\_TCP\_连接\_卸载\_硬件\_功能状态指示，通知 NDIS 和过量驱动程序已在基础硬件的连接卸载特性。

<a name="remarks"></a>备注
-------

如果添加或删除了基础 NIC，则与 MUX 中间驱动程序相关联的一组硬件功能可能会改变。

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含一个[**ndis\_TCP\_连接\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。 \_卸载的 NDIS\_TCP\_连接指定任务卸载硬件功能。

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


[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[ **\_卸载的 NDIS\_TCP\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

[OID\_TCP\_连接\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)

 

 




