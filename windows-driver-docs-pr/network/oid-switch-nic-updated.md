---
title: OID_SWITCH_NIC_UPDATED
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 将 OID_SWITCH_NIC_UPDATED 的请求设置为可扩展交换机驱动程序堆栈。
ms.assetid: C1B446A3-861F-41B4-99EF-C7CB45F86F39
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_UPDATED 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9d55f82dac9eac83642beb6177887e5b93302d73
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210119"
---
# <a name="oid_switch_nic_updated"></a>\_ \_ 已更新 OID 交换机 NIC \_


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 将 OID \_ 交换机 NIC 的请求 \_ \_ 更新为可扩展交换机驱动程序堆栈。 此 OID 请求通知底层的可扩展交换机扩展关于网络适配器的参数更新。 仅为已连接并且尚未开始断开连接过程的 Nic 发出 OID。 这些运行时配置更改可以包括 **NicFriendlyName**、 **NetCfgInstanceId**、 **MTU**、 **NumaNodeId**、 **PermanentMacAddress**、 **VMMacAddress**、 **CurrentMacAddress**和 **VFAssigned**。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**PortId**成员指定进行更新通知的端口。 可扩展交换机扩展可以通过发出 oid [ \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)的 oid 查询请求，获取可扩展交换机上此端口和其他端口的参数信息。

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**index**成员指定正在为其进行更新通知的网络适配器的索引。 具有指定 **索引** 值的网络适配器连接到由 **PortId** 成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

此扩展必须遵循以下准则，以便处理 \_ 已更新 oid 交换机 NIC 的 oid 集请求 \_ \_ ：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) 结构。
-   扩展必须始终将此 OID 集请求转发到基础扩展。 扩展不能完成请求。
-   扩展不得颁发其自己的 OID \_ 交换机 NIC 更新的 oid 设置 \_ 请求 \_ 。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成更新 OID 交换机 NIC 的 OID 查询 \_ 请求 \_ \_ ，并返回以下状态代码。

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
[*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID \_ 交换机 \_ NIC \_ 断开连接](oid-switch-nic-disconnect.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

