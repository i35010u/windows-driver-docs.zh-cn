---
title: OID_GEN_LINK_PARAMETERS
description: 作为集，NDIS 和过量驱动程序使用 OID_GEN_LINK_PARAMETERS OID 来设置微型端口适配器的当前链接状态。 微型端口驱动程序接收 NDIS_LINK_PARAMETERS 结构中的双工状态、链接速度和暂停函数。
ms.assetid: 6a8ee5b1-ac68-424f-b749-45b085ca1d75
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9c100faed784a0bbb121aacbce077ef120862cc4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843071"
---
# <a name="oid_gen_link_parameters"></a>OID\_代\_LINK\_参数


作为集，NDIS 和过量驱动程序使用 OID\_代\_LINK\_参数 OID 设置微型端口适配器的当前链接状态。 微型端口驱动程序在 NDIS\_链接\_参数结构中接收双工状态、链接速度和暂停函数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需.

\_参数结构的 NDIS\_链接定义如下：

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
[**Ndis\_对象的对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)\_结构\_参数结构。 将**标头**指定的结构的**类型**成员设置为 NDIS\_对象\_类型\_默认值、ndis 的**修订**成员\_链接\_参数\_修订版\_1 和**大小**成员到 NDIS\_SIZEOF\_LINK\_参数\_修订\_版本1。

<a href="" id="mediaduplexstate"></a>**MediaDuplexState**  
媒体双工状态。 此值与[OID\_GEN\_MEDIA\_双工\_状态](oid-gen-media-duplex-state.md)oid 返回的值相同。

<a href="" id="xmitlinkspeed"></a>**XmitLinkSpeed**  
传输链接速度，以每秒位数为单位。

<a href="" id="rcvlinkspeed"></a>**RcvLinkSpeed**  
接收链接的速度（以每秒位数为单位）。

<a href="" id="pausefunctions"></a>**PauseFunctions**  
IEEE 802.3 暂停帧的支持类型。 此成员必须是以下 pause 函数之一：

<a href="" id="ndispausefunctionsunsupported"></a>**NdisPauseFunctionsUnsupported**  
适配器或链接伙伴不支持暂停帧。

<a href="" id="ndispausefunctionssendonly"></a>**NdisPauseFunctionsSendOnly**  
适配器和链接伙伴支持仅将暂停帧从适配器发送到链接伙伴。

<a href="" id="ndispausefunctionsreceiveonly"></a>**NdisPauseFunctionsReceiveOnly**  
适配器和链接伙伴仅支持将暂停帧从链接伙伴发送到适配器

<a href="" id="ndispausefunctionssendandreceive"></a>**NdisPauseFunctionsSendAndReceive**  
适配器和链接伙伴支持在传输和接收方向上发送和接收暂停帧。

<a href="" id="autonegotiationflags"></a>**AutoNegotiationFlags**  
微型端口适配器的自动协商设置。 此成员是从以下标志的按位 "或" 创建的：

<a href="" id="ndis-link-state-xmit-link-speed-auto-negotiated"></a>NDIS\_链接\_状态\_XMIT\_链接\_速度\_自动\_协商  
适配器应通过链接伙伴自动协商传输链接速度。 如果未设置此标志，微型端口驱动程序应将传输链接速度设置为在**XmitLinkSpeed**成员中指定的值。

<a href="" id="ndis-link-state-rcv-link-speed-auto-negotiated"></a>NDIS\_链接\_状态\_RCV\_链接\_速度\_自动\_协商  
适配器应通过链接伙伴自动协调接收链接速度。 如果未设置此标志，微型端口驱动程序应将接收链接速度设置为在**RcvLinkSpeed**成员中指定的值。

<a href="" id="ndis-link-state-duplex-auto-negotiated"></a>NDIS\_链接\_状态\_双工\_自动\_协商  
适配器应通过链接伙伴自动协商双工状态。 如果未设置此标志，微型端口驱动程序应将双工状态设置为**MediaDuplexState**成员中指定的值。

<a href="" id="ndis-link-state-pause-functions-auto-negotiated"></a>NDIS\_LINK\_状态\_暂停\_函数\_已协商自动\_  
微型端口驱动程序应自动协调对暂停帧与另一端的支持。 如果未设置此标志，微型端口驱动程序应使用**PauseFunctions**成员中指定的暂停帧支持。

<a name="remarks"></a>备注
-------

**注意** 设置 OID\_代\_LINK\_参数会导致连接断开。 设置此 OID 时，微型端口驱动程序必须重新配置微型端口适配器。 例如，微型端口驱动程序可以重置微型端口适配器，导致现有连接丢失。 用于重新配置的特定机制依赖于应用程序。



如果微型端口适配器的链接状态由于 OID\_代\_LINK\_参数设置请求而发生更改，则微型端口驱动程序应生成[**NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示以通知新链接状态的 NDIS 和过量驱动程序。

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


[ **\_标头的 NDIS\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[**NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)

[OID\_代\_介质\_双工\_状态](oid-gen-media-duplex-state.md)








