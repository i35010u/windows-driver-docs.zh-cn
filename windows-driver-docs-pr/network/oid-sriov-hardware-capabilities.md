---
title: OID_SRIOV_HARDWARE_CAPABILITIES
description: 过量驱动程序发出 OID_SRIOV_HARDWARE_CAPABILITIES 的对象标识符（OID）查询请求，以获取网络适配器的单个根 i/o 虚拟化（SR-IOV）硬件功能。
ms.assetid: EEF99105-BBDC-4093-8B11-D27F13B1A3D0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_HARDWARE_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 14574a9f973f2e5036f74977e1c87ebcd36c1e3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843990"
---
# <a name="oid_sriov_hardware_capabilities"></a>OID\_SRIOV\_硬件\_功能


过量驱动程序发出 OID\_的对象标识符（OID）查询请求\_硬件\_功能，以获取网络适配器的单个根 i/o 虚拟化（SR-IOV）硬件功能。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构包含有关网络适配器的硬件功能的信息，例如适配器是否支持 sr-iov 以及微型端口驱动程序是否正在管理适配器的 PCI Express （PCIe）物理功能（PF）或虚拟功能（VF）。 这些功能可能包括 INF 文件设置当前禁用的硬件功能，或通过 "**高级**属性" 页当前禁用的硬件功能。

**请注意**  网络适配器的所有 sr-iov 功能\_SRIOV\_硬件\_功能的 oid 查询请求返回，而不考虑是否启用或禁用功能。

 

从 NDIS 6.30 开始，微型端口驱动程序会在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时提供 sr-iov 硬件功能。 驱动程序使用 SR-IOV 硬件功能初始化[**ndis\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构，并设置[**NDIS\_微型端口\_适配器的 HARDWARESRIOVCAPABILITIES 成员\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构指向**NDIS\_SRIOV\_功能**结构的指针。 然后，小型端口驱动程序将调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将*MiniportAttributes*参数设置为指向**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**结构。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_SRIOV 的 OID 查询请求，\_微型端口驱动程序的硬件\_功能请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID\_SRIOV\_硬件\_功能请求时，它将返回以下状态代码之一。

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
<td><p>信息缓冲区太短。 微型端口驱动程序必须设置<strong>数据。QUERY_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[ **\_附加\_参数的 NDIS\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

 

 




