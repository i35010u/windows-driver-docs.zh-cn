---
title: OID_GEN_MEDIA_SUPPORTED
description: 作为查询，OID_GEN_MEDIA_SUPPORTED OID 指定了 NIC 可支持的媒体类型，但不一定是 NIC 当前使用的媒体类型。
ms.assetid: e7b8d2b1-4e84-416f-aeb3-75591ed44b22
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_SUPPORTED 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5a5f3f54eed66f8762b8e051a5d558f6486e2092
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843131"
---
# <a name="oid_gen_media_supported"></a>支持 OID\_GEN\_介质\_


作为查询，OID\_代\_媒体\_支持的 OID 指定了 NIC 可支持的媒体类型，但不一定是 NIC 当前使用的媒体类型。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
已过时。

为 NDIS 6.0 和更高版本的驱动程序添加了以下介质类型：

-   **NdisMediumTunnel**

-   **NdisMediumLoopback**

-   **NdisMediumNative802\_11**

为 NDIS 6.20 和更高版本的驱动程序添加了以下介质类型：

-   **NdisMediumIP**

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需. 请参阅[支持 OID\_GEN\_支持的媒体\_（NDIS 5.1）](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560254(v=vs.85))。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需. 请参阅[支持 OID\_GEN\_支持的媒体\_（NDIS 5.1）](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560254(v=vs.85))。

<a name="remarks"></a>备注
-------

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 使用小型端口驱动程序在初始化期间提供的缓存值处理此 OID。

这些媒体类型作为以下系统定义的值的正确子集列出：

<a href="" id="ndismedium802-3"></a>**NdisMedium802\_3**  
以太网（802.3）。

**请注意**  NDIS 5。符合802.11 接口的*x*微型端口驱动程序必须使用这种媒体类型。 有关802.11 接口的详细信息，请参阅[802.11 无线 LAN 微型端口驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff543933(v=vs.85))。

 

<a href="" id="ndismedium802-5"></a>**NdisMedium802\_5**  
令牌环（802.5）。 对于 NDIS 6.0 和更高版本的驱动程序，此媒体类型不受支持。

**注意**  从 Windows 8 开始，操作系统将不支持任何微型端口驱动程序的此媒体类型。

 

<a href="" id="ndismediumfddi"></a>**NdisMediumFddi**  
FDDI. Windows Vista 和更高版本的 Windows 不支持此媒体类型。

<a href="" id="ndismediumwan"></a>**NdisMediumWan**  
WAN

<a href="" id="ndismediumlocaltalk"></a>**NdisMediumLocalTalk**  
LocalTalk

<a href="" id="ndismediumdix"></a>**NdisMediumDix**  
DEC/Intel/Xerox （DIX）以太网

<a href="" id="ndismediumarcnetraw"></a>**NdisMediumArcnetRaw**  
ARCNET （原始）。 Windows Vista 和更高版本的 Windows 不支持此媒体类型。

<a href="" id="ndismediumarcnet878-2"></a>**NdisMediumArcnet878\_2**  
ARCNET （878.2）。 Windows Vista 和更高版本的 Windows 不支持此媒体类型。

<a href="" id="ndismediumatm"></a>**NdisMediumAtm**  
ATM. 对于 NDIS 6.0 和更高版本的驱动程序，此媒体类型不受支持。

<a href="" id="ndismediumnative802-11"></a>**NdisMediumNative802\_11**  
本机802.11。 此媒体类型由符合本机802.11 接口的微型端口驱动程序使用。 有关此接口的详细信息，请参阅[本机802.11 无线 LAN 微型端口驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff560648(v=vs.85))。

<a href="" id="ndismediumwirelesswan"></a>**NdisMediumWirelessWan**  
各种类型的 **NdisWireless * * * Xxx*媒体。 此媒体类型不能从 Windows Vista 和更高版本的 Windows 开始使用。

<a href="" id="ndismediumirda"></a>**NdisMediumIrda**  
红外（IrDA）。

<a href="" id="ndismediumcowan"></a>**NdisMediumCoWan**  
面向连接的 WAN。

<a href="" id="ndismedium1394"></a>**NdisMedium1394**  
IEEE 1394 （firewire）总线。 Windows Vista 和更高版本的 Windows 不支持此媒体类型。

<a href="" id="ndismediumbpc"></a>**NdisMediumBpc**  
广播 PC 网络。

<a href="" id="ndismediuminfiniband"></a>**NdisMediumInfiniBand**  
无限网络。

<a href="" id="ndismediumtunnel"></a>**NdisMediumTunnel**  
隧道网络。

<a href="" id="ndismediumloopback"></a>**NdisMediumLoopback**  
NDIS 环回网络。

<a href="" id="ndismediumip"></a>**NdisMediumIP**  
能够发送和接收原始 IP 数据包的通用介质。

NDIS 5。 支持无线 LAN （WLAN）或无线 WAN （WWAN）数据包的*x*微型端口驱动程序显示在操作系统上，并以以太网数据包形式出现。 这些 NDIS 驱动程序必须为 WWAN 或 WLAN 网络提供对以太网网络的支持。 此类驱动程序将其 "NdisMedium802" 声明为 " **\_** "，并将以太网模拟到更高级别的 NDIS 驱动程序。 此类驱动程序还必须在 OID 中声明[\_代\_物理\_中型](oid-gen-physical-medium.md)提供支持的适当物理介质。

有关 NDIS 1.x WLAN 微型端口驱动程序的详细信息，请参阅[802.11 无线 LAN 微型端口驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff543933(v=vs.85))。

NDIS 6.0 和更高版本的微型端口驱动程序，支持显示到操作系统中的 WLAN 媒体传输数据包，以及作为 IEEE 802.11 数据包的 NDIS。 这些 NDIS 驱动程序必须提供 WLAN 网络支持作为本机802.11 微型端口驱动程序。 此类驱动程序将其媒体声明为**NdisMediumNative802\_11**。

有关本机802.11 微型端口驱动程序的详细信息，请参阅[本机802.11 无线 LAN 微型端口驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff560648(v=vs.85))。

如果基础微型端口驱动程序为此查询返回**NULL** ，或者如果使用的是实验媒体类型，则驱动程序必须使用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数指示接收操作。 绑定到此类基础微型端口驱动程序的任何协议都会接收所有此类指示，也就是说，协议驱动程序无法使用 OID 筛选接收操作[\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)

[OID\_GEN\_物理\_中型](oid-gen-physical-medium.md)

 

 




