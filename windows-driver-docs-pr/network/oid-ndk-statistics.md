---
title: OID_NDK_STATISTICS
description: 作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID_NDK_STATISTICS OID 来获取微型端口适配器的 NDK 统计信息。
ms.assetid: 30F16DEC-AEE6-49D4-8599-95374ACBD446
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_STATISTICS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 24373920041a5b176ec6036f37458e07582d95b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844102"
---
# <a name="oid_ndk_statistics"></a>OID\_NDK\_统计信息


作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID\_NDK\_STATISTICS OID 来获取微型端口适配器的 NDK 统计信息。

提供 NDK 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

**请注意**  通过直接 OID 请求接口，NDIS 支持此 oid。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 Oid 请求接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

NDIS 使用[**ndis\_oid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)的**InformationBuffer**成员向此 oid 发出\_请求结构指向[**NDIS\_NDK\_NDK\_统计信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)结构。

支持 NDK 的微型端口驱动程序必须提供**CounterSet**成员，这是一个[**NDIS\_NDK\_性能\_计数器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters)结构。

计数器将发布到[perfmon](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731067(v=ws.11))等工具（请参阅[NetworkDirect 活动](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997022(v=ws.11))性能计数器），并使用性能数据助手（PDH）和性能库（PERFLIB）编程接口以编程方式提供。 有关这些接口的详细信息，请参阅[性能计数器](https://docs.microsoft.com/windows/desktop/PerfCtrs/performance-counters-portal)。

还可以通过使用**RdmaStatistics**属性调用 NetAdapterStatistics PowerShell Cmdlet 来[获取](https://docs.microsoft.com/powershell/module/network-adapter/get-netadapterstatistics)这些计数器。 有关**RdmaStatistics**属性的详细信息，请参阅[**MSFT\_NetAdapterStatisticsSettingData**](https://docs.microsoft.com/previous-versions/windows/desktop/netadaptercimprov/msft-netadapterstatisticssettingdata)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>无受支持的版本</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
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


[内核模式性能监视](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-mode-performance-monitoring)

[**NDIS\_NDK\_性能\_计数器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters)

[**NDIS\_NDK\_统计信息\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




