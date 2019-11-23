---
title: Hyper-V 可扩展交换机端口和网络适配器状态
description: Hyper-V 可扩展交换机端口和网络适配器状态
ms.assetid: 1E2075E3-D7CC-4364-ABB2-D5969DB361B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7238a232dc5f58155429587aaaa004bae5b702c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823869"
---
# <a name="hyper-v-extensible-switch-port-and-network-adapter-states"></a>Hyper-V 可扩展交换机端口和网络适配器状态


Hyper-v 可扩展交换机接口管理以下组件的生存期：

<a href="" id="hyper-v-extensible-switch-ports"></a>Hyper-v 可扩展交换机端口  
与可扩展交换机之间的每个网络适配器连接由端口表示。 当 Hyper-v 子分区配置为连接到可扩展交换机的实例时，将创建端口。 根据交换机类型，还会为外部和内部网络适配器连接创建端口。 有关交换机类型的详细信息，请参阅[Hyper-v 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md)。

每个端口用于保存网络接口连接的配置。 如果网络接口连接的配置已删除或子分区已停止，则该端口将被断开并被删除。

有关此组件的详细信息，请参阅[Hyper-v 可扩展交换机端口](hyper-v-extensible-switch-ports.md)。

<a href="" id="hyper-v-extensible-switch-network-adapters"></a>Hyper-v 可扩展交换机网络适配器  
这些是连接到可扩展交换机端口的虚拟网络适配器。 这些虚拟网络适配器在 Hyper-v 子分区和父分区内公开。 这包括在子分区中公开的虚拟机（VM）网络适配器，以及包含基础物理网络适配器的外部网络适配器。

每个网络适配器连接都需要一个相应的可扩展交换机端口。 必须已在启动网络适配器连接之前创建了端口。 同样，必须先删除网络适配器连接，然后才能关闭端口并将其删除。

**请注意**  在某些情况下，可以在不使用网络适配器连接的情况下创建和删除可扩展的交换机端口。

 

例如，启动 Hyper-v 子分区时，可扩展交换机接口会在来宾操作系统内公开 VM 网络适配器之前创建端口。 公开并枚举 VM 网络适配器后，可扩展交换机接口会在 VM 网络适配器和可扩展交换机端口之间创建网络连接。 如果子分区已停止，可扩展交换机接口首先会删除网络连接，然后删除可扩展交换机端口。

有关此组件的详细信息，请参阅[Hyper-v 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)。

当可扩展交换机接口创建、删除或更改这些组件的配置时，它会发出对象标识符（OID）在可扩展交换机驱动程序堆栈下的设置请求。 执行此操作的目的是使底层可扩展交换机扩展可以获得有关组件状态及其配置的通知。 每个 OID 设置请求都会导致为这些组件提供状态转换。

在可扩展交换机实例上绑定和启用扩展时，它可以发出 Oid 来发现交换机的现有端口和网络适配器连接配置。

下图显示了可扩展交换机端口和网络适配器连接组件的各种状态。 该关系图还显示了导致组件的状态转换的 OID 设置请求。

![显示导致组件状态转换的 oid 集请求的流程图](images/vswitchstate.png)

以下列表描述了可扩展交换机端口和网络适配器连接组件的各种状态：

<a href="" id="port-not-created"></a>*未创建端口*  
在此状态下，可扩展交换机端口不存在。 在端口进入此状态之后，无法发出以先前创建的端口为目标的 OID 请求。

<a href="" id="port-created"></a>*端口已创建*  
当可扩展交换机接口发出 oid [\_switch\_端口\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)时，将在可扩展交换机上创建端口。 在此状态下，可扩展交换机接口和扩展可以发出针对端口的 OID 请求。

有关通过可扩展交换机驱动程序堆栈的 OID 流量的详细信息，请参阅[Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path.md)。

**请注意**  基础扩展可以使 OID 设置请求失败并拒绝端口创建。 此扩展通过以下方式实现此功能：完成 OID 请求，状态\_数据\_不\_接受。 如果执行此操作，则不会在可扩展交换机上创建端口。 有关此过程的详细信息，请参阅[Hyper-v 可扩展交换机端口](hyper-v-extensible-switch-ports.md)。

 

<a href="" id="network-adapter-connection-created"></a>*已创建网络适配器连接*  
当可扩展交换机接口发出 Oid 的 OID 集请求时[\_交换机\_NIC\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)时，将在可扩展交换机上创建与该端口的网络适配器连接。 在此状态下，可扩展交换机接口可以执行以下操作：

-   发出针对网络适配器连接的 OID 请求。

-   转发进出网络适配器连接的数据包流量。

新适配器还可以连接到现有端口，无需通过端口拆卸和创建序列。

在此状态下，扩展必须通过可扩展交换机扩展堆栈转发这些数据包和 OID 请求。 但是，扩展不能将数据包或 OID 请求发起或重定向到可扩展交换机上的其他网络适配器连接。

**请注意**  此状态下，扩展不能发出 OID 请求，也不能将数据包流量发送到网络适配器连接。

 

有关通过可扩展交换机驱动程序堆栈的 OID 流量的详细信息，请参阅[Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path.md)。

