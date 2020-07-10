---
title: OID_GEN_LINK_PARAMETERS
description: 作为集，NDIS 和过量驱动程序使用 OID_GEN_LINK_PARAMETERS OID 来设置微型端口适配器的当前链接状态。 微型端口驱动程序在 NDIS_LINK_PARAMETERS 结构中接收双工状态、链接速度和暂停函数。
ms.assetid: 6a8ee5b1-ac68-424f-b749-45b085ca1d75
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7b406886165212a65820260d71f578b6a7e12c29
ms.sourcegitcommit: 3d676aa234debfc34668705beddd36f543f7f828
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199486"
---
# <a name="oid_gen_link_parameters"></a>OID \_ 生成 \_ 链接 \_ 参数


作为集，NDIS 和过量驱动程序使用 OID 生成 \_ \_ 链接 \_ 参数 OID 设置微型端口适配器的当前链接状态。 小型端口驱动程序在 NDIS \_ 链接参数结构中接收双工状态、链接速度和暂停函数 \_ 。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。

NDIS \_ LINK \_ 参数结构定义如下：

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
NDIS 链接参数结构的[**ndis \_ 对象 \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构 \_ \_ 。 设置**标头**指定为 ndis 对象类型默认值的结构的**类型**成员 \_ \_ \_ 、Ndis **Revision** \_ 链接参数修订版本1的修订成员， \_ \_ \_ 以及 ndis **Size** \_ SIZEOF \_ 链接 \_ 参数 \_ 修订版本 \_ 1 的大小成员。

<a href="" id="mediaduplexstate"></a>**MediaDuplexState**  
媒体双工状态。 此值与[OID 生成 \_ \_ 媒体 \_ 双工 \_ 状态](oid-gen-media-duplex-state.md)oid 返回的值相同。

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

<a href="" id="ndis-link-state-xmit-link-speed-auto-negotiated"></a>NDIS \_ 链接 \_ 状态 \_ XMIT \_ 链接 \_ 速度 \_ 自动 \_ 协商  
适配器应通过链接伙伴自动协商传输链接速度。 如果未设置此标志，微型端口驱动程序应将传输链接速度设置为在**XmitLinkSpeed**成员中指定的值。

<a href="" id="ndis-link-state-rcv-link-speed-auto-negotiated"></a>NDIS \_ 链接 \_ 状态 \_ RCV \_ 链接 \_ 速度 \_ 自动 \_ 协商  
适配器应通过链接伙伴自动协调接收链接速度。 如果未设置此标志，微型端口驱动程序应将接收链接速度设置为在**RcvLinkSpeed**成员中指定的值。

<a href="" id="ndis-link-state-duplex-auto-negotiated"></a>NDIS \_ 链接 \_ 状态 \_ 双工 \_ 自动 \_ 协商  
适配器应通过链接伙伴自动协商双工状态。 如果未设置此标志，微型端口驱动程序应将双工状态设置为**MediaDuplexState**成员中指定的值。

<a href="" id="ndis-link-state-pause-functions-auto-negotiated"></a>NDIS \_ 链接 \_ 状态 \_ 暂停 \_ 函数 \_ 自动 \_ 协商  
微型端口驱动程序应自动协调对暂停帧与另一端的支持。 如果未设置此标志，微型端口驱动程序应使用**PauseFunctions**成员中指定的暂停帧支持。

<a name="remarks"></a>注解
-------

**注意** 设置 OID \_ 生成 \_ 链接 \_ 参数可能会导致连接断开。 设置此 OID 时，微型端口驱动程序必须重新配置微型端口适配器。 例如，微型端口驱动程序可以重置微型端口适配器，导致现有连接丢失。 用于重新配置的特定机制依赖于应用程序。



如果微型端口适配器的链接状态由于 OID 生成 \_ \_ 链接 \_ 参数设置请求而发生更改，则微型端口驱动程序应生成一个[**NDIS \_ 状态 \_ 链接 \_ 状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示，以通知 ndis 和过量驱动程序的新链接状态。

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

## <a name="see-also"></a>另请参阅


[**NDIS \_ 对象 \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[**NDIS \_ 状态 \_ 链接 \_ 状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)

[OID \_ 生成 \_ 介质 \_ 双工 \_ 状态](oid-gen-media-duplex-state.md)








