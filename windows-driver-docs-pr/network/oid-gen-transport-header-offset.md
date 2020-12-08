---
title: OID_GEN_TRANSPORT_HEADER_OFFSET
description: 作为集，OID_GEN_TRANSPORT_HEADER_OFFSET OID 指示特定传输发送和接收的数据包的附加标头的大小。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSPORT_HEADER_OFFSET 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a1670a788212471b836facc1d7c9fd92addde3b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822873"
---
# <a name="oid_gen_transport_header_offset"></a>OID \_ 生成 \_ 传输 \_ 标头 \_ 偏移


作为集，OID 生成 \_ \_ 传输 \_ 标头的 \_ 偏移量 oid 表示特定传输发送和接收的数据包的附加标头的大小。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a name="remarks"></a>备注
-------

传输通知微型端口驱动程序和此标头大小的其他分层驱动程序;然后，这些驱动程序可以在处理数据包时使用此信息。 例如，驱动程序可以使用从传输中获得的子层标头大小来查找数据包中较高层信息的开头，例如 IP 标头的开头;然后，该驱动程序可以根据需要分析和调整 IP 协议标头的字段。 传输使用 \_ 如下定义的传输标头 \_ 偏移结构来指示此标头大小。

```C++
typedef struct _TRANSPORT_HEADER_OFFSET {
  USHORT  ProtocolType; 
  USHORT  HeaderOffset; 
} TRANSPORT_HEADER_OFFSET, *PTRANSPORT_HEADER_OFFSET;
```

此结构的成员包含以下信息：

<a href="" id="protocoltype"></a>**ProtocolType**  
指定发送此 OID 并随后使用指定的子层标头大小发送和接收数据包的协议类型。 协议为以下值之一：

<a href="" id="ndis-protocol-id-default"></a>NDIS \_ 协议 \_ ID \_ 默认值  
默认协议

<a href="" id="ndis-protocol-id-tcp-ip"></a>NDIS \_ 协议 \_ ID \_ TCP \_ IP  
TCP/IP 协议

<a href="" id="ndis-protocol-id-ipx"></a>NDIS \_ 协议 \_ ID \_ IPX  
NetWare IPX 协议

<a href="" id="ndis-protocol-id-nbf"></a>NDIS \_ 协议 \_ ID \_ NBF  
NetBIOS 协议

<a href="" id="headeroffset"></a>**HeaderOffset**  
指定在协议标头之前的子层标头的大小（以字节为单位），该协议随后将发送到或从微型端口驱动程序或其他分层驱动程序接收或接收的数据包。 例如，sizeof (以太网标头) + sizeof (SNAP 标头) 。

通常，传输会根据从小型端口驱动程序检索的信息计算数据包的标头大小。 若要请求 NIC 支持的最大数据包总大小（以字节为单位），包括标头，传输使用 [oid \_ GEN \_ 最大 \_ 总 \_ 大小](oid-gen-maximum-total-size.md) oid。 若要请求 NIC 支持的最大数据包大小（以字节为单位）（不包括标头），传输使用 [oid \_ GEN \_ 最大 \_ 帧 \_ 大小](oid-gen-maximum-frame-size.md) oid。 为了计算最大标头大小，传输将从最大总大小中减去最大帧大小。

如果传输传输包含子层标头信息的数据包，则传输必须知道这些数据包的子层标头大小，并必须通知底层微型端口驱动程序和其他有关大小的分层驱动程序，以便驱动程序可以处理这些数据包。 在数据包中发送和接收特定子层标头信息可能是可以在注册表中为特定协议设置的选项。 然后，传输可能会从注册表获取有关子层标头的信息，并将标头大小向下传递到微型端口驱动程序或其他分层驱动程序。

例如，如果某个传输处理来自光纤分布式数据接口中型的数据包，则传输必须使用 OID 生成传输标头偏移量将一个 set 请求发送到基础微型端口驱动程序和其他分层驱动程序， \_ \_ \_ \_ 以通知这些驱动程序有关数据包的子层标头的大小。 Windows Vista 和更高版本的 Windows 不支持 (FDDI。 ) 来自 FDDI 的这些数据包可能包含 (LLC) 信息的逻辑链接控制。 此 LLC 信息可将 LLC 标头和其他标头（例如 Sub-Network 访问协议 (SNAP) ）包括在内。 传输从注册表确定使用 LLC/SNAP，并将数据包的 LLC/SNAP 段大小传递给微型端口驱动程序。

此 OID 对于微型端口驱动程序和其他分层驱动程序是可选的。 由于此 OID 是可选的，因此，驱动程序不需要响应使用此 OID 传输的请求。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ GEN \_ 最大 \_ 帧 \_ 大小](oid-gen-maximum-frame-size.md)

[OID \_ GEN \_ 最大 \_ 总 \_ 大小](oid-gen-maximum-total-size.md)

 

 




