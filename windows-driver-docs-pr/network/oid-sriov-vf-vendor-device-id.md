---
title: OID_SRIOV_VF_VENDOR_DEVICE_ID
description: 基础驱动程序发出的对象标识符 (OID) 方法请求 OID_SRIOV_VF_VENDOR_DEVICE_ID 的查询的 PCI Express (PCIe) 设备标识符 (DeviceID) 和 PCI Express (PCIe) 的虚拟函数 (VF) 网络适配器供应商标识符 (VendorID)。 此虚拟网络适配器附加到 VF HYPER-V 子分区中公开。基础驱动程序微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的网络适配器向颁发此 OID 方法请求。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。
ms.assetid: 19D98264-325B-4EA4-83BF-BBFECD185E55
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_VENDOR_DEVICE_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6ce3875d1b5986a9d5a2c0c901cdb9c471010acb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373891"
---
# <a name="oidsriovvfvendordeviceid"></a>OID\_SRIOV\_VF\_VENDOR\_DEVICE\_ID


基础驱动程序发出的 OID 的对象标识符 (OID) 方法请求\_SRIOV\_VF\_供应商\_设备\_要查询的 PCI Express (PCIe) 设备标识符 (DeviceID) 和供应商 IDPCI Express (PCIe) 的虚拟函数 (VF) 网络适配器的标识符 (VendorID)。 此虚拟网络适配器附加到 VF HYPER-V 子分区中公开。

基础驱动程序微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的网络适配器向颁发此 OID 方法请求。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_SRIOV\_VF\_供应商\_设备\_ID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)结构。

<a name="remarks"></a>备注
-------

它会发出此 OID 方法请求之前，必须初始化基础驱动程序[ **NDIS\_SRIOV\_VF\_供应商\_设备\_ID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)结构并且必须设置**VFId** VF 是要读取信息的标识符的成员。

当它处理此 OID 请求时，PF 微型端口驱动程序必须验证指定的 VF 具有先前已分配的资源。 PF 微型端口驱动程序 OID 方法请求的过程将资源分配的 VF [OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。 如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

有关详细信息，请参阅[虚拟函数的查询的 PCI 供应商和设备标识符](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-vendor-and-device-identifiers-for-a-virtual-function)。

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序将返回一个 OID 的 OID 方法请求的以下状态代码\_SRIOV\_VF\_供应商\_设备\_id。

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
<td><p>一个或多个的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)"> <strong>NDIS_SRIOV_VF_VENDOR_DEVICE_ID_INFO</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_VF\_供应商\_设备\_ID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_vendor_device_id_info)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




