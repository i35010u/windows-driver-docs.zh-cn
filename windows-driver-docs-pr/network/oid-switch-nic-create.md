---
title: OID_SWITCH_NIC_CREATE
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_NIC_CREATE 通知基础可扩展交换机扩展，可扩展交换机端口之间建立新连接和外部或虚拟网络适配器。 完全建立连接后，可扩展交换机的协议边缘颁发 OID_SWITCH_NIC_CONNECT OID 集请求。
ms.assetid: 1D6B2C6B-A63E-4A20-B534-AF12714F5FB5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_CREATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f3584f254ecb9d46de4431daace33fa0d86dd676
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344225"
---
# <a name="oidswitchniccreate"></a>OID\_交换机\_NIC\_创建


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_创建通知基础可扩展交换机扩展建立新连接之间的可扩展交换机端口和外部或虚拟网络适配器。 完全建立连接后，可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](oid-switch-nic-connect.md)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_切换\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的可扩展交换机端口它由正在创建通知。 可扩展交换机扩展可以通过发出的 OID 查询请求获取此信息以及其他端口可扩展交换机上的参数信息[OID\_切换\_端口\_数组](oid-switch-port-array.md)。

**索引**的成员[ **NDIS\_开关\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的网络适配器的索引为其创建通知进行了。 使用指定的网络适配器**索引**值连接到指定的可扩展交换机端口**PortId**成员。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

当它收到 OID 集请求的 OID\_交换机\_NIC\_创建、 扩展必须遵守以下原则：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)与 OID 请求关联的结构。

-   OID\_切换\_NIC\_创建请求仅通知正在启动新的可扩展交换机连接的扩展插件和该数据包流量可能很快就会开始出现通过指定端口。 但是，该扩展无法使用的端口，直到可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](oid-switch-nic-connect.md)。 发出该 OID 之前, 扩展必须执行以下操作：

    -   生成可扩展的交换机端口上为其网络适配器连接到的任何数据包流量 OID\_切换\_NIC\_发出创建 OID 请求。

    -   转发或源于的 OID 请求[OID\_交换机\_NIC\_请求](oid-switch-nic-request.md)到为其基础网络适配器 OID\_开关\_NIC\_发出创建 OID 请求。

    -   转发或源于的 NDIS 状态迹象[ **NDIS\_状态\_交换机\_NIC\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598205)从为其基础网络适配器OID\_交换机\_NIC\_发出创建 OID 请求。

    -   调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)可扩展交换机端口上指定的网络适配器连接的可扩展交换机引用计数器递增。

    **请注意**  的扩展插件可能会截获发送或接收的 OID 的 OID 请求之间的指定端口的数据包\_交换机\_NIC\_创建并[OID\_开关\_NIC\_CONNECT](oid-switch-nic-connect.md)。 在这种情况下，该扩展应转发发送或接收数据包请求而不是取消它们。

     

-   扩展有权创建通知决策通过返回 NDIS\_状态\_数据\_不\_OID 请求被接受。 例如，如果扩展不能满足其配置的策略上指定的端口，该扩展应能阻止创建通知。

    如果扩展插件可以返回其他 NDIS\_状态\_*Xxx*还禁止状态代码，创建通知。 但是，返回状态代码为暂时性的情况下，如返回 NDIS\_状态\_资源，可能会导致创建通知的重试。

    如果扩展不能阻止 OID 请求，它在请求完成时应监视的状态。 该扩展应这样做可以确定 OID 请求已被否决的可扩展交换机控制路径中的基础扩展或可扩展交换机接口。

    **请注意**  如果来扩展仅可以禁止 OID 请求**索引**的成员[ **NDIS\_交换机\_NIC\_参数** ](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的网络适配器索引值为零。

     

-   如果扩展不能阻止创建通知，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)此 OID 请求转发到可扩展交换机驱动程序堆栈中的基础扩展。

    **请注意**  扩展应该监视此 OID 请求的完成状态。 扩展执行此检测中可扩展交换机驱动程序堆栈的基础扩展是否已被否决创建通知操作。

     

-   如果扩展将调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)转发此 OID 请求，该扩展将不会立即接收到的任何数据包流量或从可扩展交换机端口。 此外，该扩展不能立即注入发送或接收可扩展交换机端口的流量。

-   该扩展可以仅数据包将流量转发到可扩展交换机端口后可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](oid-switch-nic-connect.md)。

    **请注意**  在某些情况下之前 OID 设置的请求, 可能由可扩展切换到的端口转发数据包流量[OID\_切换\_NIC\_CONNECT](oid-switch-nic-connect.md)会发出。

     

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于每个绑定到外部网络适配器的物理网络适配器，可扩展交换机的协议边缘会发出一个单独的 OID 集请求的 OID\_切换\_NIC\_创建。 每个 OID 集请求指定一个不同的网络适配器连接的索引值。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

    扩展必须维护每个基础物理适配器的连接状态。 有关在其中的物理网络适配器可以绑定到外部网络适配器的不同配置的详细信息，请参阅[的物理网络适配器配置的类型](https://msdn.microsoft.com/library/windows/hardware/hh582274)。

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。

**请注意**  扩展必须发出其自己的 OID 的 OID 集请求\_交换机\_NIC\_创建。

 

### <a name="return-status-codes"></a>返回状态代码

如果该扩展完成 OID 集请求的 OID\_交换机\_NIC\_创建，它返回一个下面的状态代码。

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
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>扩展操作禁止创建通知。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_RESOURCES</p></td>
<td><p>该扩展被否决由于资源不足的情况创建通知。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>扩展操作由于其他原因禁止创建通知。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  如果扩展完成 OID 集请求，它必须返回 NDIS\_状态\_成功。

 

如果扩展不会完成 OID 集请求的 OID\_切换\_NIC\_可扩展交换机基础的微型端口边缘完成创建，该请求。 基础的微型端口边缘返回此 OID 集请求的以下状态代码：

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
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[OID\_交换机\_NIC\_连接](oid-switch-nic-connect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)

 

 




