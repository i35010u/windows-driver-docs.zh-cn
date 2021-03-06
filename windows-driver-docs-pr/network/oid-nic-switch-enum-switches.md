---
title: OID_NIC_SWITCH_ENUM_SWITCHES
description: 过量的驱动程序或用户模式应用程序发出对象标识符 (OID) 查询请求 OID_NIC_SWITCH_ENUM_SWITCHES 获取数组。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ENUM_SWITCHES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b6ca6c55aa506f2f41eeaadd99482d370a04072d
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248551"
---
# <a name="oid_nic_switch_enum_switches"></a>OID \_ NIC \_ 交换机 \_ 枚举 \_ 开关


过量驱动程序或用户模式应用程序会发出对象标识符 (OID，) OID \_ NIC \_ 交换机枚举参数的查询请求 \_ \_ ，以获取一个数组。 数组中的每个元素指定已在网络适配器上创建的 NIC 交换机的属性。

成功从此 OID 查询请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   用于定义数组中的元素数的 [**NDIS \_ NIC \_ 交换机 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array) 结构。

-   [**NDIS \_ NIC \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构的数组。 其中每个结构都包含有关在网络适配器上创建的单个 NIC 交换机的信息。

    **注意** 如果网络适配器没有 NIC 交换机，则驱动程序将 [**ndis \_ nic \_ 交换机 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)结构的 **NumElements** 成员设置为零，且不会返回任何 [**NDIS \_ nic \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。

     

<a name="remarks"></a>备注
-------

过量驱动程序和用户模式应用程序发出 oid \_ NIC 交换机枚举开关的 oid 查询请求 \_ \_ \_ ，以枚举网络适配器上创建的 NIC 交换机。

**注意**  从 Windows Server 2012 开始，单个根 i/o 虚拟化 (SR-IOV) 接口仅支持网络适配器上的默认 NIC 交换机。 因此，返回的 [**ndis \_ nic \_ 交换机 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array) 结构必须为默认 NIC 交换机指定一个 [**ndis \_ NIC \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info) 元素，该元素由 NDIS \_ 默认 \_ 交换机 ID 的标识符引用 \_ 。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理对 \_ \_ \_ 微型端口驱动程序的 oid NIC 交换机枚举 \_ 开关请求的 oid 查询请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID \_ NIC \_ 交换机 \_ 枚举请求时 \_ ，它将返回以下状态代码之一。

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
<td><p>微型端口驱动程序不支持 SR-IOV 接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_INFO_ARRAY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_INFO_ARRAY</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NDIS \_ NIC \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)

[**NDIS \_ NIC \_ 交换机 \_ 信息 \_ 阵列**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info_array)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[OID \_ NIC \_ 交换机 \_ 创建 \_ 开关](oid-nic-switch-create-switch.md)

[OID \_ NIC \_ 交换机 \_ 参数](oid-nic-switch-parameters.md)

