---
title: OID_SRIOV_BAR_RESOURCES
description: NDIS 发出一个对象标识符 (OID) 方法请求的 OID_SRIOV_BAR_RESOURCES 来确定分配到 PCI Express (PCIe) 基本地址注册 （栏） 的 PCIe 虚拟函数 (VF) 的内存资源。
ms.assetid: CA29591B-EBFB-4B12-A980-F3FAD65207E2
ms.date: 08/08/2017
keywords: -OID_SRIOV_BAR_RESOURCES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c00487b842b64e49307e3a05a18a24e2fde978ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521751"
---
# <a name="oidsriovbarresources"></a>OID\_SRIOV\_栏\_资源


NDIS 发出对象标识符 (OID) 方法请求的 OID\_SRIOV\_栏\_资源，以确定所分配到 PCI Express (PCIe) 基本地址注册 （栏） 的 PCIe 虚拟函数 (VF) 的内存资源.

NDIS 此 OID 方法向发出请求的微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF)。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区包含以下结构：

-   [ **NDIS\_SRIOV\_栏\_资源\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451675)结构，它指定 VF 和栏的 PF 微型端口驱动程序返回的资源信息。

-   一个[ **CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构，它遵循[ **NDIS\_SRIOV\_栏\_资源\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451675)结构。 **CM\_分部\_资源\_描述符**结构包含有关已分配的内存资源的信息与指定栏。

<a name="remarks"></a>备注
-------

NDIS 发出 OID 方法请求的 OID\_SRIOV\_栏\_资源，以获取系统的物理地址和长度分配给取景器栏的内存资源。 它会发出 OID 方法请求之前，设置格式 NDIS [ **NDIS\_SRIOV\_栏\_资源\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451675)结构如下所示：

-   NDIS 集**VFId**的成员[ **NDIS\_SRIOV\_栏\_资源\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451675)结构与 VF 相关联的标识符。

-   NDIS 集**BarIndex**的成员[ **NDIS\_SRIOV\_栏\_资源\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451675)结构索引指定 VF 栏。 栏索引是寄存器的 PCI 配置空间中的条在表中的偏移量。

-   NDIS 集**BarResourcesOffset**的成员[ **NDIS\_SRIOV\_栏\_资源\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451675)从开始处的偏移量，单位为字节，结构**NDIS\_SRIOV\_栏\_资源\_信息**结构[ **CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构。

**请注意**  过量驱动程序，例如协议或筛选器驱动程序不能发出 OID 方法请求的 OID\_SRIOV\_栏\_PF 微型端口驱动程序的资源。

 

当 PF 微型端口驱动程序收到 OID 方法请求时，驱动程序将返回为指定的资源的格式设置栏[ **CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构内**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 驱动程序格式**CM\_分部\_资源\_描述符**结构的指定 VF 栏与关联的系统硬件资源。

**请注意**  驱动程序必须格式化为资源类型的结构**CmResourceTypeMemory**。

 

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序将返回一个 OID 的方法请求的以下状态代码\_SRIOV\_栏\_资源。

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
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451675" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451675)"> <strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区小于 (sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451675" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451675)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>) + sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/ff541977" data-raw-source="[&lt;strong&gt;CM_PARTIAL_RESOURCE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541977)"><strong>CM_PARTIAL_RESOURCE_DESCRIPTOR</strong> </a>). PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
<td><p>版本</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_栏\_资源\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451675)

 

 




