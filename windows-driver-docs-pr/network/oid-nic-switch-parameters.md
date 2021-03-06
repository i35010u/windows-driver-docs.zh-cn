---
title: OID_NIC_SWITCH_PARAMETERS
description: 过量驱动程序发出对象标识符 (OID) 方法请求 OID_NIC_SWITCH_PARAMETERS 获取网络适配器上指定 NIC 交换机的当前配置参数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 080b84266567e3f11fee7bda6f99a52b376ec1e1
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249059"
---
# <a name="oid_nic_switch_parameters"></a>OID \_ NIC \_ 交换机 \_ 参数


过量驱动程序) OID NIC 交换机参数 (OID 中发出对象标识符 \_ \_ \_ ，以获取网络适配器上指定 NIC 交换机的当前配置参数。 NDIS 处理微型端口驱动程序的这些 OID 方法请求。

过量驱动程序发出 oid NIC 交换机参数的 OID 集请求 \_ \_ \_ ，以设置网络适配器上指定 NIC 交换机的配置参数。 这些 OID 集请求将颁发给网络适配器 PCI Express (PCIe) 物理功能 (PF) 的微型端口驱动程序。 对于支持 (SR-IOV) 接口的单个根 i/o 虚拟化的 PF 微型端口驱动程序，这些 OID 设置请求是必需的。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的指针。

过量驱动程序通过将 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的 **SwitchId** 成员设置为 switch 标识符，来指定 OID 方法或 set 请求的 NIC 开关。 过量驱动程序通过以下方式之一获取交换机标识符：

-   从 [oid \_ NIC \_ 交换机 \_ 枚举 \_ 参数](oid-nic-switch-enum-switches.md)的上一个 oid 方法请求开始。

-   从 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **NicSwitchArray** 成员。 NDIS 在 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数的 *BindParameters* 参数中传递指向此结构的指针。

-   从 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构的 **NicSwitchArray** 成员。 NDIS 在 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数的 *AttachParameters* 参数中传递指向此结构的指针。

**注意**  从 Windows Server 2012 开始，Windows 只支持网络适配器上的默认 NIC 交换机。 必须将 [**ndis \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的 **SwitchId** 成员设置为 ndis \_ 默认 \_ 交换机 \_ ID。

 

<a name="remarks"></a>备注
-------

过量驱动程序 \_ \_ 按以下方式发出 OID NIC 交换机 \_ 参数请求：

-   过量驱动程序发出 OID \_ nic 交换机参数的 oid 方法 \_ 请求 \_ ，以获取指定 NIC 交换机的当前参数。 有关详细信息，请参阅 [查询 NIC 交换机的参数](./querying-the-parameters-of-a-nic-switch.md)。

    **注意**  NDIS 处理 PF NIC 交换机参数的 OID 方法请求， \_ \_ \_ 用于 PF 的微型端口驱动程序。

     

-   过量驱动程序发出 oid \_ nic 交换机参数的 oid 集 \_ 请求 \_ ，以更改指定 NIC 交换机的当前参数。 有关详细信息，请参阅 [设置 NIC 交换机的参数](./setting-the-parameters-of-a-nic-switch.md)。

    **注意**  PF 微型端口驱动程序处理 OID \_ NIC 交换机参数的 oid 设置请求 \_ \_ 。

     

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序为 OID \_ NIC 交换机参数的设置或方法 oid 请求返回以下状态代码 \_ \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF 微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 或 PF 微型端口驱动程序设置 <strong>数据。METHOD_INFORMATION。</strong> (OID 方法请求) 或数据的 BytesNeeded 成员 <strong>。SET_INFORMATION。BytesNeeded</strong> 成员 () 在 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中，将其设置为所需的最小缓冲区大小。</p></td>
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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[OID \_ NIC \_ 交换机 \_ 创建 \_ 开关](oid-nic-switch-create-switch.md)

[OID \_ NIC \_ 交换机 \_ 枚举 \_ 开关](oid-nic-switch-enum-switches.md)

[*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

