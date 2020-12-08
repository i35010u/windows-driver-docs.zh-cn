---
title: OID_GEN_ALIAS
description: 作为查询，使用 OID_GEN_ALIAS OID 从 RFC 2863) 获取接口 (的别名字符串。 Windows Vista 和 laterSupported 的版本信息。 已请求 NDIS 6.0 和更高的微型端口 driversNot。 仅适用于 NDIS 接口提供程序。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_ALIAS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d5b4d1f12b346a9c7cdf0fe01876ef684733659d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840631"
---
# <a name="oid_gen_alias"></a>OID \_ 生成 \_ 别名


作为查询，使用 OID 生成 \_ \_ 别名 OID 从 [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)) 中获取接口 (*ifAlias* 的别名字符串。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

[NDIS 网络接口](./ndis-network-interfaces2.md)提供程序可以为其接口指定唯一的别名字符串。 如果该名称应与相同的接口保持关联，则提供程序可以在计算机重新启动后使字符串持久，并 reinitializations。

只有 NDIS 网络接口提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 OID 请求。

如果接口提供程序返回 NDIS \_ 状态 \_ SUCCESS，则查询的结果是在 NDIS 中返回的别名字符串（ \_ 如果 \_ 计数 \_ 字符串结构）。

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

 

