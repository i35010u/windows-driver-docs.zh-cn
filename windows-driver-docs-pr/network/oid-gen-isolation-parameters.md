---
title: OID_GEN_ISOLATION_PARAMETERS
description: NDIS 和过量驱动程序发出 OID_GEN_ISOLATION_PARAMETERS 的对象标识符（OID）请求，以获取在 VM 网络适配器的端口上设置的多租户配置（隔离）参数。
ms.assetid: 68E89349-4907-4241-9C50-B13C75273F0D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_ISOLATION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8601ee40be6a20a2b4fae64d0d790a2b7d96954f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844624"
---
# <a name="oid_gen_isolation_parameters"></a>OID\_代\_隔离\_参数


NDIS 和过量驱动程序发出 OID\_代\_隔离\_参数的对象标识符（OID）请求，以获取在 VM 网络适配器的端口上设置的多租户配置（隔离）参数。

尽管每个路由域都在端口上单独配置，但此 OID 在单个查询中返回所有路由域的参数。

过量驱动程序应通过两个步骤发出此 OID：

1.  Io 查询所需的缓冲区大小，并通过[**ndis\_隔离\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)结构设置为 **ndis\_SIZEOF\_ndis\_隔离来发出 OID 查询\_参数\_版本\_1**。 （请参阅下面的 " **NDIS\_状态\_无效的\_长度**。）
2.  使用所需大小的**InformationBuffer**发出 OID。

如果 OID 查询请求成功完成， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区按顺序包含以下数据：

1.  [**NDIS\_隔离\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)结构

2.  一个或多个[**NDIS\_路由\_域\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)结构，每个路由域一个

3.  一个或多个[**NDIS\_路由\_域\_隔离\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)结构，按路由域分组

在每个[**NDIS\_路由\_域\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)结构中， **FIRSTISOLATIONINFOENTRYOFFSET**成员包含 OID 信息缓冲区开始处的偏移量（即，缓冲区**的开头** [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构指向）的 ndis 成员指向该路由域的第一个[**NDIS\_路由\_域\_隔离\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)。 列表中最后一个结构的**NextIsolationInfoEntryOffset**成员中的偏移量为零。

如果未在 VM 网络适配器上设置多租户配置参数，网络适配器微型端口驱动程序将设置**数据。查询\_信息。BytesWritten** [**NDIS\_OID 的成员\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构为零并返回**NDIS\_状态\_成功**。 在这种情况下，数据中的数据 **。查询\_InformationBuffer**成员不由微型端口驱动程序修改。

<a name="remarks"></a>备注
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区的长度太小，无法返回请求的信息。 VM 网络适配器微型端口驱动程序设置<strong>数据。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小（以字节为单位）。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_隔离\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_isolation_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_路由\_域\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_entry)

[**NDIS\_路由\_域\_隔离\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_routing_domain_isolation_entry)

[**NDIS\_状态\_隔离\_参数\_更改**](ndis-status-isolation-parameters-change.md)

 

 




