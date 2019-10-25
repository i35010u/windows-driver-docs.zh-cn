---
title: OID_NIC_SWITCH_ENUM_VPORTS
description: 过量驱动程序或用户模式应用程序发出 OID_NIC_SWITCH_ENUM_VPORTS 的对象标识符（OID）方法请求，以获取一个数组。
ms.assetid: 4B9587E0-3CA9-46AF-A80E-969E6D563922
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ENUM_VPORTS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 612f5be262fbd7960ec2da9cd43970d7843b48fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844086"
---
# <a name="oid_nic_switch_enum_vports"></a>OID\_NIC\_交换机\_枚举\_VPORTS


过量驱动程序或用户模式应用程序发出 OID\_NIC 的对象标识符（OID）方法请求\_交换机\_枚举\_VPORTS 以获取一个数组。 数组中的每个元素指定已在网络适配器的 NIC 交换机上创建的虚拟端口（VPort）的属性。

成功从此 OID 查询请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   [**NDIS\_NIC\_交换机\_VPORT\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)结构，该结构定义数组中的元素数目。

-   [**NDIS\_NIC 的数组\_交换机\_VPORT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构。 其中每个结构都包含有关网络适配器的 NIC 交换机上的 VPort 的信息。

    **注意**  如果未在网络适配器上创建 VPorts，则驱动程序会将[**NDIS\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)的**NumElements**成员设置\_VPORT\_[**返回\_NIC\_交换机\_VPORT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构。

     

<a name="remarks"></a>备注
-------

过量驱动程序和用户模式应用程序发出 oid\_NIC 的 oid 查询请求\_交换机\_枚举\_VPORTS 枚举在网络适配器的 NIC 交换机上分配的 VPorts。

在驱动程序或应用程序发出 OID 请求之前，它必须将[**NDIS\_NIC\_交换机\_VPORT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)与请求一起传递\_数组结构。 在初始化 NDIS\_NIC 时，驱动程序或应用程序必须遵循以下准则 **\_交换机\_VPORT\_信息\_数组**结构：

-   如果 NDIS\_NIC\_交换机\_VPORT\_信息\_数组\_在**Flags**成员中设置\_特定\_交换机标志，将返回在指定 NIC 交换机上创建的所有 VPorts 的信息。 NIC 交换机由该结构的**SwitchId**成员指定。

    **注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的默认 NIC 交换机。 不管**flags**成员中设置了哪些标志，都必须将**SwitchId**成员设置为 NDIS\_默认\_交换机\_ID。

     

-   如果 NDIS\_NIC\_交换机\_VPORT\_信息\_数组\_在**Flags**成员中设置\_特定\_函数标志，将返回连接到网络适配器上指定 PCI Express （PCIe）物理功能（PF）或虚拟功能（VF）的所有 VPorts 的信息。 PF 或 VF 由该结构的**AttachedFunctionId**成员指定。

    如果**AttachedFunctionId**成员设置为 NDIS\_PF\_函数\_ID，则会为所有 VPorts （包括默认 VPort）返回与网络适配器的 PF 关联的信息。 如果**AttachedFunctionId**成员设置为有效的 vf 标识符，则会将所有 VPorts 的信息返回给指定的 vf。

    **注意**  从 Windows Server 2012 开始，只能将一个非默认的 VPort 附加到 VF。 但是，可以将多个 VPorts （包括默认的 VPort）附加到 PF。

     

-   如果**Flags**成员设置为零，则将返回连接到网络适配器上的 PF 或 VF 的所有 VPorts 的信息。 在这种情况下，将忽略**SwitchId**和**AttachedFunctionId**的值。

有关详细信息，请参阅[枚举网络适配器上的虚拟端口](https://docs.microsoft.com/windows-hardware/drivers/network/enumerating-virtual-ports-on-a-network-adapter)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_NIC 的 OID 方法请求\_交换机\_枚举\_小型端口驱动程序的 VPORTS 请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS\_交换机\_枚举\_VPORTS 请求处理 OID\_NIC 时，它将返回以下状态代码之一：

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
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)"><strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[**NDIS\_NIC\_交换机\_VPORT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)

[**NDIS\_NIC\_交换机\_VPORT\_信息\_阵列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_交换机\_创建\_交换机](oid-nic-switch-create-switch.md)

[OID\_NIC\_交换机\_参数](oid-nic-switch-parameters.md)

 

 




