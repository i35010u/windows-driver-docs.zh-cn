---
title: OID_GEN_ISOLATION_PARAMETERS
description: NDIS 和过量驱动程序发出对象标识符 (OID) 请求 OID_GEN_ISOLATION_PARAMETERS 获取在 VM 网络适配器的端口上设置 (隔离) 参数的多租户配置。
ms.assetid: 68E89349-4907-4241-9C50-B13C75273F0D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_ISOLATION_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 07a0dd3255458ee9111bf9e0ecd42ebab1fab517
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106830"
---
# <a name="oid_gen_isolation_parameters"></a>OID \_ 代 \_ 隔离 \_ 参数


NDIS 和过量驱动程序发出对象标识符 (OID) 请求 OID \_ GEN \_ 隔离 \_ 参数，以获取 (VM 网络适配器端口上设置的隔离) 参数的多租户配置。

尽管每个路由域都在端口上单独配置，但此 OID 在单个查询中返回所有路由域的参数。

过量驱动程序应通过两个步骤发出此 OID：

1.  Io 查询所需的缓冲区大小，并将[**ndis \_ 隔离 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)结构中的**标头**成员的**大小**成员设置为**ndis \_ SIZEOF \_ ndis \_ 隔离 \_ 参数 \_ 修订版本 \_ 1**。  (参阅下面的 **NDIS \_ 状态 \_ 无效 \_ 长度** 。 ) 
2.  使用所需大小的 **InformationBuffer** 发出 OID。

如果 OID 查询请求成功完成， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区按顺序包含以下数据：

1.  [**NDIS \_ 隔离 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)结构

2.  一个或多个 [**NDIS \_ 路由 \_ 域 \_ 条目**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry) 结构，每个路由域一个

3.  一个或多个 [**NDIS \_ 路由 \_ 域 \_ 隔离 \_ 条目**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry) 结构，按路由域分组

在每个[**NDIS \_ 路由 \_ 域 \_ 条目**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)结构中， **FirstIsolationInfoEntryOffset**成员都包含从 OID 信息缓冲区开始处的偏移量 (即， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员指向的缓冲区开始) 到该路由域的第一个[**NDIS \_ 路由 \_ 域 \_ 隔离 \_ 条目**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)。 列表中最后一个结构的 **NextIsolationInfoEntryOffset** 成员中的偏移量为零。

如果未在 VM 网络适配器上设置多租户配置参数，网络适配器微型端口驱动程序将设置 **数据。查询 \_ 信息。** 将 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构的成员 BytesWritten 为零并返回 **ndis \_ 状态 \_ 成功**。 在这种情况下，数据中的数据 **。查询 \_ 信息。** 微型端口驱动程序不修改 InformationBuffer 成员。

<a name="remarks"></a>注解
-------

### <a name="return-status-codes"></a>返回状态代码

VM 网络适配器微型端口驱动程序返回此 OID 请求的以下状态代码之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区的长度太小，无法返回请求的信息。 VM 网络适配器微型端口驱动程序设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>由于其他原因，请求失败。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>在 NDIS 6.40 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 隔离 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 路由 \_ 域 \_ 条目**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)

[**NDIS \_ 路由 \_ 域 \_ 隔离 \_ 条目**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)

[**NDIS \_ 状态 \_ 隔离 \_ 参数 \_ 更改**](ndis-status-isolation-parameters-change.md)

