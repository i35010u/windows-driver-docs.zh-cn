---
title: OID_GEN_UNKNOWN_PROTOS
description: 作为查询，使用 OID_GEN_UNKNOWN_PROTOS OID 从 RFC 2863) 确定 (ifInUnknownProtos 的网络接口的未知协议数据包计数。
ms.assetid: a0bebd8d-c202-41f5-84be-a3056a2eeef9
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_UNKNOWN_PROTOS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4dc0952ddd38c5ee686c4f6f10fdbc14524d3274
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217985"
---
# <a name="oid_gen_unknown_protos"></a>OID \_ 生成 \_ 未知 \_ PROTOS


作为查询，使用 OID \_ GEN \_ UNKNOWN \_ PROTOS Oid 确定*ifInUnknownProtos*) [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)中的网络 (接口的未知协议数据包计数。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

未知协议统计信息计数器指定由于关联的协议未知或不受支持而被丢弃的接口收到的数据包数。

如果接口提供程序返回 NDIS \_ 状态 \_ SUCCESS，则查询的结果为指定数据包数量的 ULONG64 值。

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

 

