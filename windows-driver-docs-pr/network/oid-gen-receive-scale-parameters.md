---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS
description: 作为查询，NDIS 和过量驱动程序可以使用 OID_GEN_RECEIVE_SCALE_PARAMETERS OID 来查询 NIC 的当前接收方缩放 (RSS) 参数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_SCALE_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b386d4f6c9fc6b599283ae89089fa17b2a910c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822136"
---
# <a name="oid_gen_receive_scale_parameters"></a>OID \_ 生成 \_ 接收 \_ 刻度 \_ 参数


作为查询，NDIS 和过量驱动程序可以使用 OID 生成 \_ \_ 接收 \_ 刻度 \_ 参数 oid 查询当前的接收方缩放 (RSS) NIC 参数。 NDIS 返回用于定义当前 RSS 参数的 [**ndis \_ 接收 \_ 缩放 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters) 结构。

作为集，NDIS 和过量驱动程序使用 OID 生成 \_ \_ 接收 \_ 刻度 \_ 参数 oid 设置 NIC 的当前 RSS 参数。 微型端口驱动程序接收 \_ \_ \_ 用于定义 RSS 参数的 NDIS 接收缩放参数结构。

> [!NOTE]
> 在 RSSv2 中，此 OID 仅用于查询给定缩放实体的当前 RSS 参数。 对于支持 RSSv2 的微型端口驱动程序，请参阅设置除间接表之外的 RSS 参数 [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) 。

<a name="remarks"></a>备注
-------

对于 NDIS 微型端口驱动程序，不会请求该查询，并且支持 RSS 的驱动程序需要此设置。 NDIS 处理微型端口驱动程序的查询。

TCP/IP 驱动程序使用 OID 生成 \_ \_ 接收 \_ 缩放参数的单个 oid 集请求来配置 IPv4 和 IPv6 \_ 。 也就是说，当堆栈应同时启用 IPv4 和 IPv6 的 RSS 时，它会在 [**NDIS \_ 接收 \_ 缩放 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)结构的 **HashInformation** 成员中设置这两个对应的标志，并发送一个 OID 请求。 此外，IPv4 和 IPv6 使用相同的密钥，密钥将始终为40字节，即使只启用 IPv4。

基础微型端口适配器必须使用收到的最近 OID \_ 生成 \_ 接收 \_ 刻度 \_ 参数 oid 设置。 例如，如果微型端口获取 OID 生成 \_ \_ 接收 \_ 刻度 \_ 参数 OID，但该 oid 缺少 ipv4 哈希类型，则它必须禁用 ipv4 RSS （如果以前已启用）。

**注意**  过量驱动程序可以使用 [OID 生成 \_ \_ 接收 \_ 哈希](oid-gen-receive-hash.md) OID 在收到的帧上启用和配置哈希计算，而无需启用 RSS。

 

**注意**  协议驱动程序必须在启用 RSS 之前，禁用 ([OID \_ GEN \_ 接收 \_ 哈](oid-gen-receive-hash.md) 希) 的接收哈希计算。 如果启用了 RSS，则协议驱动程序会在启用接收哈希计算之前禁用 RSS。 如果当前已启用 OID 生成接收哈希，微型端口驱动程序应使具有 **NDIS \_ 状态 \_ 无效 \_ OID** 的 set 请求或 **\_ \_ 不 \_ 支持的 ndis 状态** 设置为启用 RSS \_ \_ \_ 。

 

**注意**  间接寻址表和机密密钥追加在 [**NDIS \_ 接收 \_ 缩放 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters) 结构成员之后。 有关间接表和密钥的详细信息，请参阅 **NDIS \_ 接收 \_ 缩放 \_ 参数**。

 

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

## <a name="see-also"></a>请参阅


[**NDIS \_ 接收 \_ 刻度 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)

[OID \_ 生成 \_ 接收 \_ 哈希](oid-gen-receive-hash.md)

 

