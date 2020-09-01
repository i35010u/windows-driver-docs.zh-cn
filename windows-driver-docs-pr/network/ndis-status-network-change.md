---
title: NDIS_STATUS_NETWORK_CHANGE
description: "\"NDIS_STATUS_NETWORK_CHANGE 状态\" 指示网络更改，以允许过量驱动程序启动网络地址的重新协商。"
ms.assetid: feb6bb71-7147-43dd-b09d-cb41404164eb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 047cb2dac3f75887533de34a476a63bbe0614dd2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214704"
---
# <a name="ndis_status_network_change"></a>NDIS \_ 状态 \_ 网络 \_ 更改


NDIS \_ 状态 \_ 网络 \_ 更改状态指示网络更改，以允许过量驱动程序启动网络地址的重新协商。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序可以生成此状态指示，请求过量的协议驱动程序以重新协商层三个地址。

NDIS \_ \_ \_ 为模拟802.3 的旧版 802.1 x 无线微型端口驱动程序生成 ndis 状态网络更改状态指示。 这些微型端口驱动程序报告媒体类型为 **NdisMedium802 \_ 3** ，物理媒体类型为 **NdisPhysicalMediumWirelessLan**。 当这样的微型端口驱动程序生成 [**NDIS \_ 状态 \_ 媒体 \_ 连接**](ndis-status-media-connect.md) 状态指示并且关联的微型端口适配器处于连接状态时，ndis 将 \_ \_ 为微型端口适配器生成 ndis 状态网络 \_ 更改状态指示。

\_ \_ 只有在准备好处理网络数据后，ndis 6.0 和更高版本的微型端口驱动程序才应生成 ndis 状态网络 \_ 更改状态指示。 例如，在本机802.11 中，此状态指示在成功完成身份验证并实现完全第2层连接后生成。

**注意**   尽管媒体连接状态不是精确定义的，但这种状态可以是松散定义的，即微型端口适配器能够传输和接收网络数据的状态。 媒体连接与链接身份验证状态无关。 在对链接进行身份验证之前，本机 WiFi 802.3 接口无法发送或接收数据包。 在这种情况下，媒体连接状态与本机802.11 中的链接身份验证状态一致。

 

NDIS \_ \_ \_ 在[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员中提供以下 ndis 网络更改类型值之一：

<a href="" id="ndispossiblenetworkchange"></a>**NdisPossibleNetworkChange**  
微型端口驱动程序检测到可能存在网络更改。 在这种情况下，过量协议必须检测网络更改（如果有），并在必要时重新协商地址。

如果 \_ \_ \_ 为模拟802.3 的旧版 802.1 x 无线微型端口驱动程序生成 ndis 状态网络更改状态指示，NDIS 还会使用此值。 但是，在为 Windows Management Instrumentation (WMI) 转换相同事件时，NDIS 将使用 **NdisNetworkChangeFromMediaConnect** 而不是 **NdisPossibleNetworkChange** 。

<a href="" id="ndisdefinitelynetworkchange"></a>**NdisDefinitelyNetworkChange**  
微型端口驱动程序检测到存在网络更改，因此过量协议必须重新协商地址。

<a href="" id="ndisnetworkchangefrommediaconnect"></a>**NdisNetworkChangeFromMediaConnect**  
模拟802.3 的老式 802.1 X 无线微型端口驱动程序在处于连接状态时生成了 [**NDIS \_ 状态 \_ 媒体 \_ 连接**](ndis-status-media-connect.md) 状态指示。 此值用于 WMI 事件通知中的 [GUID \_ NDIS \_ 状态 \_ 网络 \_ 更改](./guid-ndis-status-network-change.md)。 **NdisNetworkChangeFromMediaConnect** 未在 NDIS \_ 状态 \_ 网络 \_ 更改状态指示中使用。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBufferSize**成员设置为 sizeof (NDIS \_ 网络 \_ 更改 \_ 类型) 。

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


[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ 状态 \_ 媒体 \_ 连接**](ndis-status-media-connect.md)

 

