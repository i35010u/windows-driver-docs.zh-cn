---
title: OID_TCP_RSC_STATISTICS
description: 作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID_TCP_RSC_STATISTICS OID 来获取微型端口适配器的接收段合并（RSC）统计信息。
ms.assetid: CD289868-1925-4222-8A4D-359118124325
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_RSC_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d23634c0cb6ff59b4a01583bc7d33d0fce5c2561
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843899"
---
# <a name="oid_tcp_rsc_statistics"></a>OID\_TCP\_RSC\_统计信息


作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID\_TCP\_RSC\_STATISTICS OID 来获取微型端口适配器的接收段合并（RSC）统计信息。

提供 RSC 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个[**ndis\_RSC\_STATISTICS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)结构。

微型端口驱动程序必须在[**NDIS\_RSC\_统计信息\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)结构的成员中维护统计信息，如下所示：

-   每次向单个合并的单元（SCU）添加数据包时，驱动程序必须在**CoalescedPkts**成员中递增合并的数据包计数。
-   每次将数据包添加到 SCU 时，驱动程序必须在**CoalescedOctets**成员中递增每个数据包的 TCP 负载大小。
-   每次完成 SCU 时，驱动程序必须将合并的事件计数**CoalesceEvents**成员递增1。 所有此类 SCUs 应有一个非零的**CoalescedSegCount**值。
-   驱动程序必须在每次遇到不超过 IP 数据报长度的异常**时，将中止成员中**的中止计数递增1。 此计数应包括由于硬件资源未合并数据包的情况。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_RSC\_统计信息\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rsc_statistics_info)

 

 




