---
title: OID_GEN_INTERFACE_INFO
description: 作为查询，使用 OID_GEN_INTERFACE_INFO OID 获取网络接口的当前状态和统计信息。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_INTERFACE_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e45fb340cb8221b0e70858aefd6a89476fd91e11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787193"
---
# <a name="oid_gen_interface_info"></a>OID \_ 代 \_ 接口 \_ 信息


作为查询，使用 OID \_ GEN \_ 接口 \_ 信息 OID 获取网络接口的当前状态和统计信息。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

如果查询成功，接口提供程序将返回 NDIS \_ 状态 \_ 成功，查询的结果为 [**ndis \_ 接口 \_ 信息**](/windows/win32/api/ifdef/ns-ifdef-ndis_interface_information) 结构。 此结构包含在接口的生存期内发生更改的信息。

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


[**NDIS \_ 接口 \_ 信息**](/windows/win32/api/ifdef/ns-ifdef-ndis_interface_information)

[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

