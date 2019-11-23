---
title: OID_NIC_SWITCH_PARAMETERS
description: 过量驱动程序发出 OID_NIC_SWITCH_PARAMETERS 的对象标识符（OID）方法请求，以获取网络适配器上指定 NIC 交换机的当前配置参数。
ms.assetid: 3F2FF2C0-8710-4243-8583-CD80F244FCFB
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c6f0b640dae8975c188fd0a0b6dd82076dbb7b58
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844080"
---
# <a name="oid_nic_switch_parameters"></a>OID\_NIC\_交换机\_参数


过量驱动程序发出 OID\_NIC 的对象标识符（OID）方法请求\_交换机\_参数，以获取网络适配器上指定 NIC 交换机的当前配置参数。 NDIS 处理微型端口驱动程序的这些 OID 方法请求。

过量驱动程序发出 oid\_NIC 的 OID 集请求\_交换机\_参数，以设置网络适配器上指定 NIC 交换机的配置参数。 这些 OID 集请求将颁发给网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。 支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要这些 OID 设置请求。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_SWITCH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。

过量驱动程序通过将 NDIS\_NIC 的**SwitchId**成员设置为 switch 标识符，为 OID 方法或设置请求指定 nic 交换机[ **\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 过量驱动程序通过以下方式之一获取交换机标识符：

-   通过 Oid\_的上一个 OID 方法请求[\_交换机\_枚举\_开关](oid-nic-switch-enum-switches.md)。

-   从 NDIS 的**NicSwitchArray**成员[ **\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构。 NDIS 在[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数的*BindParameters*参数中传递指向此结构的指针。

-   从[**NDIS\_筛选器的 NicSwitchArray 成员\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 NDIS 在[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数的*AttachParameters*参数中传递指向此结构的指针。

**注意**  从 windows Server 2012 开始，windows 只支持网络适配器上的默认 NIC 交换机。 [ **\_交换机\_参数结构的 ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)的**SwitchId**成员必须设置为 NDIS\_默认\_交换机\_ID。

 

<a name="remarks"></a>备注
-------

过量驱动程序会按照以下方式发出 OID\_NIC\_交换机\_参数请求：

-   过量驱动程序发出 oid\_NIC 的 OID 方法请求\_交换机\_参数获取指定 NIC 交换机的当前参数。 有关详细信息，请参阅[查询 NIC 交换机的参数](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-parameters-of-a-nic-switch)。

    **请注意**  NDIS 处理 OID 的 oid 方法请求\_NIC\_开关 "PF" 微型端口驱动程序\_参数。

     

-   过量驱动程序发出 oid\_NIC 的 OID 集请求\_交换机\_参数，以更改指定 NIC 交换机的当前参数。 有关详细信息，请参阅[设置 NIC 交换机的参数](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-parameters-of-a-nic-switch)。

    **请注意**  PF 微型端口驱动程序处理 OID 的 oid 设置请求\_NIC\_开关\_参数。

     

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序返回 OID\_NIC 的以下状态代码\_交换机\_参数。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 或 PF 微型端口驱动程序设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>成员（用于 OID 方法请求）或<strong>数据。SET_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员（用于 OID 设置请求）设置为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_REINIT_REQUIRED</p></td>
<td><p>PF 微型端口驱动程序需要重新初始化网络适配器，才能将更改应用于 NIC 交换机。</p></td>
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
[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[ **\_附加\_参数的 NDIS\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[ **\_交换机\_参数的 NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_交换机\_创建\_交换机](oid-nic-switch-create-switch.md)

[OID\_NIC\_交换机\_枚举\_开关](oid-nic-switch-enum-switches.md)

[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

 

 




