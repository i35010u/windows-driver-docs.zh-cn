---
title: OID_SRIOV_WRITE_VF_CONFIG_SPACE
description: 过量驱动程序会 (OID 发出对象标识符) 设置 OID_SRIOV_WRITE_VF_CONFIG_SPACE 的请求，以便将数据写入 (到指定 PCIe 虚函数) 配置空间， (网络适配器上的虚拟网络适配器。
ms.assetid: 0D9866A6-A8C6-4B0A-8D17-A632E1AE37BF
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_WRITE_VF_CONFIG_SPACE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 10addfbac2af3a6e89e8ed3797be67d38a10891e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213827"
---
# <a name="oid_sriov_write_vf_config_space"></a>OID \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间


过量驱动程序发出 (OID 的对象标识符) 设置 OID \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间，以将数据写入指定 PCIe 虚拟功能的 PCI Express (PCIe) 配置空间， (网络适配器上的 VF) 。

过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能 (PF) 的微型端口驱动程序。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS \_ SRIOV \_ 写入 \_ vf \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)结构，其中包含 VF 的 PCI 配置空间的写入操作的参数。

-   其他缓冲区空间，其中包含要写入 PCI 配置空间的数据。

<a name="remarks"></a>备注
-------

VF 微型端口驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 因此，VF 微型端口驱动程序无法直接访问硬件资源，如 VF 的 PCI 配置空间。 只有在 Hyper-v 父分区的管理操作系统中运行的 "PF" 微型端口驱动程序才能访问 VF 的 PCI 配置空间。

\_ \_ \_ \_ \_ 当 VF 微型端口驱动程序调用[**NdisMSetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)来写入 PCI 配置空间时，占用了虚拟化堆栈（如虚拟化堆栈）的 oid 集请求会发出 OID SRIOV 写入 VF 配置空间的 oid 设置请求。

当它处理 OID \_ SRIOV WRITE VF 配置空间的 oid 方法请求时 \_ \_ \_ \_ ，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由[**NDIS \_ SRIOV \_ WRITE \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)结构的**VFId**成员指定的 VF 是否包含以前分配的资源。 PF 微型端口驱动程序通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](oid-nic-switch-allocate-vf.md)的 oid 方法请求为 VF 分配资源。

    如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   PF 微型端口驱动程序调用 [**NdisMSetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata) 来写入请求的 PCI 配置空间。 但是，PF 微型端口驱动程序还可以返回该驱动程序从 PCI 配置空间的先前读取或写入操作中缓存的 VF 的 PCI 配置空间数据。

    **注意**   如果独立硬件供应商 (IHV) 提供一个虚拟总线驱动程序 (VBD) 作为其 SR-IOV[驱动程序包](../install/driver-packages.md)的一部分，则它的 PF 微型端口驱动程序不得调用[**NdisMSetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)。 相反，驱动程序必须通过专用信道与 VBD 交互，并请求该 VBD 调用 [*SetVirtualFunctionData*](/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)。 此函数从底层虚拟 PCI (VPCI) 总线驱动程序支持的 [GUID \_ VPCI \_ 接口 \_ 标准](https://msdn.microsoft.com/library/windows/hardware/hh451146) 接口公开。

     

如果 PF 微型端口驱动程序能够成功完成 OID 请求，则驱动程序必须将请求的 PCI 配置空间数据复制到[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员所引用的缓冲区。 驱动程序会将数据复制到由[**NDIS \_ SRIOV \_ READ \_ VF \_ CONFIG \_ SPACE \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构的**BufferOffset**成员指定的偏移量处的缓冲区。

有关详细信息，请参阅 [设置虚拟功能的 PCI 配置数据](./setting-the-pci-configuration-data-of-a-virtual-function.md)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间，PF 微型端口驱动程序将返回以下状态代码之一。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)"><strong>NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[GUID \_ VPCI \_ 接口 \_ 标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)

[**NdisMSetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)

[**NdisMSetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[OID \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间](oid-sriov-read-vf-config-space.md)

[*SetVirtualFunctionData*](/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)

 

