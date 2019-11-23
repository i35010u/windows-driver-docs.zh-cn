---
title: OID_NIC_SWITCH_CURRENT_CAPABILITIES
description: 过量驱动程序发出 OID_NIC_SWITCH_CURRENT_CAPABILITIES 的对象标识符（OID）查询请求，以获取网络适配器中 NIC 交换机当前启用的硬件功能。
ms.assetid: 529dc5d5-9b84-4891-9e7a-1f9f7850c6d7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CURRENT_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f1bf011e3ec836f322bea55a6567f006a743859b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844096"
---
# <a name="oid_nic_switch_current_capabilities"></a>OID\_NIC\_交换机\_当前\_功能


过量驱动程序发出 OID\_NIC 的对象标识符（OID）查询请求\_交换机\_当前\_功能，以获取网络适配器中 NIC 交换机当前启用的硬件功能。

成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。

<a name="remarks"></a>备注
-------

从 NDIS 6.20 开始，微型端口驱动程序会在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，为网络适配器提供当前启用的 NIC 交换机硬件功能。 驱动程序使用 NIC 交换机硬件功能初始化[**ndis\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构，并将 NDIS\_微型端口\_适配器的**CurrentNicSwitchCapabilities**成员设置\_[**硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构转换为指向**NDIS\_NIC\_交换机\_功能**结构的指针。 然后，小型端口驱动程序将调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将*MiniportAttributes*参数设置为指向**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**结构。

**请注意**  从 NDIS 6.30 开始，支持单个根 i/o 虚拟化（sr-iov）接口的微型端口驱动程序必须注册 NIC 交换机的已启用硬件功能。 驱动程序通过调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)注册这些功能。

 

过量协议和筛选器驱动程序不必发出 oid\_NIC\_SWITCH\_当前\_功能的 OID 查询请求。 NDIS 按以下方式将网络适配器的当前启用的 NIC 交换机硬件功能提供给这些驱动程序：

-   NDIS 将基础网络适配器的当前启用的 NIC 交换机硬件功能报告到 NDIS\_在绑定操作过程中[**绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)**结构的内部**协议驱动程序。

-   NDIS 报告基础网络适配器的当前启用的 NIC 交换机硬件功能，以便在附加操作期间[ **\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构，从而在 NDIS\_筛选器的**NicSwitchCapabilities**成员中对驱动程序进行筛选。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_\_NIC 的 OID 查询请求\_最新的针对微型端口驱动程序的\_功能请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理\_NIC\_SWITCH\_当前\_功能请求时的 OID 时，它将返回以下状态代码之一：

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者未启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>）。 微型端口驱动程序必须设置<strong>数据。QUERY_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

[ **\_附加\_参数的 NDIS\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




