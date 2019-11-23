---
title: OID_SRIOV_WRITE_VF_CONFIG_SPACE
description: 过量驱动程序发出 OID_SRIOV_WRITE_VF_CONFIG_SPACE 的对象标识符（OID）设置请求，以将数据写入到网络适配器上指定 PCIe 虚拟功能（VF）的 PCI Express （PCIe）配置空间。
ms.assetid: 0D9866A6-A8C6-4B0A-8D17-A632E1AE37BF
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_WRITE_VF_CONFIG_SPACE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5745d1c52d5763e7cdacefec65101fba0f99ec8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843968"
---
# <a name="oid_sriov_write_vf_config_space"></a>OID\_SRIOV\_写入\_VF\_配置\_空间


过量驱动程序发出 OID\_的对象标识符（OID）设置请求\_写入\_VF\_配置\_空间，将数据写入到网络适配器上指定 PCIe 虚拟功能（VF）的 PCI Express （PCIe）配置空间。

过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS\_SRIOV\_写入\_vf\_配置\_空间\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)包含 VF 的 PCI 配置空间写入操作参数的参数结构。

-   其他缓冲区空间，其中包含要写入 PCI 配置空间的数据。

<a name="remarks"></a>备注
-------

VF 微型端口驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 因此，VF 微型端口驱动程序无法直接访问硬件资源，如 VF 的 PCI 配置空间。 只有在 Hyper-v 父分区的管理操作系统中运行的 "PF" 微型端口驱动程序才能访问 VF 的 PCI 配置空间。

占用大量的驱动程序（例如虚拟化堆栈）发出 oid\_SRIOV 的 OID 集请求\_在 VF 微型端口驱动程序调用[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)写入其 PCI 配置空间时，\_配置\_空间写入\_vf。

当处理 OID\_SRIOV 的 OID 方法请求时\_写入\_VF\_配置\_空间，则 PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 NDIS\_SRIOV 的**VFId**成员指定的 VF [ **\_写入\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)结构是否包含之前已有的资源分配. PF 微端口驱动程序通过 oid 的 oid 方法请求为 VF 分配资源[\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

    如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   PF 微型端口驱动程序调用[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)来写入请求的 PCI 配置空间。 但是，PF 微型端口驱动程序还可以返回该驱动程序从 PCI 配置空间的先前读取或写入操作中缓存的 VF 的 PCI 配置空间数据。

    **请注意**  如果独立硬件供应商（IHV）提供了虚拟总线驱动程序（VBD）作为其 sr-iov[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)的一部分，则它的 PF 微型端口驱动程序不得调用[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)。 相反，驱动程序必须通过专用信道与 VBD 交互，并请求该 VBD 调用[*SetVirtualFunctionData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)。 此函数由基础虚拟 PCI （VPCI）总线驱动程序所支持的[GUID\_VPCI\_接口\_标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)接口公开。

     

如果 PF 微型端口驱动程序能够成功完成 OID 请求，则驱动程序必须将所请求的 PCI 配置空间数据复制到[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员引用的缓冲区. 该驱动程序会将数据复制到 NDIS\_SRIOV 的**BufferOffset**成员指定的偏移量处的缓冲区， [ **\_读取\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构。

有关详细信息，请参阅[设置虚拟功能的 PCI 配置数据](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-pci-configuration-data-of-a-virtual-function)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序返回 OID\_SRIOV 的 OID 集的以下状态代码之一\_写入\_VF\_配置\_空间。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)"><strong>NDIS_SRIOV_WRITE_VF_CONFIG_SPACE_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据。SET_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[GUID\_VPCI\_INTERFACE\_STANDARD](https://msdn.microsoft.com/library/windows/hardware/hh451146)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_写入\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)

[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)

[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_读取\_VF\_配置\_空间](oid-sriov-read-vf-config-space.md)

[*SetVirtualFunctionData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)

 

 




