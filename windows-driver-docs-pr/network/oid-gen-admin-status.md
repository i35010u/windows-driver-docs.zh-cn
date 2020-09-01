---
title: OID_GEN_ADMIN_STATUS
description: 作为查询，使用 OID_GEN_ADMIN_STATUS OID 确定 (ifAdminStatus 从 RFC 2863) 的管理状态。
ms.assetid: e8f45521-7419-4c11-b84b-36d4d3306fc2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_ADMIN_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4fa3dffe9a7a99615c0bc9433d6a713b6e1147f8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206367"
---
# <a name="oid_gen_admin_status"></a>OID \_ 生成 \_ 管理员 \_ 状态


作为查询，使用 OID 生成 \_ \_ 管理员 \_ 状态 oid 来确定 (*ifAdminStatus* 从 [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)) 的管理状态。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

"管理状态" 是系统管理员请求的状态。

只有 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

如果查询成功，接口提供程序将返回 NDIS \_ 状态 \_ SUCCESS，查询的结果可以是 [**NET \_ IF \_ ADMIN \_ STATUS**](/windows/desktop/api/ifdef/ne-ifdef-_net_if_admin_status) 枚举中的值之一。

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


[**NET \_ IF \_ 管理员 \_ 状态**](/windows/desktop/api/ifdef/ne-ifdef-_net_if_admin_status)

[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

