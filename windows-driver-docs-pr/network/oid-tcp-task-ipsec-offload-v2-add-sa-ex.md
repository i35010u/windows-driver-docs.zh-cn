---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX
description: 作为集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX OID 来请求微型端口驱动程序将指定的安全关联（SAs）添加到 NIC。
ms.assetid: 9D356CFA-3353-4E62-9B1C-0FF650DCE75C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f0038311fbeb7573920fc4f31e5fc44b8265db9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843889"
---
# <a name="oid_tcp_task_ipsec_offload_v2_add_sa_ex"></a>OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组设置，TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_EX OID 来请求微型端口驱动程序将指定的安全关联（SAs）添加到 NIC。

**请注意**  通过直接 OID 请求接口，NDIS 支持此 oid。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 Oid 请求接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本2（IPsecOV2）的 NDIS 6.30 微型端口驱动程序必须支持此 OID。

TCP/IP 传输确定 NIC 可以执行 IPsecOV2 操作后，TCP/IP 传输请求微型端口驱动程序以添加 SAs。 传输添加 SA 之前，传输无法将 IPsecOV2 操作卸载到 NIC。

微型端口驱动程序将 NIC 配置为针对 SAs 的 IPsecOV2 处理。 成功设置到 OID 后\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_例如，微型端口驱动程序提供了用于标识[**IPSEC\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)的**OffloadHandle**成员中的卸载 sa 的句柄\_\_# EX 结构。\_ （例如，传输使用发送路径中的句柄来指示要使用的卸载 SA）。 如果卸载了 SA，则该设置请求成功。

小型端口驱动程序可能会返回 OID 请求的失败状态，例如，当 NIC 用尽容量来卸载更多 SAs 时。 此外，微型端口驱动程序可能会返回失败状态，因为它需要避免争用条件。 在这种情况下，NIC 配置会更改，并排除特定的算法。

如果请求失败，则不会卸载 SAs。 如果 SA 发生故障，微型端口驱动程序应将相应 IPSEC 中的**OffloadHandle**成员设置\_卸载\_V2\_将\_SA\_EX 结构添加到**NULL**。

微型端口驱动程序报告在初始化期间，在[**NDIS\_IPSEC\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构的**SaOffloadCapacity**成员中可以支持的最大 SAs 数目。 如有必要，TCP/IP 传输可以将[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_delete\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md) OID 来请求微型端口驱动程序删除 NIC 中的 SA。

此 OID 本质上与以前的版本相同， [oid\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)。 唯一的区别是更新后的[**IPSEC\_卸载\_V2\_添加\_SA\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)结构。

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IPSEC\_卸载\_V2\_添加\_SA\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)

[ **\_卸载\_V2 的 NDIS\_IPSEC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)

[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)

[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




