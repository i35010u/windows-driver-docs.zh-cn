---
title: OID_SWITCH_NIC_UPDATED
description: Hyper-v 可扩展交换机的协议边缘向可扩展交换机驱动程序堆栈发出 OID_SWITCH_NIC_UPDATED 的对象标识符（OID）设置请求。
ms.assetid: C1B446A3-861F-41B4-99EF-C7CB45F86F39
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_UPDATED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1b2e8e5bd806e8ce87f10a797bd6e972f2529996
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843942"
---
# <a name="oid_switch_nic_updated"></a>OID\_交换机\_NIC\_更新


Hyper-v 可扩展交换机的协议边缘发出\_交换机\_NIC 的对象标识符（OID）设置请求，\_更新为可扩展交换机驱动程序堆栈。 此 OID 请求通知底层的可扩展交换机扩展关于网络适配器的参数更新。 仅为已连接并且尚未开始断开连接过程的 Nic 发出 OID。 这些运行时配置更改可以包括**NicFriendlyName**、 **NetCfgInstanceId**、 **MTU**、 **NumaNodeId**、 **PermanentMacAddress**、 **VMMacAddress**、 **CurrentMacAddress**和**VFAssigned**.

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

NDIS\_交换机的**PortId**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定进行更新通知的端口。 可扩展交换机扩展可以通过发出 oid [\_switch\_端口\_数组](oid-switch-port-array.md)的 oid 查询请求，获取可扩展交换机上此端口和其他端口的参数信息。

NDIS\_交换机的**索引**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定正在为其进行更新通知的网络适配器的索引。 具有指定**索引**值的网络适配器连接到由**PortId**成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

扩展必须遵循以下准则，以便处理\_交换机\_NIC\_更新的 OID 集请求：

-   扩展不能修改与 OID 请求关联[ **\_NIC\_参数结构的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)。
-   扩展必须始终将此 OID 集请求转发到基础扩展。 扩展不能完成请求。
-   扩展不能\_NIC\_更新\_交换机的 oid 的 OID 设置请求。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID\_交换机的 OID 查询请求\_NIC\_更新并返回以下状态代码。

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
[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[ **\_NIC\_参数的 NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID\_交换机\_NIC\_断开连接](oid-switch-nic-disconnect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 




