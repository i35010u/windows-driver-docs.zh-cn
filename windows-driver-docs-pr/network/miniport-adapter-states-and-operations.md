---
title: 微型端口适配器状态和操作
description: 微型端口适配器状态和操作
keywords:
- 微型端口适配器 WDK 网络，状态
- 适配器 WDK 网络，状态
- 微型端口适配器 WDK 网络，操作
- 适配器 WDK 网络，操作
- 暂停状态 WDK 网络
- 关闭状态 WDK 网络
- 正在初始化状态 WDK ne
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58354afdbd2b58368993816bb59b5f7f16a2c291
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802327"
---
# <a name="miniport-adapter-states-and-operations"></a>微型端口适配器状态和操作





对于它管理的每个适配器，NDIS 6.0 或更高版本的微型端口驱动程序必须支持以下操作状态集：

<a href="" id="halted"></a>中断  
停止状态是所有适配器的初始状态。 当适配器处于暂停状态时，NDIS 可以调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数来初始化适配器。

<a href="" id="shutdown"></a>立即  
在关闭状态下，必须先进行系统关闭并重启，然后系统才能再次使用该适配器。

<a href="" id="initializing"></a>正在初始化  
在 "正在初始化" 状态下，微型端口驱动程序完成初始化适配器所需的任何操作。

<a href="" id="paused"></a>悬停  
在暂停状态下，适配器不指示接收的网络数据或接受发送请求。

<a href="" id="restarting"></a>重新  
在重新启动状态下，微型端口驱动程序完成了重新启动适配器的发送和接收操作所需的任何操作。

<a href="" id="running"></a>正在运行  
在运行状态下，微型端口驱动程序对适配器执行发送和接收处理。

<a href="" id="pausing"></a>暂停  
在暂停状态下，微型端口驱动程序会完成停止适配器的发送和接收操作所需的任何操作。

在下表中，标题是适配器状态。 主要事件在第一列中列出。 表中的其余条目指定了在状态中发生事件后适配器进入的下一个状态。 空白条目表示无效的事件/状态组合。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件 \ 状态</th>
<th align="left">中断</th>
<th align="left">关机</th>
<th align="left">正在初始化</th>
<th align="left">已暂停</th>
<th align="left">重新启动</th>
<th align="left">正在运行</th>
<th align="left">正在暂停</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a></p></td>
<td align="left"><p>正在初始化</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>初始化已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)"><em>MiniportShutdownEx</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>关机</p></td>
<td align="left"><p>关机</p></td>
<td align="left"><p>关机</p></td>
<td align="left"><p>关机</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>MiniportHaltEx</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>中断</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart" data-raw-source="[&lt;em&gt;MiniportRestart&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)"><em>MiniportRestart</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>重新启动</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>重新启动已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)"><em>MiniportPause</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在暂停</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>暂停完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
</tr>
<tr class="odd">
<td align="left"><p>初始化失败</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>中断</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>重新启动失败</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>发送和接收操作</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>正在暂停</p></td>
</tr>
<tr class="even">
<td align="left"><p>OID 请求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"><p>重新启动</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>正在暂停</p></td>
</tr>
</tbody>
</table>

 

**注意**  上表中列出的事件是 NDIS 6.0 或更高版本适配器的主要事件。

 

**注意**  Reset 操作不会影响微型端口适配器操作状态。 正在执行重置操作时，适配器的状态可能会发生变化。 例如，当正在进行重置操作时，NDIS 可能会调用驱动程序的暂停处理程序。 在这种情况下，驱动程序可以按任意顺序完成重置或暂停操作，同时满足每个操作的一般要求。 对于 reset 操作，驱动程序可能会导致传输请求数据包失败，或者可以将它们保留在队列中，稍后再完成。 但是，你应注意，如果某个过量驱动程序的传输数据包处于挂起状态，则无法完成暂停操作。

 

主要微型端口驱动程序事件定义如下：

<a href="" id="miniportinitializeex"></a>MiniportInitializeEx  
NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数来初始化适配器。 有关适配器初始化的详细信息，请参阅 [初始化微型端口适配器](initializing-a-miniport-adapter.md)。

<a href="" id="initialize-is-complete"></a>初始化已完成  
成功返回 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 后，初始化操作完成，并且适配器处于暂停状态。

<a href="" id="miniportshutdownex"></a>MiniportShutdownEx  
NDIS 调用驱动程序的 [*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 函数来关闭适配器。 有关详细信息，请参阅 [微型端口适配器关闭](miniport-adapter-shutdown.md)。

<a href="" id="miniporthaltex"></a>MiniportHaltEx  
NDIS 调用驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数来停止适配器。 有关详细信息，请参阅 [停止微型端口适配器](halting-a-miniport-adapter.md)。

<a href="" id="miniportrestart"></a>MiniportRestart  
NDIS 调用驱动程序的 [**MiniportRestart**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart) 函数以重新启动已暂停的适配器。 由于适配器在初始化后处于暂停状态，因此在适配器初始化完成后，还需要使用此事件来启动适配器。 有关详细信息，请参阅 [启动适配器](starting-an-adapter.md)。

<a href="" id="restart-is-complete"></a>重新启动已完成  
驱动程序准备好处理发送和接收操作后，重启操作将完成，并且适配器处于 "正在运行" 状态。

<a href="" id="miniportpause"></a>MiniportPause  
NDIS 调用驱动程序的 [*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause) 函数来暂停适配器。 有关详细信息，请参阅 [暂停适配器](pausing-an-adapter.md)。

<a href="" id="pause-is-complete"></a>暂停完成  
驱动程序完成停止发送和接收操作所需的所有操作后，暂停操作完成，并且适配器处于暂停状态。

**注意**  在暂停操作完成之前，驱动程序必须等待 NDIS 返回所有未完成的接收指示。

 

<a href="" id="initialize-failed"></a>初始化失败  
如果 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数，并且初始化尝试失败，则适配器将返回到 "已停止" 状态。

<a href="" id="restart-failed"></a>重新启动失败  
如果 NDIS 调用驱动程序的 [**MiniportRestart**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart) 函数，并且重新启动尝试失败，则该适配器将保持暂停状态。

<a href="" id="send-and-receive-operations"></a>发送和接收操作  
驱动程序必须在正在运行和正在暂停的状态处理发送和接收操作。 有关发送和接收操作的详细信息，请参阅 [微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md)。

<a href="" id="oid-requests"></a>OID 请求  
驱动程序必须在正在运行、正在重新启动、已暂停和正在暂停的状态下处理 OID 请求。 有关 OID 请求的详细信息，请参阅 [对适配器的 Oid 请求](miniport-adapter-oid-requests.md)。

## <a name="related-topics"></a>相关主题


[停止微型端口适配器](halting-a-miniport-adapter.md)

[初始化微型端口适配器](initializing-a-miniport-adapter.md)

[微型端口适配器关闭](miniport-adapter-shutdown.md)

[微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md)

[暂停适配器](pausing-an-adapter.md)

[启动适配器](starting-an-adapter.md)

