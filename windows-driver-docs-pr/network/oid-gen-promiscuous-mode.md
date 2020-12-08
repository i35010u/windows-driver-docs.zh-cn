---
title: OID_GEN_PROMISCUOUS_MODE
description: 作为查询，请使用 OID_GEN_PROMISCUOUS_MODE OID 来确定是否 (ifPromiscuousMode 从 RFC 2863) 混合了网络接口。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PROMISCUOUS_MODE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1eb97f872140a05b656a2496261631a6f56bad30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829437"
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

## <a name="see-also"></a>请参阅


[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

