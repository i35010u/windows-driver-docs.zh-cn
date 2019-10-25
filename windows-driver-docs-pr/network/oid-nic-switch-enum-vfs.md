---
title: OID_NIC_SWITCH_ENUM_VFS
description: 过量驱动程序或用户模式应用程序发出 OID_NIC_SWITCH_ENUM_VFS 的对象标识符（OID）方法请求，以获取一个数组。
ms.assetid: ABACB70C-9307-4560-93DD-0475AD1FFF10
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ENUM_VFS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7e9acf7303d8f3f5af0d6ca11ce589116ac6f8be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844088"
---
# <a name="oid_nic_switch_enum_vfs"></a>OID\_NIC\_交换机\_枚举\_VFS


过量驱动程序或用户模式应用程序发出 OID\_NIC 的对象标识符（OID）方法请求\_交换机\_枚举\_VFS 以获取一个数组。 数组中的每个元素都指定了附加到网络适配器的 NIC 交换机上的 NIC 交换机的 PCI Express （PCIe）虚拟功能（VF）的特性。

成功从此 OID 查询请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   [**NDIS\_NIC\_交换机\_VF\_信息\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)定义数组中元素数目的数组结构。

-   [**NDIS\_NIC 的数组\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构。 其中每个结构都包含有关网络适配器的 NIC 交换机上单个 VF 的信息。 VF 通过 oid\_NIC 的 OID 方法请求（ [\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)）附加到 nic 开关。

    **注意**  如果没有连接到网络适配器上的 NIC 交换机的 VFs，NDIS\_NIC 的**NUMELEMENTS**成员[ **\_交换机\_VF\_\_ARRAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array) [**structure @no__t_返回 12_ NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构。

     

<a name="remarks"></a>备注
-------

过量驱动程序和用户模式应用程序向 OID\_NIC\_交换机\_枚举\_VFS 的 OID 方法请求，以枚举附加到网络适配器的 NIC 交换机的 VFs。

在驱动程序或应用程序发出 OID 请求之前，它必须将[**NDIS\_NIC\_交换机\_\_VF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)与请求一起传递\_数组结构。 在初始化 NDIS\_NIC 时，驱动程序或应用程序必须遵循以下准则 **\_交换机\_VF\_信息\_数组**结构：

-   如果 NDIS\_NIC\_交换机\_VF\_信息\_数组\_在**Flags**成员中设置\_特定\_交换机标志，驱动程序或应用程序必须将**SwitchId**成员设置为 sr-iov 网络适配器上的 NIC 交换机标识符。 通过以这种方式设置这些成员，只会为 SR-IOV 网络适配器上指定的 NIC 交换机返回 VF 信息。

    **请注意**  过量驱动程序和用户模式应用程序可以通过\_nic 发出 oid 查询请求来获取 nic 交换机标识符， [\_开关\_枚举\_开关](oid-nic-switch-enum-switches.md)。

     

-   如果**Flags**成员设置为零，则驱动程序或应用程序必须将**SwitchId**成员设置为零。 通过以这种方式设置这些成员，将为 SR-IOV 网络适配器上的所有 NIC 交换机返回 VF 信息。

**注意**  从 windows Server 2012 开始，windows 只支持网络适配器上的默认 NIC 交换机。 不管**flags**成员中的标志集如何，都必须将**SwitchId**成员设置为 NDIS\_默认\_交换机\_ID。

 

有关 NIC 交换机的详细信息，请参阅[Nic 交换机](https://docs.microsoft.com/windows-hardware/drivers/network/nic-switches)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_NIC 的 OID 方法请求\_交换机\_枚举\_用于微型端口驱动程序的 VFS 请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID\_NIC\_交换机\_枚举\_VFS 请求时，它将返回以下状态代码之一。

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
[**NDIS\_NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)

[**NDIS\_NIC\_交换机\_VF\_信息\_阵列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_交换机\_创建\_交换机](oid-nic-switch-create-switch.md)

[OID\_NIC\_交换机\_VF\_参数](oid-nic-switch-vf-parameters.md)

 

 




