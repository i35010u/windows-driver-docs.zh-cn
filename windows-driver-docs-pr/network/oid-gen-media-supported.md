---
title: OID_GEN_MEDIA_SUPPORTED
description: 为查询，OID_GEN_MEDIA_SUPPORTED OID 指定 NIC 可以支持的媒体类型，但不是一定 NIC 当前使用的媒体类型。
ms.assetid: e7b8d2b1-4e84-416f-aeb3-75591ed44b22
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_SUPPORTED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b121850c66dc8990be0701c6e5d5dd05d33ea0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563693"
---
# <a name="oidgenmediasupported"></a>OID\_GEN\_媒体\_支持


为查询，OID\_GEN\_媒体\_支持 OID 指定 NIC 可以支持的媒体类型，但不是一定 NIC 当前使用的媒体类型。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
已过时。

NDIS 6.0 和更高版本的驱动程序添加以下媒体类型：

-   **NdisMediumTunnel**

-   **NdisMediumLoopback**

-   **NdisMediumNative802\_11**

NDIS 6.20 和更高版本的驱动程序添加以下媒体类型：

-   **NdisMediumIP**

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。 请参阅[OID\_代\_媒体\_支持 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff560254)。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。 请参阅[OID\_代\_媒体\_支持 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff560254)。

<a name="remarks"></a>备注
-------

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 处理此 OID 微型端口驱动程序在初始化过程中提供的缓存值。

为以下系统定义的值的正确子集列出了这些媒体类型：

<a href="" id="ndismedium802-3"></a>**NdisMedium802\_3**  
以太网 (802.3)。

**请注意**  NDIS 5。*x*符合 802.11 接口的微型端口驱动程序必须使用此媒体类型。 802.11 接口的详细信息，请参阅[802.11 无线 LAN 微端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff543933)。

 

<a href="" id="ndismedium802-5"></a>**NdisMedium802\_5**  
令牌环 (802.5)。 NDIS 6.0 和更高版本的驱动程序不支持此媒体类型。

**请注意**  从 Windows 8 开始，操作系统将不支持此媒体类型的任何微型端口驱动程序。

 

<a href="" id="ndismediumfddi"></a>**NdisMediumFddi**  
FDDI。 在 Windows Vista 和更高版本的 Windows 上不支持此媒体类型。

<a href="" id="ndismediumwan"></a>**NdisMediumWan**  
WAN

<a href="" id="ndismediumlocaltalk"></a>**NdisMediumLocalTalk**  
LocalTalk

<a href="" id="ndismediumdix"></a>**NdisMediumDix**  
DEC/Intel Xerox (DIX) 以太网

<a href="" id="ndismediumarcnetraw"></a>**NdisMediumArcnetRaw**  
ARCNET （原始）。 在 Windows Vista 和更高版本的 Windows 上不支持此媒体类型。

<a href="" id="ndismediumarcnet878-2"></a>**NdisMediumArcnet878\_2**  
ARCNET (878.2)。 在 Windows Vista 和更高版本的 Windows 上不支持此媒体类型。

<a href="" id="ndismediumatm"></a>**NdisMediumAtm**  
ATM。 NDIS 6.0 和更高版本的驱动程序不支持此媒体类型。

<a href="" id="ndismediumnative802-11"></a>**NdisMediumNative802\_11**  
本机 802.11。 本机 802.11 接口符合的微型端口驱动程序使用此媒体类型。 有关此接口的详细信息，请参阅[本机 802.11 无线 LAN 微端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff560648)。

<a href="" id="ndismediumwirelesswan"></a>**NdisMediumWirelessWan**  
各种类型的 **NdisWireless * * * Xxx*媒体。 此媒体类型不是适用于使用开头的 Windows Vista 和更高版本的 Windows。

<a href="" id="ndismediumirda"></a>**NdisMediumIrda**  
红外 (IrDA)。

<a href="" id="ndismediumcowan"></a>**NdisMediumCoWan**  
面向连接的 WAN。

<a href="" id="ndismedium1394"></a>**NdisMedium1394**  
IEEE 1394 (firewire) 总线。 在 Windows Vista 和更高版本的 Windows 上不支持此媒体类型。

<a href="" id="ndismediumbpc"></a>**NdisMediumBpc**  
PC 网络广播。

<a href="" id="ndismediuminfiniband"></a>**NdisMediumInfiniBand**  
InfiniBand 网络。

<a href="" id="ndismediumtunnel"></a>**NdisMediumTunnel**  
隧道网络。

<a href="" id="ndismediumloopback"></a>**NdisMediumLoopback**  
NDIS 环回网络。

<a href="" id="ndismediumip"></a>**NdisMediumIP**  
泛型的人士能够发送和接收原始 IP 数据包。

NDIS 5。 *x*支持无线 LAN (WLAN) 或无线广域网 (WWAN) 数据包的微型端口驱动程序出现对操作系统和 NDIS 作为以太网数据包。 这些 NDIS 驱动程序必须为以太网网络的 WWAN 或 WLAN 的网络提供支持。 此类驱动程序声明为其中等**NdisMedium802\_3**和模拟以太网更高级别的的 NDIS 驱动程序。 此类驱动程序还必须在声明[OID\_代\_物理\_中等](oid-gen-physical-medium.md)它们支持的相应物理介质...

详细了解 NDIS 5.X WLAN 微型端口驱动程序，请参阅[802.11 无线 LAN 微端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff543933)。

NDIS 6.0 和更高版本支持 WLAN 媒体的微型端口驱动程序传输到操作系统和 NDIS 以 IEEE 802.11 数据包的形式显示的数据包。 作为本机 802.11 微型端口驱动程序，这些 NDIS 驱动程序必须为 WLAN 网络提供支持。 此类驱动程序声明为其中等**NdisMediumNative802\_11**。

有关本机 802.11 微型端口驱动程序的详细信息，请参阅[本机 802.11 无线 LAN 微端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff560648)。

如果基础微型端口驱动程序将返回**NULL**对于此查询，或如果使用实验性的媒体类型，该驱动程序必须指示接收操作使用[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数。 绑定到此类基础微型端口驱动程序的任何协议接收所有此类指示，即筛选协议驱动程序不能接收操作与[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)

[OID\_GEN\_CURRENT\_PACKET\_FILTER](oid-gen-current-packet-filter.md)

[OID\_GEN\_PHYSICAL\_MEDIUM](oid-gen-physical-medium.md)

 

 




