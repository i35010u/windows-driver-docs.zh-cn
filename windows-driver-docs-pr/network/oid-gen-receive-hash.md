---
title: OID_GEN_RECEIVE_HASH
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_RECEIVE_HASH OID 来获取微型端口适配器的当前接收哈希计算设置。
ms.assetid: be120dab-c98d-418f-8777-e2fb37b774a1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_HASH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c2d5d3c6fc63a37d3fcd552855d81e243e392158
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840474"
---
# <a name="oid_gen_receive_hash"></a>OID\_代\_接收\_哈希


作为查询，NDIS 和过量驱动程序使用 OID\_GEN\_接收\_哈希 OID 来获取微型端口适配器的当前接收哈希计算设置。 NDIS 返回[**ndis\_接收\_哈希\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)结构，其中包含当前的接收哈希设置。

作为集，NDIS 和过量驱动程序使用 OID\_GEN\_接收\_哈希 OID 来配置微型端口适配器上的接收哈希计算。 微型端口驱动程序接收 NDIS\_接收\_哈希\_参数结构。

<a name="remarks"></a>备注
-------

对于 NDIS 微型端口驱动程序，不请求查询。

对此 OID 集的支持对于微型端口驱动程序是可选的，包括那些支持 RSS 的程序集。

过量驱动程序可以使用 OID\_GEN\_接收\_哈希 OID）在收到的帧上启用和配置哈希计算，而无需启用 RSS。

**请注意**  协议驱动程序必须在启用 RSS 计算之前禁用它们。 如果启用了 RSS，则协议驱动程序会在启用接收哈希计算之前禁用 RSS。 微型端口驱动程序应使具有 NDIS\_状态的 set 请求失败 **\_无效的\_OID**或**ndis\_状态\_不\_支持**，以在[OID\_代\_接收时启用接收哈希计算\_缩放\_参数](oid-gen-receive-scale-parameters.md)当前已启用。

 

**请注意**  在[**NDIS\_接收\_哈希\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)结构成员后追加机密密钥。

 

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_接收\_哈希\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)

 

 




