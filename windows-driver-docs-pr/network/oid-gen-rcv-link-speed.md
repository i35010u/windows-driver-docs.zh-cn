---
title: OID_GEN_RCV_LINK_SPEED
description: 作为查询，请使用 OID_GEN_RCV_LINK_SPEED OID 来确定网络接口的接收链接速度。 Windows Vista 和 laterSupported 的版本信息。 已请求 NDIS 6.0 和更高的微型端口 driversNot。 仅适用于 NDIS 接口提供程序。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RCV_LINK_SPEED 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9f5c5bc59b85ded8f135eab93f2b5229dc0380b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836753"
---
# <a name="oid_gen_rcv_link_speed"></a>OID \_ 生成 \_ RCV \_ 链接 \_ 速度


作为查询，使用 OID \_ GEN \_ RCV \_ LINK \_ 速度 OID 来确定网络接口的接收链接速度。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

如果接口提供程序返回 NDIS \_ 状态 \_ SUCCESS，则查询的结果是一个 ULONG64 值，该值指示接口的接收链接速度（以每秒位数为单位）。

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


[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

