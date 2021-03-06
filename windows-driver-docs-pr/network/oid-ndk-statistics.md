---
title: OID_NDK_STATISTICS
description: 作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID_NDK_STATISTICS OID 来获取微型端口适配器的 NDK 统计信息。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_STATISTICS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dec3338f253dafb3e7ae3a746e5cd3a92534684b
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248577"
---
# <a name="oid_ndk_statistics"></a>OID \_ NDK \_ 统计信息


作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID \_ NDK \_ statistics OID 来获取微型端口适配器的 NDK 统计信息。

提供 NDK 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

**注意**  NDIS 支持直接 OID 请求接口的此 OID。 有关直接 OID 请求接口的详细信息，请参阅 [NDIS 6.1 直接 Oid 请求接口](/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

NDIS 使用指向 [**ndis \_ NDK \_ 统计 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)结构的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员颁发此 OID。

支持 NDK 的微型端口驱动程序必须提供 **CounterSet** 成员，这是一个 [**NDIS \_ NDK \_ 性能 \_ 计数器**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters) 结构。

计数器将发布到 [perfmon](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731067(v=ws.11)) (的工具中，请参阅 " [NetworkDirect 活动](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997022(v=ws.11)) 性能计数器") ，并使用性能数据助手 (PDH) 和性能库 (PERFLIB) 编程接口以编程方式提供。 有关这些接口的详细信息，请参阅 [性能计数器](/windows/desktop/PerfCtrs/performance-counters-portal)。

还可以通过使用 **RdmaStatistics** 属性调用 NetAdapterStatistics PowerShell Cmdlet 来 [获取](/powershell/module/netadapter/get-netadapterstatistics)这些计数器。 有关 **RdmaStatistics** 属性的详细信息，请参阅 [**MSFT \_ NetAdapterStatisticsSettingData**](/previous-versions/windows/desktop/netadaptercimprov/msft-netadapterstatisticssettingdata)。

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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[内核模式性能监视](../devtest/kernel-mode-performance-monitoring.md)

[**NDIS \_ NDK \_ 性能 \_ 计数器**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_performance_counters)

[**NDIS \_ NDK \_ 统计 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_statistics_info)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

 

