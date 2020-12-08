---
title: OID_GEN_ADMIN_STATUS
description: 作为查询，使用 OID_GEN_ADMIN_STATUS OID 确定 (ifAdminStatus 从 RFC 2863) 的管理状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_ADMIN_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6c6942b2b330548f197c072915f79affed145fd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789669"
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

如果查询成功，接口提供程序将返回 NDIS \_ 状态 \_ SUCCESS，查询的结果可以是 [**NET \_ IF \_ ADMIN \_ STATUS**](/windows/win32/api/ifdef/ne-ifdef-net_if_admin_status) 枚举中的值之一。

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


[**NET \_ IF \_ 管理员 \_ 状态**](/windows/win32/api/ifdef/ne-ifdef-net_if_admin_status)

[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

