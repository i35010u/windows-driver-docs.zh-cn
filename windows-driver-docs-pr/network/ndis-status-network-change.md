---
title: NDIS_STATUS_NETWORK_CHANGE
description: "\"NDIS_STATUS_NETWORK_CHANGE 状态\" 指示网络更改，以允许过量驱动程序启动网络地址的重新协商。"
ms.assetid: feb6bb71-7147-43dd-b09d-cb41404164eb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 89616ed87053ec21377793efa7dffa6ce1a4baf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842785"
---
# <a name="ndis_status_network_change"></a>\_网络\_更改的 NDIS\_状态


\_网络\_更改状态的 NDIS\_状态指示网络更改，以允许过量驱动程序启动网络地址的重新协商。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序可以生成此状态指示，请求过量的协议驱动程序以重新协商层三个地址。

NDIS\_状态\_网络\_更改模拟802.3 的旧版 802.1 X 无线微型端口驱动程序的状态指示来生成 NDIS 状态。 这些微型端口驱动程序报告 **\_NdisMedium802**为**NdisPhysicalMediumWirelessLan**的媒体类型。 当这样的微型端口驱动程序生成[**ndis\_状态时\_MEDIA\_连接**](ndis-status-media-connect.md)状态指示，并且关联的微型端口适配器处于连接状态，ndis 将为微型端口适配器生成 NDIS\_状态\_网络\_更改状态指示。

只有在已准备好处理网络数据后，NDIS 6.0 和更高版本的小型端口驱动程序才会\_网络\_更改状态指示生成 NDIS\_状态。 例如，在本机802.11 中，此状态指示在成功完成身份验证并实现完全第2层连接后生成。

**请注意**  虽然未准确定义媒体连接状态，但这种状态可以是松散定义的，即微型端口适配器能够传输和接收网络数据的状态。 媒体连接与链接身份验证状态无关。 在对链接进行身份验证之前，本机 WiFi 802.3 接口无法发送或接收数据包。 在这种情况下，媒体连接状态与本机802.11 中的链接身份验证状态一致。

 

NDIS 提供以下 NDIS\_的其中一种\_更改[**ndis\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)的**STATUSBUFFER**成员\_类型值\_指示结构：

<a href="" id="ndispossiblenetworkchange"></a>**NdisPossibleNetworkChange**  
微型端口驱动程序检测到可能存在网络更改。 在这种情况下，过量协议必须检测网络更改（如果有），并在必要时重新协商地址。

在为模拟802.3 的旧版 802.1 X 无线微型端口驱动程序生成 NDIS\_状态\_网络\_更改状态指示时，NDIS 还会使用此值。 但是，在为 Windows Management Instrumentation （WMI）转换相同事件时，NDIS 将使用**NdisNetworkChangeFromMediaConnect**而不是**NdisPossibleNetworkChange** 。

<a href="" id="ndisdefinitelynetworkchange"></a>**NdisDefinitelyNetworkChange**  
微型端口驱动程序检测到存在网络更改，因此过量协议必须重新协商地址。

<a href="" id="ndisnetworkchangefrommediaconnect"></a>**NdisNetworkChangeFromMediaConnect**  
模拟802.3 的老式 802.1 X 无线微型端口驱动程序在[ **\_媒体\_连接**](ndis-status-media-connect.md)状态时，生成了 NDIS\_状态。 此值用于 WMI 事件通知中的[GUID\_NDIS\_状态\_网络\_更改](https://docs.microsoft.com/windows-hardware/drivers/network/guid-ndis-status-network-change)。 **NdisNetworkChangeFromMediaConnect**未在 NDIS\_状态中使用\_网络\_更改状态指示。

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBufferSize**成员设置为 SIZEOF （NDIS\_网络\_更改\_类型）。

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

[ **\_媒体\_连接的 NDIS\_状态**](ndis-status-media-connect.md)

 

 




