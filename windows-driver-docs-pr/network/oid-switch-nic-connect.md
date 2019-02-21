---
title: OID_SWITCH_NIC_CONNECT
description: HYPER-V 可扩展的协议边缘切换对象标识符 (OID) 设置的 OID_SWITCH_NIC_CONNECT 的请求，以通知基础可扩展交换机扩展的可扩展交换机端口和网络适配器之间的网络连接问题完全建立。 协议边缘以前扩展进行此连接建立它发出 OID_SWITCH_NIC_CREATE OID 集请求时收到通知。
ms.assetid: 98A4AD28-2716-40DD-AE46-70969A23FAB7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_CONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0a5a9a95aa1390d530160326764507d6bd086a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526286"
---
# <a name="oidswitchnicconnect"></a>OID\_交换机\_NIC\_连接


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_连接以通知基础可扩展交换机扩展的之间的网络连接完全建立可扩展交换机端口和一个网络适配器。 当它颁发的 OID 集请求正在此连接的协议之前通知的边缘扩展建立[OID\_交换机\_NIC\_创建](oid-switch-nic-create.md)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_切换\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的可扩展交换机端口这进行连接通知。 可扩展的交换机扩展可以获取此端口和其他可扩展交换机的参数信息端口按以下方式：

-   通过发出 OID 查询的请求[OID\_交换机\_端口\_数组](oid-switch-port-array.md)。 该扩展在发出此 OID [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)时，才 OID\_开关\_参数返回[ **NDIS\_开关\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598220)结构**IsActive**设置为 TRUE。 如果**IsActive**为 FALSE 时，扩展问题 OID 时**NetEventSwitchActivate** [ **NET\_PNP\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff568751)扩展微型端口适配器颁发。

-   通过检查各种 OID 设置的请求[OID\_交换机\_端口\_创建](oid-switch-port-create.md)并[OID\_交换机\_端口\_删除](oid-switch-port-delete.md).

**索引**的成员[ **NDIS\_开关\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的网络适配器的索引为其连接通知进行了。 使用指定的网络适配器**索引**值连接到指定的可扩展交换机端口**PortId**成员。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

当它收到 OID 集请求的 OID\_交换机\_NIC\_连接中，该扩展必须遵守以下原则：

-   当 OID\_切换\_NIC\_连接请求完成时 NDIS\_状态\_成功、 网络连接和可扩展的交换机端口都是完全正常运行。 该扩展可以生成或数据包将流量转发到端口的网络连接。 扩展还可以颁发可扩展交换机 Oid 或用作源端口使用的端口的状态指示。 扩展还可以调用[ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295)递增该端口的可扩展交换机引用计数器。

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)与 OID 请求关联的结构。

-   扩展必须始终调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)此 OID 请求转发到基础扩展。 扩展必须完成 OID 请求本身。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于每个绑定到外部网络适配器的物理网络适配器，可扩展交换机的协议边缘会发出一个单独的 OID 集请求的 OID\_切换\_NIC\_连接。 每个 OID 集请求指定一个不同的网络适配器连接的索引值。 有关这些值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

    扩展必须维护每个基础的物理适配器，绑定到外部网络适配器的连接状态。 有关在其中的物理网络适配器可以绑定到外部网络适配器的不同配置的详细信息，请参阅[的物理网络适配器配置的类型](https://msdn.microsoft.com/library/windows/hardware/hh582274)。

**请注意**  扩展必须发出其自己的 OID 的 OID 集请求\_交换机\_NIC\_连接。

 

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 集请求的 OID\_切换\_NIC\_连接，并返回以下状态代码。

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NdisFReturnNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562613)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[OID\_SWITCH\_NIC\_CREATE](oid-switch-nic-create.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)

 

 




