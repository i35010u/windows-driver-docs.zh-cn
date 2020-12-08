---
title: OID_WAN_CO_GET_STATS_INFO
description: OID_WAN_CO_GET_STATS_INFO OID 请求微型端口驱动程序返回特定于 (VC) 虚拟连接的统计信息。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_STATS_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ae7c36de8fc890af6507b365fbba9f0e19ea59a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838735"
---
# <a name="oid_wan_co_get_stats_info"></a>OID \_ WAN \_ CO \_ 获取 \_ 统计 \_ 信息


OID \_ WAN \_ CO \_ 获取 \_ 统计 \_ 信息 OID 请求微型端口驱动程序返回特定于虚拟连接 (VC) 的统计信息。 WAN 微型端口驱动程序应保留统计信息，并在 NDIS \_ WAN \_ CO 获取统计信息结构中为此 OID 返回这些统计信息 \_ \_ \_ ，如下所示：

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_STATS_INFO {
         OUT ULONG BytesSent;
         OUT ULONG BytesRcvd;
         OUT ULONG FramesSent;
         OUT ULONG FramesRcvd;
         OUT ULONG CRCErrors;
         OUT ULONG TimeoutErrors;
         OUT ULONG AlignmentErrors;
         OUT ULONG SerialOverrunErrors;
         OUT ULONG FramingErrors;
         OUT ULONG BufferOverrunErrors;
         OUT ULONG BytesTransmittedUncompressed;
         OUT ULONG BytesReceivedUncompressed;
         OUT ULONG BytesTransmittedCompressed;
         OUT ULONG BytesReceivedCompressed;
    } NDIS_WAN_CO_GET_STATS_INFO,   *PNDIS_WAN_CO_GET_STATS_INFO;
```




此结构的成员包含以下信息：

<a href="" id="bytessent"></a>**内 bytessent**  
指定传输的字节数。

<a href="" id="bytesrcvd"></a>**BytesRcvd**  
指定接收的字节数。

<a href="" id="framessent"></a>**FramesSent**  
指定) 发送 (WAN 数据包的帧数。

<a href="" id="framesrcvd"></a>**FramesRcvd**  
指定接收的帧数。

<a href="" id="crcerrors"></a>**CRCErrors**  
指定此 VC 遇到的 CRC 错误数。 CRC 错误是由循环冗余检查失败引起的。 CRC 错误表明收到的帧中的一个或多个字节在到达时出现乱码。

<a href="" id="timeouterrors"></a>**TimeoutErrors**  
指定此 VC 遇到的超时错误数。 如果未及时接收预期字节，则会出现超时错误。

<a href="" id="alignmenterrors"></a>**AlignmentErrors**  
指定此 VC 遇到的对齐错误数。 当接收的字节与预期的字节不同时，会发生对齐错误。 当某个字节丢失或出现超时错误时，通常会发生这种情况。

<a href="" id="serialoverrunerrors"></a>**SerialOverrunErrors**  
指定为此 VC 遇到的串行溢出数。 当 WAN NIC 无法处理接收数据的速率时，会发生串行超限。

<a href="" id="framingerrors"></a>**FramingErrors**  
指定此 VC 遇到的帧错误数。 当使用无效的开始或停止位接收到异步字节时，会发生组帧错误。

<a href="" id="bufferoverrunerrors"></a>**BufferOverrunErrors**  
指定为此 VC 遇到的缓冲区溢出数。 当 WAN 微型端口驱动程序无法处理接收数据的速率时，会发生缓冲区溢出。

<a href="" id="bytestransmitteduncompressed"></a>**BytesTransmittedUncompressed**  
指定传输的未压缩数据的字节数。 仅当微型端口驱动程序支持压缩时，它才返回非零值。

<a href="" id="bytesreceiveduncompressed"></a>**BytesReceivedUncompressed**  
指定收到的未压缩数据的字节数。 仅当微型端口驱动程序支持压缩时，它才返回非零值。

<a href="" id="bytestransmittedcompressed"></a>**BytesTransmittedCompressed**  
指定传输的压缩数据的字节数。 仅当微型端口驱动程序支持压缩时，它才返回非零值。

<a href="" id="bytesreceivedcompressed"></a>**BytesReceivedCompressed**  
指定收到的压缩数据的字节数。 仅当微型端口驱动程序支持压缩时，它才返回非零值。

<a name="remarks"></a>备注
-------

如果基础驱动程序或其 NIC 不支持压缩，则驱动程序将为字节返回零 **。未压缩或压缩** 的成员。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>








