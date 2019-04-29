---
title: OID_GEN_LINK_PARAMETERS
description: 作为一组 NDIS 和基础驱动程序使用 OID_GEN_LINK_PARAMETERS OID 来设置的微型端口适配器的当前链接状态。 微型端口驱动程序收到 NDIS_LINK_PARAMETERS 结构中的双工状态、 链接速度和暂停函数。
ms.assetid: 6a8ee5b1-ac68-424f-b749-45b085ca1d75
ms.date: 08/08/2017
keywords: -OID_GEN_LINK_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 18fac22d61a6ce300cb234cc680e93117e1d1bcc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375687"
---
# <a name="oidgenlinkparameters"></a>OID\_GEN\_链接\_参数


作为一组 NDIS 和基础驱动程序使用 OID\_GEN\_链接\_参数 OID 的微型端口适配器的当前链接状态设置。 微型端口驱动程序在 NDIS 接收双工状态、 链接速度和暂停函数\_链接\_参数结构。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。

NDIS\_链接\_参数结构定义，如下所示：

```ManagedCPlusPlus
    typedef struct _NDIS_LINK_PARAMETERS {
         NDIS_OBJECT_HEADER Header;
         NDIS_MEDIA_DUPLEX_STATE MediaDuplexState;
         ULONG64 XmitLinkSpeed;
         ULONG64 RcvLinkSpeed;
         NDIS_SUPPORTED_PAUSE_FUNCTIONS PauseFunctions;
         ULONG AutoNegotiationFlags;
    } NDIS_LINK_PARAMETERS, *PNDIS_LINK_PARAMETERS;
```




此结构包含以下成员：

<a href="" id="header"></a>**标头**  
[ **NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588) ndis 结构\_链接\_参数结构。 设置**类型**结构中的成员的**标头**指定到 NDIS\_对象\_类型\_默认情况下，**修订**成员添加到 NDIS\_链接\_参数\_修订\_1，并且**大小**成员添加到 NDIS\_SIZEOF\_链接\_参数\_修订\_1。

<a href="" id="mediaduplexstate"></a>**MediaDuplexState**  
介质双工状态。 此值是通过返回的值相同[OID\_代\_媒体\_双工\_状态](oid-gen-media-duplex-state.md)OID。

<a href="" id="xmitlinkspeed"></a>**XmitLinkSpeed**  
传输链接的速度比特 / 秒。

<a href="" id="rcvlinkspeed"></a>**RcvLinkSpeed**  
接收链接的速度比特 / 秒。

<a href="" id="pausefunctions"></a>**PauseFunctions**  
支持 IEEE 802.3 暂停帧的类型。 此成员必须为下列暂停函数之一：

<a href="" id="ndispausefunctionsunsupported"></a>**NdisPauseFunctionsUnsupported**  
适配器或链接的合作伙伴不支持暂停帧。

<a href="" id="ndispausefunctionssendonly"></a>**NdisPauseFunctionsSendOnly**  
仅暂停帧发送从适配器到链接合作伙伴适配器和链接合作伙伴支持。

<a href="" id="ndispausefunctionsreceiveonly"></a>**NdisPauseFunctionsReceiveOnly**  
仅将暂停帧从链接合作伙伴发送到适配器适配器和链接的合作伙伴支持

<a href="" id="ndispausefunctionssendandreceive"></a>**NdisPauseFunctionsSendAndReceive**  
适配器和链接合作伙伴支持发送和接收的暂停在这种帧传输和接收方向。

<a href="" id="autonegotiationflags"></a>**AutoNegotiationFlags**  
微型端口适配器的自动协商设置。 此成员是从以下标志的按位 OR 创建：

<a href="" id="ndis-link-state-xmit-link-speed-auto-negotiated"></a>NDIS\_链接\_状态\_XMIT\_链接\_速度\_自动\_NEGOTIATED  
适配器应自动协商传输链接速度与链接合作伙伴。 如果未设置此标志，微型端口驱动程序应设置为在指定的值的传输链接速度**XmitLinkSpeed**成员。

<a href="" id="ndis-link-state-rcv-link-speed-auto-negotiated"></a>NDIS\_LINK\_STATE\_RCV\_LINK\_SPEED\_AUTO\_NEGOTIATED  
适配器应自动协商接收链接速度与链接合作伙伴。 如果未设置此标志，微型端口驱动程序应设置为在指定的值的接收链接速度**RcvLinkSpeed**成员。

<a href="" id="ndis-link-state-duplex-auto-negotiated"></a>NDIS\_LINK\_STATE\_DUPLEX\_AUTO\_NEGOTIATED  
适配器应自动协商的双工状态与链接合作伙伴。 如果未设置此标志，微型端口驱动程序应将双工状态设置为在指定的值**MediaDuplexState**成员。

<a href="" id="ndis-link-state-pause-functions-auto-negotiated"></a>NDIS\_链接\_状态\_暂停\_函数\_自动\_NEGOTIATED  
微型端口驱动程序应自动协商暂停帧与另一端的支持。 如果未设置此标志，微型端口驱动程序应使用中指定的暂停帧支持**PauseFunctions**成员。

<a name="remarks"></a>备注
-------

**请注意**设置 OID\_代\_链接\_参数可能会导致连接丢失。 当设置此 OID 时，微型端口驱动程序必须重新配置的微型端口适配器。 例如，微型端口驱动程序可以重置生成现有的连接丢失的微型端口适配器。 重新配置的特定机制是独立于应用程序。



如果微型端口适配器的链接状态发生更改，因为 OID\_GEN\_链接\_参数设置请求、 微型端口驱动程序应生成[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)状态指示通知 NDIS 和基础驱动程序的新的链接状态。

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


[**NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)

[**NDIS\_STATUS\_LINK\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567391)

[OID\_GEN\_MEDIA\_DUPLEX\_STATE](oid-gen-media-duplex-state.md)








