---
title: OID_SWITCH_NIC_DELETE
description: HYPER-V 可扩展交换机的协议边缘可扩展交换机驱动程序堆栈向发出 OID_SWITCH_NIC_DELETE 的对象标识符 (OID) 集请求。
ms.assetid: 7564EA39-09F5-45A3-81A0-F8DD2B23B639
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0f4079cc6ca4175e389335b17a6868423db6e315
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543108"
---
# <a name="oidswitchnicdelete"></a>OID\_交换机\_NIC\_删除


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_删除到可扩展交换机驱动程序堆栈。 此 OID 请求通知基础有关删除可扩展交换机端口和网络适配器之间的连接的可扩展的交换机扩展。 可扩展交换机的协议边缘之前通知扩展时颁发的 OID 集请求，正在删除此连接[OID\_切换\_NIC\_断开连接](oid-switch-nic-disconnect.md)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_开关\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的端口为其删除正在进行通知。 可扩展交换机扩展可以通过发出的 OID 查询请求获取此信息以及其他端口可扩展交换机上的参数信息[OID\_切换\_端口\_数组](oid-switch-port-array.md)。

**索引**的成员[ **NDIS\_开关\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的网络适配器的索引为其删除通知进行了。 使用指定的网络适配器**索引**值连接到指定的可扩展交换机端口**PortId**成员。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

之前该协议的可扩展交换机边缘发出 OID\_切换\_NIC\_DELETE 请求，它可以保证所有挂起的发送或接收数据包的请求已指定的网络适配器连接已完成。 已完成的所有挂起的连接的适配器的 OID 请求，以及连接的适配器的可扩展交换机引用计数器具有零值，还可保证协议边缘。

**请注意**  如果扩展已通过调用递增的网络适配器可扩展交换机引用计数器[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)，OID\_交换机\_NIC\_引用计数器为非零值时不发出 DELETE 请求。 扩展递减可扩展交换机引用计数器通过调用[ *DereferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598141)。

 

扩展必须遵守以下原则处理 OID 设置请求的 OID\_交换机\_NIC\_删除：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)与 OID 请求关联的结构。

-   扩展始终将转发对基础扩展的 OID 集请求。 扩展必须完成请求。

-   扩展必须发出其自己的 OID 的 OID 集请求\_交换机\_NIC\_删除。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于每个绑定到外部网络适配器的物理网络适配器，可扩展交换机的协议边缘会发出一个单独的 OID 集请求的 OID\_切换\_NIC\_删除。 每个 OID 集请求指定一个不同的网络适配器连接的索引值。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

    扩展必须维护每个基础物理适配器的连接状态。 有关在其中的物理网络适配器可以绑定到外部网络适配器的不同配置的详细信息，请参阅[的物理网络适配器配置的类型](https://msdn.microsoft.com/library/windows/hardware/hh582274)。

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_NIC\_删除并返回以下状态代码。

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
[*DereferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598141)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[OID\_交换机\_NIC\_断开连接](oid-switch-nic-disconnect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)

 

 




