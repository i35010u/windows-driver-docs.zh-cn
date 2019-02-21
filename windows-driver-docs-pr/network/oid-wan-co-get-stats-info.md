---
title: OID_WAN_CO_GET_STATS_INFO
description: OID_WAN_CO_GET_STATS_INFO OID 请求微型端口驱动程序，以返回特定于虚拟连接 (VC) 的统计信息。
ms.assetid: 53ab1c04-7bb2-401d-ad54-72f3c1587dc0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_STATS_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7ae1e2597a80d8a917eca0616c23f19df5ee4eba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555887"
---
# <a name="oidwancogetstatsinfo"></a>OID\_WAN\_共同\_获取\_统计信息\_信息


OID\_WAN\_共同\_获取\_统计信息\_信息 OID 请求微型端口驱动程序，以返回特定于虚拟连接 (VC) 的统计信息。 WAN 微型端口驱动程序应保持统计信息，并要为此 OID NDIS 中返回这些统计信息\_WAN\_共同\_获取\_统计信息\_信息结构，定义，如下所示：

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




此结构的成员包含下列信息：

<a href="" id="bytessent"></a>**BytesSent**  
指定传输的字节数。

<a href="" id="bytesrcvd"></a>**BytesRcvd**  
指定接收的字节数。

<a href="" id="framessent"></a>**FramesSent**  
指定发送帧 （WAN 数据包） 的数量。

<a href="" id="framesrcvd"></a>**FramesRcvd**  
指定接收到的帧数。

<a href="" id="crcerrors"></a>**CRCErrors**  
指定有关此 VC 遇到的 CRC 错误数。 CRC 错误的循环冗余检查故障所引起。 CRC 错误指示找出现乱码到达时接收的帧中的一个或多个字节。

<a href="" id="timeouterrors"></a>**TimeoutErrors**  
指定此 VC 中遇到超时错误数。 在时间内未收到预期的字节时出现超时错误。

<a href="" id="alignmenterrors"></a>**AlignmentErrors**  
指定遇到此 VC 对齐错误数。 对齐错误发生时接收到一个字节是不同于预期的字节。 这通常发生丢失一个字节时或发生超时错误。

<a href="" id="serialoverrunerrors"></a>**SerialOverrunErrors**  
指定遇到此 VC 串行溢出的数量。 串行溢出发生时 WAN NIC 无法处理的接收数据的速率。

<a href="" id="framingerrors"></a>**FramingErrors**  
指定遇到此 VC 帧错误数。 组帧错误发生时异步字节收到了无效的开始或停止位。

<a href="" id="bufferoverrunerrors"></a>**BufferOverrunErrors**  
指定此 VC 中遇到的缓冲区溢出的数量。 当 WAN 微型端口驱动程序无法处理的接收数据的速率时，就会发生缓冲区溢出。

<a href="" id="bytestransmitteduncompressed"></a>**BytesTransmittedUncompressed**  
指定未压缩的数据传输的字节的数。 仅当它支持压缩，微型端口驱动程序返回非零值。

<a href="" id="bytesreceiveduncompressed"></a>**BytesReceivedUncompressed**  
指定的收到的未压缩数据的字节数。 仅当它支持压缩，微型端口驱动程序返回非零值。

<a href="" id="bytestransmittedcompressed"></a>**BytesTransmittedCompressed**  
指定的压缩数据传输的字节数。 仅当它支持压缩，微型端口驱动程序返回非零值。

<a href="" id="bytesreceivedcompressed"></a>**BytesReceivedCompressed**  
指定接收的压缩数据的字节数。 仅当它支持压缩，微型端口驱动程序返回非零值。

<a name="remarks"></a>备注
-------

如果基础驱动程序或其 NIC 不支持压缩，驱动程序将返回零**字节...未压缩压缩**成员。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>








