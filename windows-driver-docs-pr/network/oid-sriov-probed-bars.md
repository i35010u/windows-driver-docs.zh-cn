---
title: OID_SRIOV_PROBED_BARS
description: NDIS 发出一个对象标识符 (OID) 查询请求的 OID_SRIOV_PROBED_BARS 以获得的网络适配器的 PCI Express (PCIe) 基本地址注册 （条形图） 的值。
ms.assetid: 81C3A5B5-58D5-41F4-A000-79F3F4E00DAD
ms.date: 08/08/2017
keywords: -OID_SRIOV_PROBED_BARS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 27f0aa9c863d7ca8977936c40f6669ba7db3826b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556082"
---
# <a name="oidsriovprobedbars"></a>OID\_SRIOV\_PROBED\_条


NDIS 发出对象标识符 (OID) 查询请求的 OID\_SRIOV\_PROBED\_条以获得的网络适配器的 PCI Express (PCIe) 基本地址注册 （条形图） 的值。 此函数返回报告的网络适配器的遵循 PCI 总线驱动程序执行的查询的栏值。 此查询确定内存或网络适配器所需的 I/O 地址空间。

NDIS 发出 OID 查询请求的 OID\_SRIOV\_PROBED\_微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF) 到图条。 支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序需要此 OID 查询请求。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_SRIOV\_PROBED\_条\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451679)结构，其中包含一个网络 PCI 条形图上的读操作的参数适配器。

-   PCIe 网络适配器的每个条形的 ULONG 值的数组。 此数组中元素的最大数目是 PCI\_TYPE0\_地址。

<a name="remarks"></a>备注
-------

PCI 总线驱动程序，它运行在管理操作系统的 HYPER-V 父分区中，查询的内存或 I/O 地址空间的要求的每个 PCI 基本注册 （的地址栏） 的网络适配器。 PCI 总线驱动程序第一次检测到总线上的适配器时执行此查询。

PCI 栏此查询中，通过 PCI 总线驱动程序确定：

-   无论网络适配器是否支持 PCI 栏。

-   如果支持一个栏，则是栏需要多少内存或 I/O 地址空间。

在 HYPER-V 子分区的来宾操作系统中运行虚拟 PCI (VPCI) 总线驱动程序。 PCI Express (PCIe) 虚拟函数 (VF) 附加到子分区，VPCI 总线驱动程序将为取景器公开的虚拟网络适配器 (*VF 网络适配器*)。 它执行此操作之前，VPCI 总线驱动程序必须执行 PCI 栏查询以确定所需的内存或 VF 网络适配器所需的地址空间。

由于对 PCI 配置空间的访问是一项特权的操作，只能由管理操作系统的 HYPER-V 父分区中运行的组件执行。 NDIS 当 VPCI 总线驱动程序查询 PCI 条时，发出 OID 查询请求的 OID\_SRIOV\_PROBED\_条到 PF 微型端口驱动程序。 此 OID 查询请求返回的结果将转发到 VPCI 总线驱动程序，以便它可以确定需要多少内存地址空间 VF 网络适配器。

**请注意**  OID 请求的 OID\_SRIOV\_PROBED\_条只可发出由 NDIS。 OID 请求并非必须由基础驱动程序，例如筛选器驱动程序的协议颁发。

 

OID\_SRIOV\_PROBED\_条查询请求包含[ **NDIS\_SRIOV\_PROBED\_条\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451679)结构。 当 PF 微型端口驱动程序处理此 OID 时，则驱动程序必须返回引用的数组中的 PCI 栏值**BaseRegisterValuesOffset**的成员**NDIS\_SRIOV\_PROBED\_条\_信息**结构。 每个数组内的偏移量，PF 微型端口驱动程序必须设置为在相同物理适配器的 PCI 配置空间内的偏移量的栏的 ULONG 值的数组元素。

每个条由驱动程序返回的值必须是将遵循 PCI 条查询，因为由管理操作系统中运行的 PCI 驱动程序执行的相同值。 PF 微型端口驱动程序可以调用[ **NdisMQueryProbedBars** ](https://msdn.microsoft.com/library/windows/hardware/hh451520)来确定此信息。

有关 PCI 设备的条形图的详细信息，请参阅*PCI 本地总线规范*。

有关如何查询 VF PCI 栏寄存器的详细信息，请参阅[查询 PCI 基本地址注册的虚拟函数](https://msdn.microsoft.com/library/windows/hardware/hh440182)。

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序将返回一个 OID 的查询请求的以下状态代码\_SRIOV\_PROBED\_条：

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
<td><p>PF 微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451679" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451679)"> <strong>NDIS_SRIOV_PROBED_BARS_INFO</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区小于 (sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451679" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451679)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>) + PCI_TYPE0_ADDRESSES)。 PF 微型端口驱动程序必须设置<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>请求由于其他原因而失败。</p></td>
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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_PROBED\_条\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451679)

[**NdisMQueryProbedBars**](https://msdn.microsoft.com/library/windows/hardware/hh451520)

 

 




