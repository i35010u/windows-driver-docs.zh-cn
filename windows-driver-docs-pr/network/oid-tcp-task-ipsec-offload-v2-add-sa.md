---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA
description: 作为一个集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA OID 来请求微型端口驱动程序 (SAs) 向 NIC 添加指定的安全关联。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e8296989f80e632cb5535d89bed7c6f4ac0a7f5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838559"
---
# <a name="oid_tcp_task_ipsec_offload_v2_add_sa"></a>OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一个集，TCP/IP 传输使用 OID \_ TCP \_ 任务 " \_ IPSEC \_ 卸载 \_ V2" \_ 添加 \_ SA OID 来请求微型端口驱动程序 (SAs) 添加到 NIC。

**注意**  NDIS 支持直接 OID 请求接口的此 OID。 有关直接 OID 请求接口的详细信息，请参阅 [NDIS 6.1 直接 Oid 请求接口](/windows-hardware/drivers/ddi/_netvista/)。

 

**注意**  此 OID 在 NDIS 6.1 和6.20 中受支持。 对于 NDIS 6.30 和更高版本的驱动程序，请参阅[OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本 2 (IPsecOV2) 的 NDIS 6.1 和6.20 微型端口驱动程序必须支持此 OID。

TCP/IP 传输确定 NIC 可以执行 IPsecOV2 操作后，TCP/IP 传输请求微型端口驱动程序以添加 SAs。 传输添加 SA 之前，传输无法将 IPsecOV2 操作卸载到 NIC。

微型端口驱动程序接收 [**IPSEC \_ 卸载 \_ v2 \_ 添加 \_ sa**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa) 结构，该结构包含指向 \_ 链接列表中下一个 IPSEC 卸载 \_ v2 \_ 添加 \_ sa 结构的指针。 微型端口驱动程序将 NIC 配置为针对 SAs 的 IPsecOV2 处理。 如果成功设置为 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ v2 \_ ADD \_ sa，微型端口驱动程序会提供用于标识 IPSEC 卸载 **OffloadHandle** \_ \_ V2 \_ 添加 \_ SA 的 OffloadHandle 成员中已卸载的 SAs 的句柄。 例如，传输使用发送路径中的句柄来指示要使用哪些卸载 SA)  (。 如果链接列表中的任何 SAs 已卸载，则该设置请求成功。

小型端口驱动程序可能会返回 OID 请求的失败状态，例如，当 NIC 用尽容量来卸载更多 SAs 时。 此外，微型端口驱动程序可能会返回失败状态，因为它需要避免争用条件。 在这种情况下，NIC 配置会更改，并排除特定的算法。

如果请求失败，则不会卸载链接列表中的任何 SAs。 如果链接列表中的某个 SA 发生故障，微型端口驱动程序应将相应 IPSEC 卸载 V2 中的 **OffloadHandle** 成员 \_ 设置 \_ \_ \_ 为 **NULL**。

微型端口驱动程序报告在初始化期间，NIC 在 [**NDIS \_ IPSEC \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构的 **SaOffloadCapacity** 成员中可以支持的最大 SAs 数。 如有必要，TCP/IP 传输可以设置 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ delete \_ SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md) OID 来请求微型端口驱动程序从 NIC 删除 sa。

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
<td><p>在 NDIS 6.1 和6.20 中受支持。 对于 NDIS 6.30 和更高版本，请使用 <a href="oid-tcp-task-ipsec-offload-v2-add-sa-ex.md" data-raw-source="[OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)">OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX</a>。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)

[**NDIS \_ IPSEC \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)

[OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

[OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ DELETE \_ SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

