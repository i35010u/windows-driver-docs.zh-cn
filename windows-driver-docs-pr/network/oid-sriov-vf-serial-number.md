---
title: OID_SRIOV_VF_SERIAL_NUMBER
description: 过量驱动程序发出 OID_SRIOV_VF_SERIAL_NUMBER 的对象标识符（OID）查询请求，以确定 PCI Express （PCIe）虚拟功能（VF）网络适配器的序列号。
ms.assetid: C4D04C96-94FA-4E01-839C-A9C5026D7AE5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_SERIAL_NUMBER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 07a6d73766e383b4737ee0de4c6ce2ad3a271fe9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843973"
---
# <a name="oid_sriov_vf_serial_number"></a>OID\_SRIOV\_VF\_序列\_号


过量驱动程序发出 OID 的对象标识符（OID）查询请求\_SRIOV\_VF\_序列\_号，以确定 PCI Express （PCIe）虚函数（VF）网络适配器的序列号。 此虚拟网络适配器显示在 VF 附加到的 Hyper-v 子分区的来宾操作系统中。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SRIOV\_VF\_\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)结构\_的指针的指针。

<a name="remarks"></a>备注
-------

过量驱动程序使用序列号将 VF 网络适配器映射到物理网络适配器上的 VF 的实例。 序列号由虚拟化堆栈生成，然后，在通过 oid 的 oid 集请求（ [\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)来分配 vf 的资源之前，会生成该序列号。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_SRIOV\_VF\_对微型端口驱动程序的串行\_号请求的 OID 查询请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS\_VF\_序列\_号请求处理 OID\_SRIOV 时，它将返回以下状态代码之一。

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
<td><p>微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者未启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
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

[**NDIS\_SRIOV\_VF\_串行\_号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

 

 




