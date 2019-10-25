---
title: OID_SRIOV_CURRENT_CAPABILITIES
description: 过量驱动程序发出 OID_SRIOV_CURRENT_CAPABILITIES 的对象标识符（OID）查询请求，以获取网络适配器的当前单一根 i/o 虚拟化（SR-IOV）功能。
ms.assetid: EE76B3F8-2883-484A-B2EE-6F7D4738934E
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_CURRENT_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3462bf4802036fe60c78cee5ad4aceb6b73dad6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843991"
---
# <a name="oid_sriov_current_capabilities"></a>\_当前\_功能的 OID\_SRIOV


过量驱动程序发出 OID\_SRIOV\_当前\_功能的对象标识符（OID）查询请求，以获取网络适配器的当前单一根 i/o 虚拟化（SR-IOV）功能。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

从 NDIS 6.30 开始，微型端口驱动程序在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，将在网络适配器上提供已启用的 sr-iov 硬件功能。 驱动程序使用当前启用的 SR-IOV 硬件功能初始化[**ndis\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构，并设置 [**NDIS\_微型端口\_适配器的 CurrentSriovCapabilities 成员\_硬件\_帮助\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构指向**NDIS\_SRIOV\_功能**结构的指针。 然后，微型端口驱动程序将调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将*MiniportAttributes*参数设置为指向**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**结构。

过量协议和筛选器驱动程序不必\_当前\_功能发出 oid\_SRIOV 的 OID 查询请求。 NDIS 按以下方式向这些驱动程序提供当前启用的网络适配器 SR-IOV 功能：

-   NDIS 将基础网络适配器的当前启用的 SR-IOV 功能报告到 NDIS\_在绑定操作过程中[**绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)**结构的内部**协议驱动程序。

-   NDIS 报告基础网络适配器当前启用的 SR-IOV 功能，以覆盖[**NDIS\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)的**SriovCapabilities**成员中的筛选器驱动程序，\_\_在附加操作。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_SRIOV\_当前\_微型端口驱动程序的功能请求的 oid 查询请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID\_SRIOV\_当前\_功能请求时，它将返回以下状态代码之一：

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
<td><p>信息缓冲区太短。 微型端口驱动程序必须设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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

 

 




