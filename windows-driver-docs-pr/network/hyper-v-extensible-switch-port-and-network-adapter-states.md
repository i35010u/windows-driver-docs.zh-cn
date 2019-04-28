---
title: Hyper-V 可扩展交换机端口和网络适配器状态
description: Hyper-V 可扩展交换机端口和网络适配器状态
ms.assetid: 1E2075E3-D7CC-4364-ABB2-D5969DB361B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bd220ab2293647821d2615c9831db60bf953363
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349524"
---
# <a name="hyper-v-extensible-switch-port-and-network-adapter-states"></a>Hyper-V 可扩展交换机端口和网络适配器状态


HYPER-V 可扩展交换机接口管理以下组件的生存期：

<a href="" id="hyper-v-extensible-switch-ports"></a>HYPER-V 可扩展交换机端口  
每个网络适配器连接到可扩展的交换机端口由表示。 当 HYPER-V 子分区配置为连接到可扩展交换机的实例上创建端口。 具体取决于交换机类型中，端口还会创建外部和内部网络适配器连接。 有关交换机类型的详细信息，请参阅[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)。

每个端口用来保存网络接口连接的配置。 如果网络接口连接的配置被删除或停止子分区，该端口是在拆解，删除。

有关此组件的详细信息，请参阅[HYPER-V 可扩展交换机端口](hyper-v-extensible-switch-ports.md)。

<a href="" id="hyper-v-extensible-switch-network-adapters"></a>HYPER-V 可扩展交换机的网络适配器  
这些是连接到可扩展交换机端口的虚拟网络适配器。 这些虚拟网络适配器的 HYPER-V 子和父分区中公开。 这包括在子分区和与基础物理网络适配器成组的外部网络适配器中公开的虚拟机 (VM) 网络适配器。

每个网络适配器连接需要相应的可扩展交换机端口。 网络适配器连接时，将启动之前，该端口必须已创建。 同样，必须删除之前该端口可关闭网络适配器连接并将其删除。

**请注意**  在某些情况下，创建和删除，但没有任何时候将网络适配器连接的可扩展的交换机端口。

 

例如，当启动 HYPER-V 子分区时，可扩展交换机接口创建端口之前的 VM 网络适配器公开在来宾操作系统中。 公开和枚举的 VM 网络适配器后，可扩展交换机接口用于创建 VM 网络适配器和可扩展的交换机端口之间的网络连接。 如果子分区已停止，可扩展交换机接口删除网络连接，，然后删除可扩展交换机端口。

有关此组件的详细信息，请参阅[HYPER-V 可扩展交换机的网络适配器](hyper-v-extensible-switch-network-adapters.md)。

当可扩展交换机接口创建、 删除或更改这些组件的配置时，它会发出可扩展交换机在驱动程序堆栈的下层对象标识符 (OID) 集请求。 执行此操作，以便基础可扩展交换机扩展可以通知该组件及其配置的状态。 每个 OID 状态转换为这些组件中设置请求结果。

当绑定并可扩展交换机实例上启用扩展时，它可以发布 Oid 来发现现有的端口和交换机的网络适配器连接配置。

下图显示的各种状态的可扩展的交换机端口和网络适配器连接组件。 该图也显示导致该组件的状态转换的 OID 集请求。

![显示 oid 流程图将会导致该组件的状态转换的请求设置](images/vswitchstate.png)

以下列表描述可扩展交换机端口和网络适配器连接组件的各种状态：

<a href="" id="port-not-created"></a>*不创建端口*  
在此状态下，可扩展交换机上不存在可扩展交换机端口。 OID 请求后进入此状态的端口不能颁发先前创建的端口的目标。

<a href="" id="port-created"></a>*创建端口*  
可扩展交换机接口时颁发的 OID 集请求[OID\_切换\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)，可扩展交换机上创建端口。 在此状态下，可扩展交换机接口和扩展可以发出 OID 请求的目标端口。

有关通过可扩展交换机驱动程序堆栈的 OID 流量的详细信息，请参阅[HYPER-V 可扩展交换机控制路径](hyper-v-extensible-switch-control-path.md)。

**请注意**  基础扩展可以使该 OID 集请求失败并能阻止端口创建。 通过完成状态为 OID 请求的扩展插件实现这\_数据\_不\_已接受。 如果执行此操作，不是可扩展的交换机上创建端口。 此过程的详细信息，请参阅[HYPER-V 可扩展交换机端口](hyper-v-extensible-switch-ports.md)。

 

<a href="" id="network-adapter-connection-created"></a>*创建的网络适配器连接*  
可扩展交换机接口时颁发的 OID 集请求[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)，可扩展交换机上创建网络适配器连接到端口。 在此状态下，可扩展交换机接口可以执行以下步骤：

-   发出 OID 请求面向连接的网络适配器。

-   转发与网络适配器连接的数据包流量。

还有可能用于新适配器连接到现有的端口，而无需通过端口拆解，并创建序列。

在此状态下，这些数据包和 OID 请求通过可扩展交换机扩展堆栈必须转发扩展。 但是，该扩展不能发起或将数据包或 OID 请求重定向到其他网络适配器连接的可扩展交换机上。

**请注意**  处于此状态的扩展插件必须不发出 OID 请求或源自网络适配器连接到的数据包流量。

 

