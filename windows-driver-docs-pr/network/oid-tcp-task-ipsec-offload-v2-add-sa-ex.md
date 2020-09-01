---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX
description: 作为一个集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX OID 来请求微型端口驱动程序 (SAs) 向 NIC 添加指定的安全关联。
ms.assetid: 9D356CFA-3353-4E62-9B1C-0FF650DCE75C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9e49f4644e3aeea9cace04e797be8e3c6400a444
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213311"
---
# <a name="oid_tcp_task_ipsec_offload_v2_add_sa_ex"></a>OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一个集，TCP/IP 传输使用 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX OID 来请求微型端口驱动程序 (SAs) 添加到 NIC。

**注意**   NDIS 支持直接 OID 请求接口的此 OID。 有关直接 OID 请求接口的详细信息，请参阅 [NDIS 6.1 直接 Oid 请求接口](/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本 2 (IPsecOV2) 的 NDIS 6.30 微型端口驱动程序必须支持此 OID。

TCP/IP 传输确定 NIC 可以执行 IPsecOV2 操作后，TCP/IP 传输请求微型端口驱动程序以添加 SAs。 传输添加 SA 之前，传输无法将 IPsecOV2 操作卸载到 NIC。

微型端口驱动程序将 NIC 配置为针对 SAs 的 IPsecOV2 处理。 将成功设置为 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX，微型端口驱动程序提供了用于标识[**IPSEC \_ 卸载 \_ V2 \_ 添加 \_ sa \_ EX**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)结构的**OffloadHandle**成员中的卸载 SA 的句柄。 例如，传输使用发送路径中的句柄来指示要使用哪些卸载 SA)  (。 如果卸载了 SA，则该设置请求成功。

小型端口驱动程序可能会返回 OID 请求的失败状态，例如，当 NIC 用尽容量来卸载更多 SAs 时。 此外，微型端口驱动程序可能会返回失败状态，因为它需要避免争用条件。 在这种情况下，NIC 配置会更改，并排除特定的算法。

如果请求失败，则不会卸载 SAs。 如果 SA 发生故障，微型端口驱动程序应将相应 IPSEC 卸载 V2 中的 **OffloadHandle** 成员 \_ 设置 \_ \_ \_ \_ 为 **NULL**。

微型端口驱动程序报告在初始化期间，NIC 在[**NDIS \_ IPSEC \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构的**SaOffloadCapacity**成员中可以支持的最大 SAs 数。 如有必要，TCP/IP 传输可以设置 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ delete \_ SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md) OID 来请求微型端口驱动程序从 NIC 删除 sa。

此 OID 本质上与以前的版本（ [oid \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)）完全相同。 唯一的区别是更新后的 [**IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex) 结构。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa_ex)

[**NDIS \_ IPSEC \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)

[OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)

[OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ DELETE \_ SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

