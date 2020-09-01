---
title: OID_GEN_PROMISCUOUS_MODE
description: 作为查询，请使用 OID_GEN_PROMISCUOUS_MODE OID 来确定是否 (ifPromiscuousMode 从 RFC 2863) 混合了网络接口。
ms.assetid: c3ba0908-724c-4149-a66f-5c3d41751165
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PROMISCUOUS_MODE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b19805d30979f5657370c3df5e7c3e164d3b9d1a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213383"
---
# <a name="oid_gen_promiscuous_mode"></a>OID \_ 代 \_ 混合 \_ 模式


作为查询，请使用 OID \_ GEN \_ 混合 \_ 模式 OID 来确定是否 (*ifPromiscuousMode* 从 [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)) 中混合了网络接口。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

如果接口提供程序返回 NDIS \_ 状态 \_ SUCCESS，并且接口仅接受寻址到该接口的数据包，则结果值应为 **FALSE**。 如果接口接受所有网络数据包，则此值应为 **TRUE** 。

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


[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

