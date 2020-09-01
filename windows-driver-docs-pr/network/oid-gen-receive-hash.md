---
title: OID_GEN_RECEIVE_HASH
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_RECEIVE_HASH OID 来获取微型端口适配器的当前接收哈希计算设置。
ms.assetid: be120dab-c98d-418f-8777-e2fb37b774a1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_HASH 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cdb1fbf6fd50b3f5c308f03f2637f1286c43589c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212153"
---
# <a name="oid_gen_receive_hash"></a>OID \_ 生成 \_ 接收 \_ 哈希


作为查询，NDIS 和过量驱动程序使用 OID \_ GEN \_ 接收 \_ 哈希 OID 来获取微型端口适配器的当前接收哈希计算设置。 NDIS 返回包含当前接收哈希设置的 [**ndis \_ 接收 \_ 哈希 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters) 结构。

作为一个集，NDIS 和过量驱动程序使用 OID \_ GEN \_ 接收 \_ 哈希 OID 来配置微型端口适配器上的接收哈希计算。 微型端口驱动程序接收 NDIS \_ 接收 \_ 哈希 \_ 参数结构。

<a name="remarks"></a>备注
-------

对于 NDIS 微型端口驱动程序，不请求查询。

对此 OID 集的支持对于微型端口驱动程序是可选的，包括那些支持 RSS 的程序集。

过量驱动程序可以使用 OID 生成 \_ \_ 接收 \_ 哈希 OID 在收到的帧上启用和配置哈希计算，而无需启用 RSS。

**注意**   协议驱动程序必须在启用 RSS 计算之前禁用它们。 如果启用了 RSS，则协议驱动程序会在启用接收哈希计算之前禁用 RSS。 如果当前启用了[oid 生成 \_ \_ 接收 \_ 刻度 \_ 参数](oid-gen-receive-scale-parameters.md)，微型端口驱动程序应使具有**NDIS \_ 状态 \_ 无效 \_ OID**或** \_ \_ 不 \_ 支持 ndis 状态**的 set 请求失败以启用接收哈希计算。

 

**注意**   在[**NDIS \_ 接收到 \_ 哈希 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)结构成员后追加机密密钥。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 接收 \_ 哈希 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)

 

