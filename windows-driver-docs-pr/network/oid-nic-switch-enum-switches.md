---
title: OID_NIC_SWITCH_ENUM_SWITCHES
description: 过量驱动程序或用户模式应用程序发出 OID_NIC_SWITCH_ENUM_SWITCHES 的对象标识符（OID）查询请求，以获取一个数组。
ms.assetid: 706C3F1C-239F-4731-A38E-E150D26C79A5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ENUM_SWITCHES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ffa90622d033e4b862fbabe43236536cc8698878
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844089"
---
# <a name="oid_nic_switch_enum_switches"></a>OID\_NIC\_交换机\_枚举\_开关


过量驱动程序或用户模式应用程序发出 OID 的对象标识符（OID）查询请求\_NIC\_SWITCH\_ENUM\_开关来获取数组。 数组中的每个元素指定已在网络适配器上创建的 NIC 交换机的属性。

成功从此 OID 查询请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   [**NDIS\_NIC\_交换机\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)结构，该结构定义数组中的元素数目。

-   [**NDIS\_NIC 的数组\_交换机\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。 其中每个结构都包含有关在网络适配器上创建的单个 NIC 交换机的信息。

    **请注意**  如果网络适配器没有 nic 交换机，则驱动程序将 NDIS\_\_NIC 的**NumElements**成员设置为[ **\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)结构设置为零，而不将[**ndis\_NIC\_返回\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构的开关。

     

<a name="remarks"></a>备注
-------

过量驱动程序和用户模式应用程序发出 oid\_NIC 的 oid 查询请求\_交换机\_枚举\_开关来枚举网络适配器上创建的 NIC 交换机。

**注意**  从 Windows Server 2012 开始，单个根 i/o 虚拟化（sr-iov）接口仅支持网络适配器上的默认 NIC 交换机。 因此，返回的[**ndis\_nic\_交换机\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)结构必须为默认 nic 交换机指定单个[**NDIS\_nic\_交换机\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)元素，这由NDIS\_默认\_交换机\_ID 的标识符。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_NIC 的 OID 查询请求\_交换机\_\_枚举为微型端口驱动程序请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID\_NIC\_交换机\_枚举\_SWITCH 请求时，它将返回以下状态代码之一。

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
<td><p>微型端口驱动程序不支持 SR-IOV 接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_INFO_ARRAY</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[**NDIS\_NIC\_交换机\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)

[**NDIS\_NIC\_交换机\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_交换机\_创建\_交换机](oid-nic-switch-create-switch.md)

[OID\_NIC\_交换机\_参数](oid-nic-switch-parameters.md)

 

 




