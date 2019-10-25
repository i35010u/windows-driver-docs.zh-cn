---
title: OID_SRIOV_PROBED_BARS
description: NDIS 发出 OID_SRIOV_PROBED_BARS 的对象标识符（OID）查询请求，以获取网络适配器 PCI Express （PCIe）基址寄存器（条）的值。
ms.assetid: 81C3A5B5-58D5-41F4-A000-79F3F4E00DAD
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_PROBED_BARS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fc31e0c4e6696ca67e74b1736cdb2b6002811865
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843985"
---
# <a name="oid_sriov_probed_bars"></a>OID\_SRIOV\_探测的\_条


NDIS 发出 OID\_SRIOV\_\_探测的对象标识符（OID）查询请求，以获取网络适配器 PCI Express （PCIe）基址寄存器（条）的值。 此函数返回由 PCI bus 驱动程序执行的查询之后网络适配器报告的条形值。 此查询确定网络适配器所需的内存或 i/o 地址空间。

NDIS 发出 oid\_SRIOV 的 OID 查询请求\_将\_条探测到网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要此 OID 查询请求。

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS\_SRIOV\_探测了\_条\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)结构，其中包含对网络适配器的 PCI 栏进行读取操作的参数。

-   PCIe 网络适配器每个栏的 ULONG 值的数组。 此数组中的元素的最大数目为 PCI\_TYPE0\_地址。

<a name="remarks"></a>备注
-------

PCI 总线驱动程序在 Hyper-v 父分区的管理操作系统中运行，它查询网络适配器的每个 PCI 基址寄存器（BAR）的内存或 i/o 地址空间要求。 PCI 总线驱动程序在第一次检测总线上的适配器时执行此查询。

通过此 PCI BAR 查询，PCI 总线驱动程序将确定以下各项：

-   网络适配器是否支持 PCI BAR。

-   如果支持一个条，则条需要多少内存或 i/o 地址空间。

虚拟 PCI （VPCI）总线驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 PCI Express （PCIe）虚拟功能（VF）附加到子分区时，VPCI bus 驱动程序将公开用于 VF （*vf 网络适配器*）的虚拟网络适配器。 在执行此之前，VPCI bus 驱动程序必须执行 PCI BAR 查询来确定 VF 网络适配器所需的内存或地址空间。

由于对 PCI 配置空间的访问是一项特权操作，因此它只能由 Hyper-v 父分区的管理操作系统中运行的组件执行。 当 VPCI 总线驱动程序查询 PCI 条时，NDIS 会发出 oid\_SRIOV 的 OID 查询请求，\_探测到 PF 微型端口驱动程序\_条。 此 OID 查询请求返回的结果将转发到 VPCI 总线驱动程序，以便它可以确定 VF 网络适配器所需的内存地址空间量。

**请注意**  OID\_SRIOV 的 oid 请求\_探测的\_条只能由 NDIS 发出。 OID 请求不得由过量驱动程序发出，如筛选器驱动程序的协议。

 

\_探测的 OID\_SRIOV 探测的\_条查询请求包含\_INFO 结构\_探测到的[**NDIS\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info) 。 当 PF 微型端口驱动程序处理此 OID 时，驱动程序必须在由 NDIS\_SRIOV 的**BaseRegisterValuesOffset**成员引用的数组中返回 PCI BAR 值， **\_探测的\_条\_信息**结构。 对于数组中的每个偏移量，PF 微型端口驱动程序必须将数组元素设置为位于物理适配器 PCI 配置空间内相同偏移量的条的 ULONG 值。

驱动程序返回的每个条形值的值都必须与在管理操作系统中运行的 PCI 驱动程序执行的 PCI BAR 查询遵循的值相同。 PF 微型端口驱动程序可以调用[**NdisMQueryProbedBars**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars)来确定此信息。

有关 PCI 设备条的详细信息，请参阅*Pci 本地总线规范*。

有关如何查询用于 VF 的 PCI BAR 注册的详细信息，请参阅[查询虚拟功能的 Pci 基址寄存器](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-base-address-registers-of-a-virtual-function)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 OID\_SRIOV\_探测的\_条返回以下状态代码之一：

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区小于（sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>） + PCI_TYPE0_ADDRESSES）。 PF 微型端口驱动程序必须设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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

[ **\_探测的 NDIS\_SRIOV\_条\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)

[**NdisMQueryProbedBars**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars)

 

 




