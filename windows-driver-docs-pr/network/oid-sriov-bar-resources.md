---
title: OID_SRIOV_BAR_RESOURCES
description: NDIS 发出 OID_SRIOV_BAR_RESOURCES 的对象标识符（OID）方法请求，以确定分配给 PCIe 虚拟功能（VF）的 PCI Express （PCIe）基址寄存器（BAR）的内存资源。
ms.assetid: CA29591B-EBFB-4B12-A980-F3FAD65207E2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_BAR_RESOURCES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8bfa71685bdb8017777d131ea2ac46656a68674f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843994"
---
# <a name="oid_sriov_bar_resources"></a>OID\_SRIOV\_BAR\_资源


NDIS 发出 OID\_SRIOV\_BAR\_资源的对象标识符（OID）方法请求，以确定分配给 PCIe 虚拟功能（VF）的 PCI Express （PCIe）基址寄存器（BAR）的内存资源。

NDIS 将此 OID 方法请求颁发给网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下结构：

-   [**NDIS\_SRIOV\_BAR\_资源\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构，该结构指定 PF 微型端口驱动程序返回其资源信息的 VF 和条形。

-   [**CM\_部分\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)结构，该结构遵循[**NDIS\_SRIOV\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)\_\_INFO 结构资源。 **CM\_PARTIAL\_资源\_描述符**结构包含有关分配给指定条的内存资源的信息。

<a name="remarks"></a>备注
-------

NDIS 发出 oid\_SRIOV\_BAR\_资源的 OID 方法请求，以获取分配给 VF 栏的内存资源的系统物理地址和长度。 在发出 OID 方法请求之前，NDIS 会按以下方式将[**ndis\_SRIOV\_BAR\_资源\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构设置格式：

-   NDIS 将[**ndis\_SRIOV\_栏\_资源\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构的**VFId**成员设置为与 VF 关联的标识符。

-   NDIS 将[**ndis\_SRIOV\_栏\_资源\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构的**BarIndex**成员设置为指定 VF 的栏索引。 条形索引是 PCI 配置空间中的栏表内寄存器的偏移量。

-   NDIS 将[**ndis\_SRIOV\_栏\_资源\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构的**BarResourcesOffset**成员设置为以字节为单位的偏移量（以字节为单位），从 NDIS\_\_\_\_[ **\_的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)**资源**\_\_

**请注意**  过量驱动程序（如协议或筛选器驱动程序）无法向 PF 小型端口驱动程序\_SRIOV\_BAR\_资源发出 oid 方法请求。

 

当 PF 微型端口驱动程序接收到 OID 方法请求时，驱动程序会通过将[ **\_部分\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)**结构的格式**设置为[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的成员，来返回指定条的资源。 驱动程序将**CM\_部分\_资源\_描述符**结构的格式设置为与指定的 VF 栏关联的系统硬件资源。

**请注意**  驱动程序必须为**CmResourceTypeMemory**的资源类型设置结构格式。

 

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 OID\_SRIOV\_BAR\_资源的方法请求返回以下状态代码之一。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区小于（sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>） + sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor" data-raw-source="[&lt;strong&gt;CM_PARTIAL_RESOURCE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)"><strong>CM_PARTIAL_RESOURCE_DESCRIPTOR</strong></a>）。 PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**CM\_部分\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_BAR\_资源\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)

 

 




