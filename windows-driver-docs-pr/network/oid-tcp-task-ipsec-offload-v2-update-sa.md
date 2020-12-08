---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA
description: 作为集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA OID 来请求微型端口驱动程序更新 NIC 上的指定安全关联 (SAs) 。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 472d5ad22090c3723b78bacb4492c7b05fff026c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792647"
---
# <a name="oid_tcp_task_ipsec_offload_v2_update_sa"></a>OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 更新 \_ SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一个集，TCP/IP 传输使用 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 更新 \_ SA OID 来请求微型端口驱动程序更新 NIC 上 (SAs) 的指定安全关联。

**注意**  NDIS 支持直接 OID 请求接口的此 OID。 有关直接 OID 请求接口的详细信息，请参阅 [NDIS 6.1 直接 Oid 请求接口](/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本 2 (IPsecOV2) 的 NDIS 6.1 微型端口驱动程序必须支持此 OID。

当微型端口驱动程序收到此请求时，驱动程序应更新 NIC 上指定的 SAs。 如果找不到 SA 或不支持 ESN，微型端口驱动程序可能会导致此请求失败。 在这种情况下，返回的状态应为 NDIS \_ 状态 \_ 无效 \_ 参数。

微型端口驱动程序接收 [**IPSEC \_ 卸载 \_ V2 \_ 更新 \_ SA**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa) 结构，该结构包含有关更新的信息，以及指向链接列表中的下一个 IPSEC \_ 卸载 \_ V2 \_ 更新 \_ sa 结构的指针。

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
<td><p>在 NDIS 6.1 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IPSEC \_ 卸载 \_ V2 \_ 更新 \_ SA**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)

 

