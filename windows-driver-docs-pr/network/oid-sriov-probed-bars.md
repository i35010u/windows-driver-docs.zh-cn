---
title: OID_SRIOV_PROBED_BARS
description: NDIS (OID 发出对象标识符) 查询请求 OID_SRIOV_PROBED_BARS 获取网络适配器 PCI Express (PCIe) 基址寄存器 () 的值。
ms.assetid: 81C3A5B5-58D5-41F4-A000-79F3F4E00DAD
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_PROBED_BARS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e8414f0472931a2cc28ea8a188f941f9e9bbcc98
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105588"
---
# <a name="oid_sriov_probed_bars"></a>OID \_ SRIOV \_ 探测的 \_ 条


NDIS)  (OID 发出对象标识符，查询 OID SRIOV 已探测条的请求， \_ \_ \_ 以获取网络适配器 PCI Express (PCIe 的值) 基址寄存器 () 。 此函数返回由 PCI bus 驱动程序执行的查询之后网络适配器报告的条形值。 此查询确定网络适配器所需的内存或 i/o 地址空间。

NDIS \_ \_ \_ 向网络适配器的 PCIe 物理功能 (PF) 的微型端口驱动程序发出 oid 查询请求。 对于支持 (SR-IOV) 接口的单个根 i/o 虚拟化的 PF 微型端口驱动程序，需要此 OID 查询请求。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   一种 [**NDIS \_ SRIOV \_ 探测 \_ 条 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info) 结构，其中包含对网络适配器的 PCI 条上的读取操作的参数。

-   PCIe 网络适配器每个栏的 ULONG 值的数组。 此数组中的最大元素数为 PCI \_ TYPE0 \_ 地址。

<a name="remarks"></a>注解
-------

PCI 总线驱动程序在 Hyper-v 父分区的管理操作系统中运行，它查询网络适配器) 的每个 PCI 基址寄存器 (的内存或 i/o 地址空间要求。 PCI 总线驱动程序在第一次检测总线上的适配器时执行此查询。

通过此 PCI BAR 查询，PCI 总线驱动程序将确定以下各项：

-   网络适配器是否支持 PCI BAR。

-   如果支持一个条，则条需要多少内存或 i/o 地址空间。

虚拟 PCI (VPCI) 总线驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 当 PCI Express (PCIe) 虚函数 (VF) 附加到子分区时，VPCI bus 驱动程序将为 VF (*vf 网络适配器*) 公开虚拟网络适配器。 在执行此之前，VPCI bus 驱动程序必须执行 PCI BAR 查询来确定 VF 网络适配器所需的内存或地址空间。

由于对 PCI 配置空间的访问是一项特权操作，因此它只能由 Hyper-v 父分区的管理操作系统中运行的组件执行。 当 VPCI 总线驱动程序查询 PCI 条时，NDIS 会 \_ \_ \_ 向 PF 小型端口驱动程序发出 oid SRIOV 探测条的 oid 查询请求。 此 OID 查询请求返回的结果将转发到 VPCI 总线驱动程序，以便它可以确定 VF 网络适配器所需的内存地址空间量。

**注意**   OID \_ SRIOV 探测条的 oid 请求 \_ \_ 只能由 NDIS 发出。 OID 请求不得由过量驱动程序发出，如筛选器驱动程序的协议。

 

OID \_ SRIOV \_ 探测的 \_ 条查询请求包含 [**NDIS \_ SRIOV \_ 探测 \_ 条 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info) 结构。 当 PF 微型端口驱动程序处理此 OID 时，驱动程序必须返回由**NDIS \_ SRIOV \_ 探测 \_ 条 \_ 信息**结构的**BASEREGISTERVALUESOFFSET**成员引用的数组中的 PCI BAR 值。 对于数组中的每个偏移量，PF 微型端口驱动程序必须将数组元素设置为位于物理适配器 PCI 配置空间内相同偏移量的条的 ULONG 值。

驱动程序返回的每个条形值的值都必须与在管理操作系统中运行的 PCI 驱动程序执行的 PCI BAR 查询遵循的值相同。 PF 微型端口驱动程序可以调用 [**NdisMQueryProbedBars**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars) 来确定此信息。

有关 PCI 设备条的详细信息，请参阅 *Pci 本地总线规范*。

有关如何查询用于 VF 的 PCI BAR 注册的详细信息，请参阅 [查询虚拟功能的 Pci 基址寄存器](./querying-the-pci-base-address-registers-of-a-virtual-function.md)。

### <a name="return-status-codes"></a>返回状态代码

PF 小型端口驱动程序为 OID SRIOV 探测的栏的查询请求返回以下状态代码之一 \_ \_ \_ ：

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
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF 微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区小于 (sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>) + PCI_TYPE0_ADDRESSES) 。 PF 微型端口驱动程序必须设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ SRIOV \_ 探测 \_ 条 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)

[**NdisMQueryProbedBars**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars)

