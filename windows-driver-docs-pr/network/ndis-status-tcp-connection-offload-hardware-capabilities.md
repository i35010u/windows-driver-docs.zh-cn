---
title: NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: MUX 中间驱动程序使用 NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 功能状态指示，通知 NDIS 和过量驱动程序，基础硬件的连接卸载特性发生了更改。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e9a07752940f53a7c8052f7f8154a11e9d28ef5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837162"
---
# <a name="ndis_status_tcp_connection_offload_hardware_capabilities"></a>NDIS \_ 状态 \_ TCP \_ 连接 \_ 卸载 \_ 硬件 \_ 功能


MUX 中间驱动程序使用 NDIS \_ 状态 " \_ TCP \_ 连接 \_ 卸载 \_ 硬件功能" \_ 状态指示通知 NDIS 和过量驱动程序，基础硬件的连接卸载特性发生了更改。

<a name="remarks"></a>备注
-------

如果添加或删除了基础 NIC，则与 MUX 中间驱动程序相关联的一组硬件功能可能会改变。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含 [**ndis \_ TCP \_ 连接 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。 NDIS \_ TCP \_ 连接 \_ 卸载指定任务卸载硬件功能。

有关任务卸载硬件功能的详细信息，请参阅 [OID \_ TCP \_ 连接 \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-connection-offload-hardware-capabilities.md)。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ TCP \_ 连接 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

[OID \_ TCP \_ 连接 \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-connection-offload-hardware-capabilities.md)

 

