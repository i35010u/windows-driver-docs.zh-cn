---
title: OID_TCP_RSC_STATISTICS
description: 作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID_TCP_RSC_STATISTICS OID 来获取 (RSC) 小型端口适配器统计信息的接收段合并。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_RSC_STATISTICS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0107f8116dd298b729a421a0d4a01cd0cbdfb6a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791383"
---
# <a name="oid_tcp_rsc_statistics"></a>OID \_ TCP \_ RSC \_ 统计信息


作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID \_ TCP \_ RSC \_ STATISTICS OID 获取接收段合并， (RSC) 小型端口适配器的统计信息。

提供 RSC 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含 [**ndis \_ RSC \_ 统计 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)结构。

微型端口驱动程序必须在 [**NDIS \_ RSC \_ 统计 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info) 结构的成员中维护统计信息，如下所示：

-   每次将数据包添加到单个合并的单元 (SCU) 时，驱动程序必须在 **CoalescedPkts** 成员中递增合并的数据包计数。
-   每次将数据包添加到 SCU 时，驱动程序必须在 **CoalescedOctets** 成员中递增每个数据包的 TCP 负载大小。
-   每次完成 SCU 时，驱动程序必须将合并的事件计数 **CoalesceEvents** 成员递增1。 所有此类 SCUs 应有一个非零的 **CoalescedSegCount** 值。
-   驱动程序必须在每次遇到不超过 IP 数据报长度的异常 **时，将中止成员中** 的中止计数递增1。 此计数应包括由于硬件资源未合并数据包的情况。

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
<td><p>Windows 8 中的 NDIS 6.30 和更高版本驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ RSC \_ 统计 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)

 

