---
title: OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: 过量驱动程序发出 OID 查询请求 OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES，以获取网络适配器的接收筛选硬件功能。
ms.assetid: 2b80944e-5309-4cb0-a69a-331f8fd3f7a4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 596f198e3252a7a365d07a436dabd1cc1ce893c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844008"
---
# <a name="oid_receive_filter_hardware_capabilities"></a>OID\_接收\_筛选器\_硬件\_功能


过量驱动程序发出 oid 查询请求，\_接收\_FILTER\_硬件\_功能，以获取网络适配器的接收筛选硬件功能。

成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)的指针构造.

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[管理包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单个根 I/o 虚拟化（sr-iov）](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置虚拟端口上的接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构包含有关网络适配器的接收筛选硬件功能的信息。 这些功能可能包括 INF 文件设置或**高级**属性页当前禁用的硬件功能。

**请注意**  网络适配器的所有接收筛选硬件功能都是通过 OID 的 oid 查询请求返回的，\_接收\_筛选器\_硬件\_功能，不管功能是否已启用或已禁用。

 

从 NDIS 6.20 开始，微型端口驱动程序会在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时注册网络适配器的当前启用的接收筛选硬件功能。 微型端口驱动程序通过执行以下步骤来注册这些功能：

1.  驱动程序使用接收筛选硬件功能初始化[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

2.  驱动程序初始化[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构，并将**CurrentReceiveFilterCapabilities**成员设置为指向[**NDIS\_接收的指针\_筛选\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

3.  微型端口驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)构造.

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_接收\_筛选器的 OID 查询请求\_微型端口驱动程序的硬件\_功能，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
请求已成功完成。 **InformationBuffer**指向[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效的\_长度  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>不\_支持 NDIS\_状态\_  
网络适配器不支持接收筛选。

<a href="" id="ndis-status-failure"></a>\_故障时的 NDIS\_状态  
由于其他原因，请求失败。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

 

 




