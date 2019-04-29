---
title: OID_GEN_TRANSPORT_HEADER_OFFSET
description: 作为一组 OID_GEN_TRANSPORT_HEADER_OFFSET OID 指示其他标头的特定传输发送和接收的数据包的大小。
ms.assetid: 00b00c5b-cdf3-4b87-8914-e87876c9ae23
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSPORT_HEADER_OFFSET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 56c52694a757b3eb5dbf37d4725e3151143603c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387890"
---
# <a name="oidgentransportheaderoffset"></a>OID\_GEN\_传输\_标头\_偏移量


作为一组 OID\_GEN\_传输\_标头\_偏移量 OID 指示的其他标头的特定传输发送和接收的数据包大小。

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

传输通知微型端口驱动程序和此标头大小; 其他分层驱动程序处理数据包时，这些驱动程序然后可以使用此信息。 例如，驱动程序可以使用子层标头大小从传输中获取要在数据包，如 IP 标头; 开始中查找的更高的层信息开头驱动程序无法然后分析并调整为适当的 IP 协议标头的字段。 传输使用的传输\_标头\_偏移量定义，如下所示，以指示此标头大小的结构。

```C++
typedef struct _TRANSPORT_HEADER_OFFSET {
  USHORT  ProtocolType; 
  USHORT  HeaderOffset; 
} TRANSPORT_HEADER_OFFSET, *PTRANSPORT_HEADER_OFFSET;
```

此结构的成员包含下列信息：

<a href="" id="protocoltype"></a>**ProtocolType**  
指定的协议类型，用于发送此 OID 和，随后发送和接收数据包使用指定的子层标头大小。 协议为下列值之一：

<a href="" id="ndis-protocol-id-default"></a>NDIS\_协议\_ID\_默认  
默认协议

<a href="" id="ndis-protocol-id-tcp-ip"></a>NDIS\_协议\_ID\_TCP\_IP  
TCP/IP 协议

<a href="" id="ndis-protocol-id-ipx"></a>NDIS\_协议\_ID\_IPX  
NetWare IPX 协议

<a href="" id="ndis-protocol-id-nbf"></a>NDIS\_PROTOCOL\_ID\_NBF  
NetBIOS 协议

<a href="" id="headeroffset"></a>**HeaderOffset**  
指定的大小，以字节为单位的子层标头之前的协议，随后将发送到或从微型端口驱动程序或其他分层驱动程序中接收的数据包的协议标头。 例如，sizeof （以太网标头） + sizeof （标头中管理单元）。

通常情况下，传输计算中的微型端口驱动程序检索到的信息的数据包的标头大小。 若要请求的最大总数据包大小 （字节） NIC 支持，包括标头，传输使用[OID\_代\_最大\_总\_大小](oid-gen-maximum-total-size.md)OID。 若要请求以字节为单位的 NIC 支持的最大数据包大小，不包括标头，传输使用[OID\_代\_最大\_帧\_大小](oid-gen-maximum-frame-size.md)OID。 若要计算的最大标头大小，传输中减去最大总大小的最大帧的大小。

如果传输传输包含子层标头信息的数据包，传输协议必须知道这些数据包的子层标头大小，以及必须告知基础微型端口驱动程序和其他分层驱动程序的大小，以便将驱动程序可以处理数据包。 发送和接收数据包中的特定子层标头信息可能是一个可以为特定协议的注册表中设置的选项。 传输无法从注册表获得有关子层标头信息，然后传递到微型端口驱动程序的标头大小或其他分层驱动程序。

例如，如果传输处理来自光纤分布式数据接口中的数据包，传输必须发送 set 请求基础的微型端口驱动程序和其他分层驱动程序使用了 OID\_GEN\_传输\_标头\_偏移量来向这些驱动程序有关的数据包的子层标头的大小。 （FDDI 不是支持在 Windows Vista 和更高版本的 Windows 中。）FDDI 从这些数据包可能包含逻辑链接控件 (LLC) 信息。 此 LLC 信息又包括 LLC 标头和其他标头如子网访问协议 （快照）。 传输从注册表确定要使用 LLC/管理单元，并将数据包的管理单元 LLC/段的标头大小传递给微型端口驱动程序。

此 OID 是可选的微型端口驱动程序和其他分层驱动程序。 因为此 OID 是可选的则驱动程序不需要响应会使用此 OID 的品牌将传输的请求。

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


[OID\_GEN\_MAXIMUM\_FRAME\_SIZE](oid-gen-maximum-frame-size.md)

[OID\_GEN\_MAXIMUM\_TOTAL\_SIZE](oid-gen-maximum-total-size.md)

 

 




