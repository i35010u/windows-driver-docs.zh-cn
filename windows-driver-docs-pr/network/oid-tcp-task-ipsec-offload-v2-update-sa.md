---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA
description: 作为集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA OID 来请求微型端口驱动程序更新 NIC 上的指定安全关联（Sa）。
ms.assetid: 22849103-9148-4621-b78f-b9f34f2c7ac1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a11b334360a2028f0d6342b2097e96750f0fbad0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843884"
---
# <a name="oid_tcp_task_ipsec_offload_v2_update_sa"></a>OID\_TCP\_任务\_IPSEC\_卸载\_V2\_更新\_SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组设置，TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_更新\_SA OID 来请求微型端口驱动程序更新 NIC 上的指定安全关联（SAs）。

**请注意**  通过直接 OID 请求接口，NDIS 支持此 oid。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 Oid 请求接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本2（IPsecOV2）的 NDIS 6.1 微型端口驱动程序必须支持此 OID。

当微型端口驱动程序收到此请求时，驱动程序应更新 NIC 上指定的 SAs。 如果找不到 SA 或不支持 ESN，微型端口驱动程序可能会导致此请求失败。 在这种情况下，返回的状态应为 NDIS\_状态\_无效\_参数。

微型端口驱动程序接收[**IPSEC\_卸载\_V2\_UPDATE\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)结构，该结构包含有关更新的信息，以及指向下一个 IPSEC\_卸载\_V2\_链接列表中的结构。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IPSEC\_卸载\_V2\_更新\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)

 

 




