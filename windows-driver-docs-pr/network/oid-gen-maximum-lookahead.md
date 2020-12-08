---
title: OID_GEN_MAXIMUM_LOOKAHEAD
description: 作为查询，OID_GEN_MAXIMUM_LOOKAHEAD OID 指定 NIC 可提供的最大字节数，作为预测先行数据。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAXIMUM_LOOKAHEAD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6bdd1c615eaca89c1f44e64ed67e6ca8dadc29a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816547"
---
# <a name="oid_gen_maximum_lookahead"></a>OID \_ 生成 \_ 最大 \_ 预测先行


作为查询，OID \_ GEN \_ 最大 \_ 预测先行 OID 指定 NIC 可提供的最大字节数，作为预测先行数据。 此规范不包含标头。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 使用小型端口驱动程序在初始化期间提供的缓存值处理此 OID。

上层驱动程序检查预测先行数据，以确定与预测先行数据关联的数据包是否适用于其一个或多个客户端。

如果基础驱动程序支持 multipacket 接收指示，则会在每次指示时为绑定协议驱动程序提供完整的网络数据包。 因此，此值与为 [OID 生成 \_ \_ 接收 \_ 块 \_ 大小](oid-gen-receive-block-size.md)返回的值相同。

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


[OID \_ 生成 \_ 接收 \_ 块 \_ 大小](oid-gen-receive-block-size.md)

 

 




