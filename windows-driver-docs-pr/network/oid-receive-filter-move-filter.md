---
title: OID_RECEIVE_FILTER_MOVE_FILTER
description: 过量驱动程序发出 OID_RECEIVE_FILTER_MOVE_FILTER 的对象标识符（OID）设置请求，以移动以前配置的接收筛选器。
ms.assetid: CC899ABD-EE6B-4932-889F-984C8B5A403F
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_MOVE_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 13a1043f27bc4dfbfd91e24cadcf381c3de5c433
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844005"
---
# <a name="oid_receive_filter_move_filter"></a>OID\_接收\_筛选器\_移动\_筛选器


过量驱动程序发出 OID\_接收\_筛选器的对象标识符（OID）设置请求，\_移动\_筛选器以移动以前配置的接收筛选器。 接收筛选器将从一个虚拟端口（VPort）移动到另一个 VPort。

过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 支持单一根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要此 OID 集请求。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)的指针\_\_参数结构移动\_筛选器。

<a name="remarks"></a>备注
-------

NDIS 验证[**ndis\_接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)的成员\_在将 OID 集请求转发到 PF 微型端口驱动程序之前，\_筛选器\_参数结构。

PF 微型端口驱动程序必须以原子方式处理此 OID 集请求。 驱动程序必须能够将网络适配器配置为同时从接收队列和 VPort 中删除筛选器，并将其设置在不同的接收队列和 VPort 中。

有关详细信息，请参阅将[接收筛选器移动到虚拟端口](https://docs.microsoft.com/windows-hardware/drivers/network/moving-a-receive-filter-to-a-virtual-port)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序将为 oid\_接收\_筛选器返回以下状态代码之一，\_移动\_筛选器。

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
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF 微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"><strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"><strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong></a>）。 PF 微型端口驱动程序必须设置<strong>数据。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_筛选器\_移动\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)

 

 




