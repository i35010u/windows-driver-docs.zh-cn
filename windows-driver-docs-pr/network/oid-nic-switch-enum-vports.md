---
title: OID_NIC_SWITCH_ENUM_VPORTS
description: 过量驱动程序或用户模式应用程序发出对象标识符 (OID) 方法请求 OID_NIC_SWITCH_ENUM_VPORTS 获取数组。
ms.assetid: 4B9587E0-3CA9-46AF-A80E-969E6D563922
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ENUM_VPORTS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f59fe1b8a4db69121b5e295fde3bf9f9c096b074
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213831"
---
# <a name="oid_nic_switch_enum_vports"></a>OID \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS


过量的驱动程序或用户模式应用程序会发出对象标识符 (oid NIC 交换机枚举 VPORTS 的 OID) 方法请求 \_ \_ \_ \_ ，以获取一个数组。 数组中的每个元素指定已在网络适配器的 NIC 交换机上创建 (VPort) 的虚拟端口属性。

成功从此 OID 查询请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   用于定义数组中的元素数的 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ INFO \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array) 结构。

-   [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构的数组。 其中每个结构都包含有关网络适配器的 NIC 交换机上的 VPort 的信息。

    **注意**   如果未在网络适配器上创建 VPorts，则驱动程序会将[**ndis \_ nic \_ 交换机 \_ VPORT \_ INFO \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)结构的**NumElements**成员设置为零，且不会返回[**ndis \_ nic \_ 交换机 \_ VPORT \_ INFO**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构。

     

<a name="remarks"></a>备注
-------

过量驱动程序和用户模式应用程序发出 oid \_ NIC 交换机枚举 VPORTS 的 oid 查询请求 \_ \_ \_ ，以枚举网络适配器的 NIC 交换机上分配的 VPORTS。

在驱动程序或应用程序发出 OID 请求之前，它必须初始化与请求一起传递的 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array) 结构。 当初始化 **NDIS \_ NIC \_ 交换机 \_ VPORT \_ INFO \_ 数组** 结构时，驱动程序或应用程序必须遵循以下准则：

-   如果在 \_ \_ \_ \_ \_ \_ Flags 成员中设置了特定交换机标志上的 NDIS NIC 交换机 VPORT INFO ARRAY ENUM \_ \_ ，则 \_ 会为指定 NIC 交换机上创建的所有 VPorts 返回信息。 **Flags** NIC 交换机由该结构的 **SwitchId** 成员指定。

    **注意**   从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的默认 NIC 交换机。 不管 **flags** 成员中设置了哪些标志，都必须将 **SwitchId** 成员设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

     

-   如果在 \_ \_ \_ \_ \_ Flags 成员中设置了特定函数标志上的 "NDIS NIC 交换机 VPORT 信息数组 \_ 枚举"，则 \_ \_ \_ 会为附加到指定 PCI Express (PCIe) 物理函数 (PF) 或虚拟函数 (网络适配器上的虚拟功能) 虚拟功能的所有 VPorts 返回信息。 **Flags** PF 或 VF 由该结构的 **AttachedFunctionId** 成员指定。

    如果将 **AttachedFunctionId** 成员设置为 NDIS \_ PF \_ 函数 \_ ID，则会为所有 VPorts （包括默认 VPort）返回连接到网络适配器的 PF 的信息。 如果 **AttachedFunctionId** 成员设置为有效的 vf 标识符，则会将所有 VPorts 的信息返回给指定的 vf。

    **注意**   从 Windows Server 2012 开始，只能向 VF 附加一个非默认的 VPort。 但是，多个 VPorts (包括默认 VPort) 可以附加到 PF。

     

-   如果 **Flags** 成员设置为零，则将返回连接到网络适配器上的 PF 或 VF 的所有 VPorts 的信息。 在这种情况下，将忽略 **SwitchId** 和 **AttachedFunctionId** 的值。

有关详细信息，请参阅 [枚举网络适配器上的虚拟端口](./enumerating-virtual-ports-on-a-network-adapter.md)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理对 \_ \_ \_ 微型端口驱动程序的 oid NIC 交换机枚举 \_ VPORTS 请求的 oid 方法请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID \_ NIC \_ 交换机 \_ ENUM \_ VPORTS 请求时，它将返回以下状态代码之一：

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
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)"><strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)

[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 信息 \_ 阵列**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID \_ NIC \_ 交换机 \_ 创建 \_ 开关](oid-nic-switch-create-switch.md)

[OID \_ NIC \_ 交换机 \_ 参数](oid-nic-switch-parameters.md)

 

