---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS
description: 作为查询，NDIS 和过量驱动程序可以使用 OID_GEN_RECEIVE_SCALE_PARAMETERS OID 来查询 NIC 的当前接收方缩放（RSS）参数。
ms.assetid: a54190f7-0d2e-4f85-84c2-05fc9ec4994a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_SCALE_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d1a045daf09cf3cf5804aa12871f29b83871335a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844606"
---
# <a name="oid_gen_receive_scale_parameters"></a>OID\_代\_接收\_扩展\_参数


作为查询，NDIS 和过量驱动程序可以使用 OID\_GEN\_接收\_扩展\_参数 OID 来查询 NIC 的当前接收方缩放（RSS）参数。 NDIS 返回[**ndis\_接收\_缩放\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)结构，该结构定义当前 RSS 参数。

作为集，NDIS 和过量驱动程序使用 OID\_GEN\_接收\_SCALE\_参数 OID 来设置 NIC 的当前 RSS 参数。 微型端口驱动程序接收 NDIS\_接收\_缩放\_参数结构，该结构定义 RSS 参数。

> [!NOTE]
> 在 RSSv2 中，此 OID 仅用于查询给定缩放实体的当前 RSS 参数。 对于支持 RSSv2 的微型端口驱动程序，请参阅设置除间接表之外的 RSS 参数[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) 。

<a name="remarks"></a>备注
-------

对于 NDIS 微型端口驱动程序，不会请求该查询，并且支持 RSS 的驱动程序需要此设置。 NDIS 处理微型端口驱动程序的查询。

TCP/IP 驱动程序使用 OID 的单个 OID 集请求来配置 IPv4 和 IPv6\_代\_接收\_缩放\_参数。 也就是说，当堆栈应同时启用 IPv4 和 IPv6 的 RSS 时，它会在 NDIS\_的**HashInformation**成员中设置这两个对应的标志， [ **\_缩放\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)结构并发送一个 OID 请求。 此外，IPv4 和 IPv6 使用相同的密钥，密钥将始终为40字节，即使只启用 IPv4。

基础微型端口适配器必须使用最近的 OID\_GEN\_接收\_已收到的参数 OID 设置\_。 例如，如果微型端口获取 OID\_代\_接收\_缩放\_缺少 IPv4 哈希类型的参数 OID，则必须禁用 IPv4 RSS （如果以前已启用）。

**请注意**  过量驱动程序可以使用[OID\_GEN\_接收\_哈希](oid-gen-receive-hash.md)OID，以便在不启用 RSS 的情况下启用和配置收到的帧上的哈希计算。

 

**请注意**  协议驱动程序必须在启用 RSS 计算之前禁用接收哈希计算（[OID\_GEN\_接收\_哈希](oid-gen-receive-hash.md)）。 如果启用了 RSS，则协议驱动程序会在启用接收哈希计算之前禁用 RSS。 微型端口驱动程序应使具有 NDIS\_状态的 set 请求失败 **\_无效的\_OID**或**ndis\_状态\_不\_支持**，以便在当前启用了 OID\_生成\_的情况时启用 RSS。\_

 

**请注意**  在[**NDIS\_接收\_扩展\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)结构成员后追加间接表和机密密钥。 有关间接表和密钥的详细信息，请参阅**NDIS\_接收\_缩放\_参数**。

 

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


[**NDIS\_接收\_刻度\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)

[OID\_代\_接收\_哈希](oid-gen-receive-hash.md)

 

 




