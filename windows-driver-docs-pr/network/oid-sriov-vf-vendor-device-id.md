---
title: OID_SRIOV_VF_VENDOR_DEVICE_ID
description: 过量驱动程序发出对象标识符 (OID) 方法请求 OID_SRIOV_VF_VENDOR_DEVICE_ID，以查询 pci express) PCIe (的的 (PCIe) 的设备标识符 (VendorID)  ()  此虚拟网络适配器在附加到 VF 的 Hyper-v 子分区中公开。过量驱动程序将此 OID 方法请求发送到 PCI Express (PCIe 的微型端口驱动程序) 物理功能 (PF) 网络适配器。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。
ms.assetid: 19D98264-325B-4EA4-83BF-BBFECD185E55
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_VENDOR_DEVICE_ID 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 38d3f7b6bf5308a413ead41ac88de98857ef8fa8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106852"
---
# <a name="oid_sriov_vf_vendor_device_id"></a>OID \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID


过量驱动程序会发出对象标识符 (oid) 方法请求 OID \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID，以查询 pci express (Pcie) 设备标识符 (DeviceID) 和供应商标识符 (的 此虚拟网络适配器在附加到 VF 的 Hyper-v 子分区中公开。

过量驱动程序将此 OID 方法请求发送到 PCI Express (PCIe 的微型端口驱动程序) 物理功能 (PF) 网络适配器。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)结构的指针。

<a name="remarks"></a>备注
-------

在发出此 OID 方法请求之前，过量驱动程序必须初始化 [**NDIS \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info) 结构，并且必须将 **VFID** 成员设置为要从中读取信息的 VF 的标识符。

当它处理此 OID 请求时，PF 微型端口驱动程序必须验证指定的 VF 是否包含以前分配的资源。 在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](oid-nic-switch-allocate-vf.md)的 oid 方法请求期间，PF 微型端口驱动程序为 VF 分配资源。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

有关详细信息，请参阅 [查询 PCI 供应商和虚拟函数的设备标识符](./querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function.md)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID 的 oid 方法请求，PF 微型端口驱动程序返回以下状态代码之一。

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
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)"><strong>NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

[**NDIS \_ SRIOV \_ VF \_ 供应商 \_ 设备 \_ ID \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

