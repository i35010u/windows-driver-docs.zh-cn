---
title: OID_GEN_OPERATIONAL_STATUS
description: 作为查询，使用 OID_GEN_OPERATIONAL_STATUS OID 确定 (ifOperStatus 从 RFC 2863) 的网络接口的当前操作状态。
ms.assetid: fa00d449-6ec0-4e72-8d9c-a453a0b1f3e9
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_OPERATIONAL_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 79b28976173e4db55e7954309b1b955a167469ab
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213413"
---
# <a name="oid_gen_operational_status"></a>OID \_ 生成 \_ 操作 \_ 状态


作为查询，使用 OID 生成 \_ \_ 操作 \_ 状态 OID 从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)) 中 (*ifOperStatus*来确定网络接口的当前操作状态。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

NDIS 处理微型端口适配器和筛选器模块的此 OID，仅 [ndis 网络接口](./ndis-network-interfaces2.md) 提供程序接收此 oid 查询。

如果查询成功，接口提供程序将返回 NDIS \_ 状态 \_ SUCCESS，查询的结果可以是 [**NET \_ IF \_ 操作系统 \_ STATUS**](/windows/desktop/api/ifdef/ne-ifdef-_net_if_oper_status) 枚举中的值之一。

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


[**NET \_ IF \_ 操作系统 \_**](/windows/desktop/api/ifdef/ne-ifdef-_net_if_oper_status)

[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

