---
title: OID_NIC_SWITCH_VPORT_PARAMETERS
description: 过量驱动程序可以获取 NIC 交换机上已在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上创建的虚拟端口（VPort）的参数。
ms.assetid: B22C760E-F2B0-4774-A532-4044C679CD64
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_VPORT_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ab219b5898adbd4b4be3b0f7fd695873897bc7ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844076"
---
# <a name="oid_nic_switch_vport_parameters"></a>OID\_NIC\_SWITCH\_VPORT\_参数


过量驱动程序可以获取 NIC 交换机上已在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上创建的虚拟端口（VPort）的参数。 驱动程序发出 OID\_NIC 的对象标识符（OID）方法请求\_交换机\_VPORT\_参数以获取这些参数。

过量驱动程序发出 oid\_NIC 的 OID 集请求\_交换机\_VPORT\_参数设置附加到网络适配器的 NIC 交换机的指定 VPort 的配置参数。 这些 OID 集请求将颁发给网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。 支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要这些 OID 设置请求。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_SWITCH\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。

过量驱动程序通过将 NDIS\_\_NIC 的**VPortId**成员设置为与 VPort 关联的标识符[ **\_VPort\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构，为 OID 方法或设置请求指定 VPort。 过量驱动程序通过以下方式之一获取 VPort 标识符：

-   通过[oid\_NIC\_开关](oid-nic-switch-create-vport.md)的上一个 oid 方法请求\_CREATE\_VPORT。

-   \_\_NIC 的上一个 OID 方法请求[\_枚举\_VPORTS](oid-nic-switch-enum-vports.md)。

<a name="remarks"></a>备注
-------

OID\_NIC\_交换机\_VPORT\_参数可用于[oid 方法请求](#oid-method-requests)或[oid 设置请求](#oid-set-requests)。

### <a href="" id="oid-method-requests"></a>处理 OID\_NIC 的 OID 方法请求\_SWITCH\_VPORT\_参数

过量驱动程序发出 OID 的 OID 方法请求\_NIC\_SWITCH\_VPORT\_参数以查询附加到网络适配器的 NIC 交换机的 VPort 的当前配置参数。 过量驱动程序通过将 NDIS\_NIC 的**VPortId**成员设置为要查询的 VPort [ **\_\_VPort\_参数结构转换**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)为 VPort 标识符。

NDIS 处理 OID\_NIC 的 OID 方法请求\_交换机\_VPORT\_参数用于微型端口驱动程序。 NDIS 返回[\_nic\_交换机\_创建\_VPORT](oid-nic-switch-create-vport.md)和 oid\_\_\_[枚举\_VPORTS](oid-nic-switch-enum-vports.md)中从 oid 的以前 oid 请求获取的信息。

成功从 OID 方法请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向 NDIS\_\_NIC 的指针，该指针[ **\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。 此结构包含指定开关的配置参数。

有关详细信息，请参阅[查询虚拟端口的参数](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-parameters-of-a-virtual-port)。

### <a href="" id="oid-set-requests"></a>处理 oid\_NIC 的 OID 集请求\_SWITCH\_VPORT\_参数

过量驱动程序发出 oid\_NIC 的 OID 集请求\_交换机\_VPORT\_参数更改附加到网络适配器的 NIC 交换机的 VPort 的当前配置参数。 此 OID 请求可用于更新默认值和非默认 VPorts 的参数。

只能更改 VPort 的配置参数的有限子集。 过量驱动程序通过设置 NDIS\_NIC 的以下成员来指定要更改的参数[ **\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构：

1.  **VPortId**成员设置为将更改其参数的 VPort 的标识符。

2.  相应的 NDIS\_NIC\_交换机\_VPORT\_参数\_*Xxx*\_更改标志在**flags**成员中设置。 仅当在 Ntddndis 中定义了相应的 NDIS\_NIC\_\_\_ *\_个*参数参数时，才可以更改[**NDIS\_nic\_switch\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的成员。

3.  [**NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的相应成员设置为要更改的 VPORT 配置参数。

在 PF 微型端口驱动程序接收 OID\_NIC\_开关\_VPORT\_参数后，该驱动程序将用配置参数配置硬件。 该驱动程序只能更改由 NDIS\_NIC 标识的配置参数，\_交换机\_VPORT\_参数\_*Xxx*\_\_\_\_ [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

有关详细信息，请参阅[设置虚拟端口的参数](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-parameters-of-a-virtual-port)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序返回 OID\_NIC 的以下状态代码\_交换机\_VPORT\_参数。

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
<td><p>PF 微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 或 PF 微型端口驱动程序设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>成员（用于 OID 方法请求）或<strong>数据。SET_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员（用于 OID 设置请求）设置为所需的最小缓冲区大小。</p></td>
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
[**NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_交换机\_枚举\_VPORTS](oid-nic-switch-enum-vports.md)

 

 




