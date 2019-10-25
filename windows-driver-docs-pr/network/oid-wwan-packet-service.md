---
title: OID_WWAN_PACKET_SERVICE
description: OID_WWAN_PACKET_SERVICE 用于指示微型端口驱动程序在当前的已注册提供程序的网络上执行数据包服务附加/分离操作，同时用于基于 GSM 和基于 CDMA 的 MB 设备。
ms.assetid: 97bb9324-8052-437c-baa5-fb9a8176c779
ms.date: 04/04/2019
keywords: -从 Windows Vista 开始 OID_WWAN_PACKET_SERVICE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ee44aacaab4fdae455f57036c0171e975ff1fa31
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843824"
---
# <a name="oid_wwan_packet_service"></a>OID\_WWAN\_数据包\_服务


OID\_WWAN\_数据包\_服务用于指示微型端口驱动程序在当前的已注册提供程序的网络上执行数据包服务附加/分离操作，同时用于基于 GSM 和基于 CDMA 的 MB 设备。 除了数据包服务附加/分离状态外，此 OID 还用于确定数据类可用性和当前使用的数据类信息。

微型端口驱动程序必须异步处理集和查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后将[**ndis\_状态\_WWAN\_数据包发送\_服务**](ndis-status-wwan-packet-service.md)状态通知，包含[**NDIS\_WWAN\_数据包\_服务\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)结构，以提供有关当前数据包服务状态的信息，而不考虑完成的集或查询请求.

请求设置当前数据包服务状态的调用方提供[**NDIS\_WWAN\_使用适当的信息将\_数据包\_服务结构设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service)为微型端口驱动程序。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 数据包服务附加操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-service-attach-operations)。

当处理查询或设置操作时，微型端口驱动程序可以访问提供程序网络，但不应访问订阅服务器标识模块（SIM 卡）。

如果可能，基于 CDMA 的设备应使用此项作为释放网络资源分配的机会。

某些 SIM 卡使 MB 设备只能在数据包域上注册，而不是在线路交换机域上注册。 数据调用结束后，VAN UI 将\_WWAN\_数据包\_服务设置请求发送 OID，以分离数据包服务。 这会导致 MB 设备从数据包域中分离。 MB 设备从网络中注销并进入省电模式。 因此，设备将从 VAN UI 中消失，因为已取消注册，并且只能通过重新启动来恢复。 在这种情况下，微型端口驱动程序应该通过返回正值来欺骗数据包附加/分离操作，而无需将 MB 设备设置为这种模式。

对于不支持数据包附加的技术，微型端口驱动程序应欺骗附加状态，以让 MB 服务知道可以继续上下文激活。 小型端口驱动程序还应在微型端口驱动程序中欺骗\_WWAN\_数据包\_服务请求的设置 OID。 小型端口驱动程序应将[**NDIS\_状态发送\_WWAN\_数据包\_** ](ndis-status-wwan-packet-service.md)用于查询操作的服务通知以及未经请求的事件。 如果设备数据包服务状态未设置为*WwanPacketServiceStateAttached*，则微型端口驱动程序应无法通过 PDP 激活。

在数据包服务状态达到*WwanPacketServiceStateAttached*之前，MB 服务不应继续进行上下文激活。

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

从 Windows 10 版本1903开始，支持此 OID 的新修订版本2。 此扩展使宿主能够查询调制解调器当前在5G 中的操作频率范围。

宿主随时可以查询扩展数据包服务状态信息。 响应与修订版本1相同，不同之处在于修订版本2具有两个新字段。

如果在5G 域中注册了该调制解调器，它将返回该运营商的5G 频率范围。 如果存在多个5G 电信公司，则返回所有有效范围。

有关5G 数据类支持的详细信息，请参阅[MB 5G 数据类支持](mb-5g-data-class-support.md)。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_设置\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service)

[**WWAN\_数据包\_服务\_的 NDIS\_状态**](ndis-status-wwan-packet-service.md)

[WWAN 数据包服务附加操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-service-attach-operations)

 

 




