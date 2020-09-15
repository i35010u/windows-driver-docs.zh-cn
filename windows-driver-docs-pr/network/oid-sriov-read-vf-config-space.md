---
title: OID_SRIOV_READ_VF_CONFIG_SPACE
description: 过量驱动程序) 方法请求 (OID 发出对象标识符，OID_SRIOV_READ_VF_CONFIG_SPACE 从 PCI Express (PCIe) 配置空间读取网络适配器上指定 PCIe 虚函数 (VF) 的数据。
ms.assetid: 48CD54F5-F18F-4BC1-A93A-A824EC041605
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_READ_VF_CONFIG_SPACE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 68fcb57720974e7422742e9e3bcb7988306aa4d4
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105526"
---
# <a name="oid_sriov_read_vf_config_space"></a>OID \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间


过量驱动程序发出 (oid 的对象标识符) 方法请求 OID， \_ \_ 读取 \_ VF \_ 配置 \_ 空间以便从 PCI Express (PCIe) 配置空间读取网络适配器上指定 PCIe 虚函数 (VF) 的数据。

成功从此 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS \_ SRIOV \_ 读取 \_ vf \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构，其中包含 VF 的 PCI 配置空间读取操作的参数。

-   要从 PCI 配置空间读取的数据的额外缓冲区空间。

<a name="remarks"></a>注解
-------

VF 微型端口驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 因此，VF 微型端口驱动程序无法直接访问硬件资源，如 VF 的 PCI 配置空间。 只有 PCIe 物理功能 (PF) 的微型端口驱动程序可以访问 VF 的 PCI 配置空间。 PF 微型端口驱动程序在 Hyper-v 父分区的管理操作系统中运行，并具有对 VF 资源的特权访问权限。

若要读取 VF PCI 配置空间，在管理操作系统中运行的过量驱动程序会发出 OID SRIOV 的 OID 方法请求 \_ \_ \_ \_ \_ 。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

例如，在管理操作系统中运行的虚拟化堆栈发出 oid 方法请求： \_ \_ \_ \_ \_ 当 VF 微型端口驱动程序调用 [**NdisMGetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata) 从其 VF PCI 配置空间读取时，SRIOV 读取 VF 配置空间。

当它处理 OID \_ SRIOV READ VF 配置空间的 oid 方法请求时 \_ \_ \_ \_ ，PF 微型端口驱动程序必须遵循以下准则：

-   微型端口驱动程序必须验证由[**NDIS \_ SRIOV \_ \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)的**VFId**成员指定的 vf 是否具有以前分配的资源。 微型端口驱动程序通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](oid-nic-switch-allocate-vf.md)的 oid 方法请求为 VF 分配资源。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   微型端口驱动程序必须验证 ([**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)) 结构的**InformationBuffer**成员引用的缓冲区是否足够大，以便返回请求的 PCIe 配置空间数据。 如果不是这样，则驱动程序必须使 OID 请求失败。
-   小型端口驱动程序通常会调用 [**NdisMGetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata) 来查询请求的 PCIe 配置空间。 但是，微型端口驱动程序还可以返回该程序已缓存的 VF 配置空间的配置空间数据。

    **注意**   如果独立硬件供应商 (IHV) 提供 (的 VBD) 作为其 SR-IOV[驱动程序包](../install/driver-packages.md)的一部分的虚拟总线驱动程序，则其微型端口驱动程序不得调用[**NdisMGetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)。 相反，驱动程序必须通过专用信道与 VBD 交互，并请求该 VBD 调用 [*ReadVfConfigBlock*](/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))。 此函数从底层虚拟 PCI (VPCI) 总线驱动程序支持的 [GUID \_ VPCI \_ 接口 \_ 标准](https://msdn.microsoft.com/library/windows/hardware/hh451146) 接口公开。

     

如果 PF 微型端口驱动程序能够成功完成 OID 请求，则驱动程序必须将请求的 PCI 配置空间数据复制到[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员所引用的缓冲区。 该驱动程序会将数据复制到由[**NDIS \_ SRIOV \_ READ \_ VF \_ CONFIG \_ SPACE \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构的**BufferOffset**成员指定的偏移量处的缓冲区。

有关详细信息，请参阅 [查询虚拟功能的 PCI 配置数据](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-configuration-data-of-a-virtual-function)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 OID \_ SRIOV \_ READ \_ VF \_ 配置 \_ 空间的 oid 方法请求返回以下状态代码之一。

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
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_READ_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)"><strong>NDIS_SRIOV_READ_VF_CONFIG_SPACE_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 微型端口驱动程序必须设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

## <a name="see-also"></a>请参阅


****
[GUID \_ VPCI \_ 接口 \_ 标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)

[**NdisMGetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)

[**NdisMGetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[*ReadVfConfigBlock*](/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))

