---
title: NDIS_STATUS_NETWORK_CHANGE
description: NDIS_STATUS_NETWORK_CHANGE 状态指示网络更改为允许过量驱动程序启动的网络地址的重新协商。
ms.assetid: feb6bb71-7147-43dd-b09d-cb41404164eb
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 93867577d2a2ec73afe379040c4f05334103bff3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567314"
---
# <a name="ndisstatusnetworkchange"></a>NDIS\_状态\_网络\_更改


NDIS\_状态\_网络\_更改状态指示网络更改为允许过量驱动程序启动的网络地址的重新协商。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序可以生成此状态指示请求的基础协议驱动程序以重新协商层三个地址。

NDIS 生成 NDIS\_状态\_网络\_更改状态指示对较旧的 802.1 X 无线模拟 802.3 的微型端口驱动程序。 这些微型端口驱动程序报告的媒体类型**NdisMedium802\_3**和物理媒体类型**NdisPhysicalMediumWirelessLan**。 当生成这样的微型端口驱动程序[ **NDIS\_状态\_媒体\_CONNECT** ](ndis-status-media-connect.md)状态指示和关联的微型端口适配器是在连接状态，NDIS 生成 NDIS\_状态\_网络\_微型端口适配器更改状态指示。

NDIS 6.0 和更高版本的微型端口驱动程序应生成 NDIS\_状态\_网络\_更改状态指示后准备好处理网络数据。 例如，在本机 802.11 后成功完成身份验证和完整的层的两个连接完成，则生成此状态指示。

**请注意**  媒体连接状态的定义不准确地说，尽管此状态可以松散定义为的微型端口适配器能够发送和接收网络数据的状态。 媒体连接不直接相关链接身份验证状态。 本机 WiFi 802.3 接口不能发送或接收数据包之前，该链接进行身份验证后。 在这种情况下，媒体连接状态中本机 802.11 是链接进行身份验证状态与重合。

 

NDIS 会提供一个以下 NDIS\_网络\_更改\_中的值类型**StatusBuffer**隶属[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构：

<a href="" id="ndispossiblenetworkchange"></a>**NdisPossibleNetworkChange**  
微型端口驱动程序检测到可能存在网络更改。 在这种情况下，覆盖协议必须检测到网络更改，如果有，并重新协商地址，如有必要。

NDIS 还使用此值时生成 NDIS\_状态\_网络\_更改状态指示对较旧的 802.1 X 无线模拟 802.3 的微型端口驱动程序。 但是，使用 NDIS **NdisNetworkChangeFromMediaConnect**而不是**NdisPossibleNetworkChange**时它将转换相同事件的 Windows Management Instrumentation (WMI)。

<a href="" id="ndisdefinitelynetworkchange"></a>**NdisDefinitelyNetworkChange**  
微型端口驱动程序检测到有网络更改，以便覆盖协议必须重新协商地址。

<a href="" id="ndisnetworkchangefrommediaconnect"></a>**NdisNetworkChangeFromMediaConnect**  
较旧 802.1x 无线的微型端口驱动程序，它模拟生成 802.3 [ **NDIS\_状态\_媒体\_CONNECT** ](ndis-status-media-connect.md)状态指示在时连接的状态。 使用此值中的 WMI 事件通知[GUID\_NDIS\_状态\_网络\_更改](https://msdn.microsoft.com/library/windows/hardware/ff553595)。 **NdisNetworkChangeFromMediaConnect**不使用在 NDIS\_状态\_网络\_更改状态指示。

**StatusBufferSize**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构设置为 sizeof (NDIS\_网络\_更改\_类型)。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状态\_媒体\_连接**](ndis-status-media-connect.md)

 

 




