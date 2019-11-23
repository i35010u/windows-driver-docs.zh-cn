---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA
description: 作为集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA OID 来请求微型端口驱动程序将指定的安全关联（SAs）添加到 NIC。
ms.assetid: bd1d0cf2-234d-4c06-904e-fe2de6022981
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cbe156d3c4aeaaf86dd146852ad83529114fb8a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843888"
---
# <a name="oid_tcp_task_ipsec_offload_v2_add_sa"></a>OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组设置，TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA OID 来请求微型端口驱动程序将指定的安全关联（SAs）添加到 NIC。

**请注意**  通过直接 OID 请求接口，NDIS 支持此 oid。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 Oid 请求接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

**请注意**，在 NDIS 6.1 和6.20 中支持此 OID  。 对于 NDIS 6.30 和更高版本的驱动程序，请参阅[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本2（IPsecOV2）的 NDIS 6.1 和6.20 微型端口驱动程序必须支持此 OID。

TCP/IP 传输确定 NIC 可以执行 IPsecOV2 操作后，TCP/IP 传输请求微型端口驱动程序以添加 SAs。 传输添加 SA 之前，传输无法将 IPsecOV2 操作卸载到 NIC。

微型端口驱动程序接收[**IPSEC\_卸载\_v2\_添加\_sa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)结构，该结构包含指向下一个 IPSEC\_卸载\_V2\_在链接列表中添加\_SA 结构的指针。 微型端口驱动程序将 NIC 配置为针对 SAs 的 IPsecOV2 处理。 成功设置到 OID 后\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA，微型端口驱动程序**提供了用于**标识 IPSEC\_\_\_\_ （例如，传输使用发送路径中的句柄来指示要使用的卸载 SA）。 如果链接列表中的任何 SAs 已卸载，则该设置请求成功。

小型端口驱动程序可能会返回 OID 请求的失败状态，例如，当 NIC 用尽容量来卸载更多 SAs 时。 此外，微型端口驱动程序可能会返回失败状态，因为它需要避免争用条件。 在这种情况下，NIC 配置会更改，并排除特定的算法。

如果请求失败，则不会卸载链接列表中的任何 SAs。 如果链接列表中的某个 SA 发生故障，微型端口驱动程序应将相应 IPSEC 中的**OffloadHandle**成员设置\_卸载\_V2\_将\_SA 结构添加到**NULL**。

微型端口驱动程序报告在初始化期间，在[**NDIS\_IPSEC\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构的**SaOffloadCapacity**成员中可以支持的最大 SAs 数目。 如有必要，TCP/IP 传输可以将[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_delete\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md) OID 来请求微型端口驱动程序删除 NIC 中的 SA。

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
<td><p>在 NDIS 6.1 和6.20 中受支持。 对于 NDIS 6.30 和更高版本，请使用<a href="oid-tcp-task-ipsec-offload-v2-add-sa-ex.md" data-raw-source="[OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)">OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX</a>。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IPSEC\_卸载\_V2\_添加\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)

[ **\_卸载\_V2 的 NDIS\_IPSEC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)

[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




