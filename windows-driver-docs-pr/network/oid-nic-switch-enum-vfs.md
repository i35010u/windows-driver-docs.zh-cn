---
title: OID_NIC_SWITCH_ENUM_VFS
description: 过量驱动程序或用户模式应用程序发出对象标识符 (OID) 方法请求 OID_NIC_SWITCH_ENUM_VFS 获取数组。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ENUM_VFS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c58533c8a5cd4a0c787cd37c39f6dcab382820e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795925"
---
# <a name="oid_nic_switch_enum_vfs"></a>OID \_ NIC \_ 交换机 \_ 枚举 \_ VFS


过量驱动程序或用户模式应用程序会发出对象标识符 (OID) 方法请求 OID \_ NIC \_ 交换机 \_ 枚举 \_ VFS 获取一个数组。 数组中的每个元素都指定 PCI Express (PCIe) 虚函数的属性， (VF) 连接到网络适配器的 NIC 交换机上的 NIC 交换机。

成功从此 OID 查询请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   用于定义数组中的元素数的 [**NDIS \_ NIC \_ 开关 \_ VF \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array) 结构。

-   [**NDIS \_ NIC \_ 交换机 \_ VF \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构的数组。 其中每个结构都包含有关网络适配器的 NIC 交换机上单个 VF 的信息。 通过 oid [ \_ nic \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)的 oid 方法请求，将 VF 附加到 NIC 开关。

    **注意** 如果网络适配器上没有连接到任何一个 NIC 交换机的 VFs， [**ndis \_ nic \_ 交换机 \_ vf \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)结构的 **NumElements** 成员将设置为零，且不会返回任何 [**NDIS \_ nic \_ 交换机 \_ vf \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构。

     

<a name="remarks"></a>备注
-------

过量驱动程序和用户模式应用程序发出 oid \_ NIC 交换机枚举 vfs 的 oid 方法请求 \_ \_ \_ ，以枚举附加到网络适配器的 NIC 交换机的 VFS。

在驱动程序或应用程序发出 OID 请求之前，它必须初始化与请求一起传递的 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array) 结构。 初始化 **NDIS \_ NIC \_ 交换机 \_ VF \_ 信息 \_ 阵列** 结构时，驱动程序或应用程序必须遵循以下准则：

-   如果在 \_ \_ \_ \_ \_ \_ Flags 成员中设置了特定交换机标志上的 NDIS NIC 交换机 VF 信息阵列枚举 \_ \_ \_ ，则驱动程序或应用程序必须将 **SwitchId** 成员设置为 sr-iov 网络适配器上的 NIC 交换机标识符。 **Flags** 通过以这种方式设置这些成员，只会为 SR-IOV 网络适配器上指定的 NIC 交换机返回 VF 信息。

    **注意**  过量驱动程序和用户模式应用程序可以通过发出 oid [ \_ nic \_ 交换机 \_ 枚举 \_ 开关](oid-nic-switch-enum-switches.md)的 oid 查询请求来获取 NIC 交换机标识符。

     

-   如果 **Flags** 成员设置为零，则驱动程序或应用程序必须将 **SwitchId** 成员设置为零。 通过以这种方式设置这些成员，将为 SR-IOV 网络适配器上的所有 NIC 交换机返回 VF 信息。

**注意**  从 Windows Server 2012 开始，Windows 只支持网络适配器上的默认 NIC 交换机。 不管 **flags** 成员中的标志集如何，都必须将 **SwitchId** 成员设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

 

有关 NIC 交换机的详细信息，请参阅 [Nic 交换机](./nic-switches.md)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理对 \_ \_ \_ 微型端口驱动程序的 oid NIC 交换机枚举 \_ VFS 请求的 oid 方法请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID \_ NIC \_ 交换机 \_ 枚举 \_ VFS 请求时，它将返回以下状态代码之一。

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
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)"><strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

## <a name="see-also"></a>请参阅


****
[**NDIS \_ NIC \_ 交换机 \_ VF \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)

[**NDIS \_ NIC \_ 交换机 \_ VF \_ 信息 \_ 阵列**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[OID \_ NIC \_ 交换机 \_ 创建 \_ 开关](oid-nic-switch-create-switch.md)

[OID \_ NIC \_ 开关 \_ VF \_ 参数](oid-nic-switch-vf-parameters.md)

