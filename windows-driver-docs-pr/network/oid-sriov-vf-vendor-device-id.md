---
title: OID_SRIOV_VF_VENDOR_DEVICE_ID
description: 过量驱动程序发出 OID_SRIOV_VF_VENDOR_DEVICE_ID 的对象标识符（OID）方法请求，以查询 pci express （pcie）虚拟功能（VF）网络适配器的 PCI Express （PCIe）设备标识符（DeviceID）和供应商标识符（VendorID）。 此虚拟网络适配器在附加到 VF 的 Hyper-v 子分区中公开。过量驱动程序将此 OID 方法请求发送到网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。
ms.assetid: 19D98264-325B-4EA4-83BF-BBFECD185E55
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_VENDOR_DEVICE_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 731513521e7e5a9d41c0addd9560bdfc5fa7bcef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843971"
---
# <a name="oid_sriov_vf_vendor_device_id"></a>OID\_SRIOV\_VF\_供应商\_设备\_ID


过量驱动程序发出 OID\_SRIOV\_VF 的对象标识符（OID）方法请求\_供应商\_设备\_ID 查询 pci express （PCIe）设备标识符（DeviceID）和供应商标识符（VendorID）PCIe虚函数（VF）网络适配器。 此虚拟网络适配器在附加到 VF 的 Hyper-v 子分区中公开。

过量驱动程序将此 OID 方法请求发送到网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SRIOV\_VF\_供应商\_设备\_ID\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)结构的指针。

<a name="remarks"></a>备注
-------

在发出此 OID 方法请求之前，过量驱动程序必须[ **\_供应商\_设备\_ID\_INFO 结构\_初始化 NDIS\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info) ，并且必须将**VFId**成员设置为 VF 的标识符要从其读取信息的。

当它处理此 OID 请求时，PF 微型端口驱动程序必须验证指定的 VF 是否包含以前分配的资源。 在 oid 的 OID 方法请求中，PF 微型端口驱动程序为一个 VF 分配资源[\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

有关详细信息，请参阅[查询 PCI 供应商和虚拟函数的设备标识符](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID\_SRIOV\_VF\_供应商\_设备\_ID，PF 小型端口驱动程序返回以下状态代码之一。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)"><strong>NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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

[**NDIS\_SRIOV\_VF\_供应商\_设备\_ID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

 

 