有关通过可扩展交换机驱动程序堆栈的 OID 流量的详细信息，请参阅[HYPER-V 可扩展交换机控制路径](hyper-v-extensible-switch-control-path.md)。

有关通过可扩展交换机驱动程序堆栈的数据包流量的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

**请注意**  基础扩展可以失败 OID 集请求并能阻止的网络适配器连接的创建。 如果是这样，不是可扩展交换机端口上创建连接。 此过程的详细信息，请参阅[HYPER-V 可扩展交换机的网络适配器](hyper-v-extensible-switch-network-adapters.md)。

 

<a href="" id="network-adapter-connected"></a>*连接的网络适配器*  
可扩展交换机接口时颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)，网络适配器完全连接到可扩展交换机端口。 在此状态下，该扩展现在可以执行以下：

-   发出 OID 请求面向连接的网络适配器。

-   源自网络适配器连接到的数据包流量。

-   数据包流量重定向到网络适配器连接。 例如，扩展可以将数据包从一个网络适配器连接到可扩展的交换机上的另一个连接重定向。

    **请注意**  仅转发扩展可以执行此操作。 有关详细信息，请参阅[转发扩展](forwarding-extensions.md)。

     

<a href="" id="network-adapter-disconnected"></a>*断开连接的网络适配器*  
可扩展交换机接口时颁发的 OID 集请求[OID\_切换\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)，可扩展交换机端口从正在断开连接的网络适配器。 例如，子分区，公开的 VM 网络适配器，已停止或外部网络适配器处于禁用状态时发出此 OID 请求。

在此状态下，可扩展交换机扩展可以不再源自数据包或 OID 请求连接该目标。 此外，转发扩展可不再重定向的数据包到连接。

**请注意**  挂起的数据包和 OID 可能仍将之前断开连接变得可扩展交换机接口发出的请求传送到该扩展。 但是，该扩展必须转发的数据包和 OID 请求而无需进行任何修改。

 

<a href="" id="network-adapter-connection-deleted"></a>*已删除的网络适配器连接*  
完成所有数据包流量和目标网络适配器连接的 OID 请求后，可扩展交换机接口颁发的 OID 集请求[OID\_切换\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598264)若要从可扩展的交换机中删除连接。

在此状态下，可扩展交换机接口将不再发出数据包或 OID 请求连接该目标。

<a href="" id="port-tearing-down"></a>*关闭端口*  
可扩展交换机接口时颁发的 OID 集请求[OID\_切换\_端口\_拆卸](https://msdn.microsoft.com/library/windows/hardware/hh598279)，正在删除准备过程正在拆解可扩展交换机端口。

在此状态下，可扩展交换机扩展可以不再源自 OID 请求该目标端口。

**请注意**  挂起 OID 端口启动其拆解过程之前由可扩展交换机接口发出的请求仍可能会提供给扩展。 但是，扩展必须转发 OID 请求，而无需进行任何修改。

 

所有挂起的 OID 目标端口的请求完成后，可扩展交换机接口颁发的 OID 集请求[OID\_切换\_端口\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598273)。 这将导致转换到端口*不创建端口*状态。

该扩展可以调用要递增或递减引用计数器对端口或网络适配器连接组件的可扩展交换机处理程序函数。 组件的引用计数器为非零值，而可扩展交换机接口不能删除该组件。

该扩展可以调用[ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295)或[ *DereferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598142)要递增或递减引用计数器，用于可扩展交换机端口。 达到该端口后，这些调用可以进行*创建的端口*状态。 达到该端口后，这些调用必须建立*端口拆除*或*端口不会创建*状态。

该扩展可以调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)或[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)要递增或递减引用计数器，用于可扩展交换机的网络适配器连接。 已达到连接之后，可以进行这些调用*连接的网络适配器*状态。 达到该连接后，这些调用必须建立*网络适配器已断开*或*删除的网络适配器*状态。

下表描述了基于可扩展交换机端口或网络适配器连接组件的状态允许的操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组件状态</th>
<th align="left">调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh598295" data-raw-source="[&lt;em&gt;ReferenceSwitchPort&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598295)"> <em>ReferenceSwitchPort</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/hh598142" data-raw-source="[&lt;em&gt;DereferenceSwitchPort&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598142)"> <em>DereferenceSwitchPort</em> </a>允许？</th>
<th align="left">调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh598294" data-raw-source="[&lt;em&gt;ReferenceSwitchNic&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598294)"> <em>ReferenceSwitchNic</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/hh598141" data-raw-source="[&lt;em&gt;DereferenceSwitchNic&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598141)"> <em>DereferenceSwitchNic</em> </a>允许？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>不创建端口</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>创建端口</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建的网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>连接的网络适配器</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>断开连接的网络适配器</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>已删除的网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>关闭端口</p></td>
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
<th align="left">从可扩展的交换机端口允许 OID 请求？</th>
<th align="left">从允许的端口的扩展的 OID 请求？</th>
<th align="left">从允许的网络适配器连接的可扩展交换机的 OID 请求？</th>
<th align="left">从允许的网络适配器连接的扩展的 OID 请求？</th>
<th align="left">从允许通过网络适配器连接的可扩展交换机的数据包流量？</th>
<th align="left">从扩展允许通过网络适配器连接的数据包流量？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>不创建端口</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>创建端口</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建的网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>连接的网络适配器</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>断开连接的网络适配器</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>已删除的网络适配器连接</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>关闭端口</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

 

 