有关通过可扩展交换机驱动程序堆栈的数据包流量的详细信息，请参阅[Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

**请注意**  基础扩展可以使 OID 设置请求失败并拒绝网络适配器连接的创建。 如果是这样，则不会在可扩展交换机端口上创建连接。 有关此过程的详细信息，请参阅[Hyper-v 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)。

 

<a href="" id="network-adapter-connected"></a>*网络适配器已连接*  
当可扩展交换机接口发出 oid 的 OID 集请求时[\_交换机\_NIC\_连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)，网络适配器完全连接到可扩展交换机端口。 在此状态下，扩展现在可以执行以下操作：

-   发出针对网络适配器连接的 OID 请求。

-   将数据包流量发送到网络适配器连接。

-   将数据包流量重定向到网络适配器连接。 例如，该扩展可以将数据包从一个网络适配器连接重定向到可扩展交换机上的另一个连接。

    **请注意**  仅转发扩展可以执行此操作。 有关详细信息，请参阅[转发扩展](forwarding-extensions.md)。

     

<a href="" id="network-adapter-disconnected"></a>*网络适配器已断开连接*  
当可扩展交换机接口发出 Oid 的 OID 集请求时[\_交换机\_NIC\_断开](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)连接，网络适配器将从可扩展交换机端口断开连接。 例如，当公开了 VM 网络适配器的子分区已停止或外部网络适配器被禁用时，将发出此 OID 请求。

在此状态下，可扩展交换机扩展不能再发起以连接为目标的数据包或 OID 请求。 此外，转发扩展不能再将数据包重定向到连接。

**请注意**，在断开连接之前，可扩展交换机接口发出  挂起的数据包和 OID 请求可能仍会传递到该扩展。 但是，扩展必须转发数据包和 OID 请求，而不进行任何修改。

 

<a href="" id="network-adapter-connection-deleted"></a>*已删除网络适配器连接*  
在所有针对网络适配器连接的数据包流量和 OID 请求都完成之后，可扩展交换机接口会发出 oid [\_switch\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)的 oid 集请求，\_delete 从可扩展交换机中删除连接。

在此状态下，可扩展交换机接口将不再发出以连接为目标的数据包或 OID 请求。

<a href="" id="port-tearing-down"></a>*端口撕裂*  
当可扩展交换机接口发出 oid 的 OID 集请求时[\_交换机\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)时，可扩展交换机端口会被删除，以便准备删除。

在此状态下，可扩展交换机扩展不能再发起以该端口为目标的 OID 请求。

**请注意**，在端口开始分离进程之前，由可扩展交换机接口发出  挂起的 OID 请求可能仍会传递到该扩展。 但是，扩展必须转发 OID 请求，而不进行任何修改。

 

在所有以端口为目标的挂起 OID 请求完成之后，可扩展交换机接口会发出 oid [\_switch\_端口\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)的 oid 请求。 这会使端口转换为*未创建端口*状态。

扩展可以调用可扩展的 switch 处理程序函数来递增或递减端口或网络适配器连接组件上的引用计数器。 当组件的引用计数器为非零值时，可扩展交换机接口无法删除该组件。

扩展可以调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)或[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)来递增或递减可扩展交换机端口的引用计数器。 可以在端口达到*端口已创建*状态之后进行这些调用。 当端口已进入*端口撕裂*或*端口未创建*状态后，不能进行这些调用。

扩展可以调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)或[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)来递增或递减可扩展交换机网络适配器连接的引用计数器。 在连接到达*网络适配器连接*状态之后，可以进行这些调用。 在连接到达*网络适配器断开*连接或*网络适配器删除*状态之后，不能进行这些调用。

下表介绍了基于可扩展交换机端口或网络适配器连接组件状态所允许的操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组件状态</th>
<th align="left">是否允许对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port" data-raw-source="[&lt;em&gt;ReferenceSwitchPort&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)"><em>ReferenceSwitchPort</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port" data-raw-source="[&lt;em&gt;DereferenceSwitchPort&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)"><em>DereferenceSwitchPort</em></a>的调用？</th>
<th align="left">是否允许对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic" data-raw-source="[&lt;em&gt;ReferenceSwitchNic&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)"><em>ReferenceSwitchNic</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic" data-raw-source="[&lt;em&gt;DereferenceSwitchNic&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)"><em>DereferenceSwitchNic</em></a>的调用？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>未创建端口</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>端口已创建</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>已创建网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>网络适配器已连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>网络适配器已断开连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>已删除网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>端口撕裂</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组件状态</th>
<th align="left">允许对端口使用来自可扩展交换机的 OID 请求？</th>
<th align="left">来自端口允许的扩展的 OID 请求？</th>
<th align="left">允许网络适配器连接的来自可扩展交换机的 OID 请求？</th>
<th align="left">允许来自网络适配器连接的扩展的 OID 请求？</th>
<th align="left">允许通过网络适配器连接来自可扩展交换机的数据包流量？</th>
<th align="left">允许通过网络适配器连接进行的扩展中的数据包流量？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>未创建端口</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>端口已创建</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>已创建网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>网络适配器已连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>网络适配器已断开连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>已删除网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>端口撕裂</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

 

 





