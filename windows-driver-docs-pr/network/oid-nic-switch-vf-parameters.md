---
title: OID_NIC_SWITCH_VF_PARAMETERS
description: 过量驱动程序或用户模式应用程序发出 OID_NIC_SWITCH_VF_PARAMETERS 的对象标识符（OID）方法请求，以获取网络适配器上 PCI Express （PCIe）虚拟功能（VF）的当前配置参数。
ms.assetid: DF08B0BA-6D86-4C4F-AC38-8A401F097925
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_VF_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7b837949593853fd8f7b7c7107387da1a7c96dad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844078"
---
# <a name="oid_nic_switch_vf_parameters"></a>OID\_NIC\_交换机\_VF\_参数


过量驱动程序或用户模式应用程序发出 OID\_\_的对象标识符（OID）方法请求，\_VF\_参数，以获取网络适配器上 PCI Express （PCIe）虚拟功能（VF）的当前配置参数。 只有通过 OID 方法（oid）的 oid 方法请求（ [\_nic\_交换机\_分配\_vf](oid-nic-switch-allocate-vf.md) ）才能通过 oid 的 oid 方法请求分配 VF\_VF\_参数。\_\_

NDIS 处理 OID\_NIC 的 OID 方法请求\_交换机\_微端口驱动程序的参数\_参数。

进行 OID 方法请求时， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)的指针，\_VF\_参数结构。

<a name="remarks"></a>备注
-------

过量驱动程序或用户模式应用程序通过将 NDIS\_NIC 的**VFId**成员设置为要查询的 VF [ **\_交换机\_vf\_参数结构转换**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)为 vf 的标识符。 过量驱动程序或应用程序通过以下方式之一获取 VF 标识符：

-   通过\_\_NIC 发出 oid 方法请求， [\_枚举\_VFS](oid-nic-switch-enum-vfs.md)。

    如果此 OID 请求成功完成，则过量驱动程序或用户模式应用程序将收到网络适配器上分配的所有 VFs 的列表。 列表中的每个元素都是一个[**NDIS\_NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构，以及由**VFId**成员指定的 vf 标识符。

-   通过向[\_分配\_VF\_\_NIC](oid-nic-switch-allocate-vf.md)发出 OID 的 oid 方法请求。

    如果此 OID 请求成功完成，则过量驱动程序会在返回的 NDIS\_NIC 的**VFId**成员中接收新创建的 VF 的标识符[ **\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

    **请注意**  只有过量驱动程序才能以这种方式获取 VF 标识符。

     

成功从 OID 方法请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_\_NIC 的指针，\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 此结构包含指定的 VF 的配置参数。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_NIC 的 OID 方法请求\_交换机\_用于微型端口驱动程序的 VF\_参数，并为 OID 的 OID 方法请求返回以下状态代码\_\_VF\_参数。\_

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>成员指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者未启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>）。 NDIS 设置<strong>数据。METHOD_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据。METHOD_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_交换机\_枚举\_VFS](oid-nic-switch-enum-vfs.md)

[**NDIS\_NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)

[OID\_NIC\_交换机\_VF\_参数](oid-nic-switch-vf-parameters.md)

 

 




