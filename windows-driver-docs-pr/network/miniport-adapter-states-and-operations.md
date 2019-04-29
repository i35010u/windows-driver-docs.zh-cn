---
title: 微型端口适配器状态和操作
description: 微型端口适配器状态和操作
ms.assetid: b47e2cbe-9da3-4600-9afe-b082e60b87fb
keywords:
- 微型端口适配器 WDK 网络状态
- 适配器 WDK 网络状态
- 微型端口适配器 WDK 网络操作
- 适配器 WDK 网络操作
- 非暂停的状态下 WDK 网络
- 关闭状态 WDK 网络
- 正在初始化状态 WDK ne
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f5e566d2e491fba9d2d7018687465b5bbf526c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379811"
---
# <a name="miniport-adapter-states-and-operations"></a>微型端口适配器状态和操作





对于它所管理的每个适配器，NDIS 6.0 或更高版本的微型端口驱动程序必须支持以下一组操作状态：

<a href="" id="halted"></a>暂停  
暂停状态是所有适配器的初始状态。 NDIS 当适配器处于暂停状态时，可以调用的驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数以初始化适配器。

<a href="" id="shutdown"></a>关闭  
在关闭状态下，系统关闭和重新启动之前必须进行系统可以再次使用适配器。

<a href="" id="initializing"></a>正在初始化  
Initializing 状态时，微型端口驱动程序完成初始化适配器所需的任何操作。

<a href="" id="paused"></a>已暂停  
在已暂停状态下，适配器不指示接收的网络数据，也接受发送请求。

<a href="" id="restarting"></a>重新启动  
在正在重新启动状态下，微型端口驱动程序完成重启发送和接收适配器的操作所需的任何操作。

<a href="" id="running"></a>运行  
处于运行状态的微型端口驱动程序执行发送和接收适配器的处理。

<a href="" id="pausing"></a>暂停  
在暂停状态下，微型端口驱动程序完成停止发送和接收适配器的操作所需的任何操作。

下表中的标题是适配器状态。 第一列中列出了主要的事件。 表中的条目的其余部分指定下一个状态适配器进入后处于状态发生的事件。 为空白条目表示无效的事件状态组合。

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
<th align="left">暂停</th>
<th align="left">关机</th>
<th align="left">初始化</th>
<th align="left">已暂停</th>
<th align="left">重新启动</th>
<th align="left">正在运行</th>
<th align="left">暂停</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"><em>MiniportInitializeEx</em></a></p></td>
<td align="left"><p>初始化</p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559449" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559449)"><em>MiniportShutdownEx</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>关机</p></td>
<td align="left"><p>关机</p></td>
<td align="left"><p>关机</p></td>
<td align="left"><p>关机</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559388" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559388)"><em>MiniportHaltEx</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559435" data-raw-source="[&lt;em&gt;MiniportRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559435)"><em>MiniportRestart</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>重新启动</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>重启已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559418" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559418)"><em>MiniportPause</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>暂停</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>暂停已完成</p></td>
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
<td align="left"><p>暂停</p></td>
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
<td align="left"><p>暂停</p></td>
</tr>
<tr class="even">
<td align="left"><p>OID 请求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"><p>重新启动</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>暂停</p></td>
</tr>
</tbody>
</table>

 

**请注意**  上表中列出的事件是 NDIS 6.0 或更高版本的适配器的主要事件。

 

**请注意**  重置操作不会影响微型端口适配器操作状态。 重置操作正在进行时，可能会更改该适配器的状态。 例如，NDIS 可能会重置操作正在进行中的时调用的驱动程序暂停处理程序。 在这种情况下，该驱动程序可以完成重置或暂停操作，按任意顺序遵循每个操作的常规要求。 对于重置操作，该驱动程序可能会传输请求数据包失败或它可以使它们保持排队和完成这些更高版本。 但是，您应该注意基础驱动程序无法完成暂停操作时其传输数据包处于挂起状态。

 

主要的微型端口驱动程序事件定义，如下所示：

<a href="" id="miniportinitializeex"></a>MiniportInitializeEx  
NDIS 称为驱动程序的[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数以初始化适配器。 有关适配器初始化的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

<a href="" id="initialize-is-complete"></a>初始化已完成  
之后[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)成功，返回初始化操作已完成，并且适配器处于已暂停状态。

<a href="" id="miniportshutdownex"></a>MiniportShutdownEx  
NDIS 称为驱动程序的[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)函数关闭适配器。 有关详细信息，请参阅[微型端口适配器关闭](miniport-adapter-shutdown.md)。

<a href="" id="miniporthaltex"></a>MiniportHaltEx  
NDIS 称为驱动程序的[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数停止适配器。 有关详细信息，请参阅[停止微型端口适配器](halting-a-miniport-adapter.md)。

<a href="" id="miniportrestart"></a>MiniportRestart  
NDIS 称为驱动程序的[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)函数以重新启动暂停的适配器。 因为适配器不处于已暂停状态初始化后，此事件也需要适配器初始化完成后启动该适配器。 有关详细信息，请参阅[启动适配器](starting-an-adapter.md)。

<a href="" id="restart-is-complete"></a>重启已完成  
驱动程序准备就绪后用于处理发送和接收操作，在重新启动操作已完成，适配器处于运行状态。

<a href="" id="miniportpause"></a>MiniportPause  
NDIS 称为驱动程序的[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)函数来暂停适配器。 有关详细信息，请参阅[暂停适配器](pausing-an-adapter.md)。

<a href="" id="pause-is-complete"></a>暂停已完成  
该驱动程序所需的所有操作都完成后停止发送和接收操作、 暂停操作已完成和适配器处于已暂停状态。

**请注意**  驱动程序必须等待 NDIS 以返回所有其未完成的指示之前收到暂停操作已完成。

 

<a href="" id="initialize-failed"></a>初始化失败  
如果 NDIS 调用驾[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数和初始化尝试失败，适配器返回到暂停状态。

<a href="" id="restart-failed"></a>重新启动失败  
如果 NDIS 调用驾[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)函数，并重新启动尝试失败，该适配器将保持在已暂停状态。

<a href="" id="send-and-receive-operations"></a>发送和接收操作  
驱动程序必须处理发送和接收操作在运行和暂停状态。 有关详细信息大约发送和接收操作，请参阅[微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md)。

<a href="" id="oid-requests"></a>OID 请求  
驱动程序必须处理在运行、 正在重新启动、 已暂停，OID 请求和暂停状态。 有关 OID 的请求的详细信息，请参阅[适配器的 OID 请求](miniport-adapter-oid-requests.md)。

## <a name="related-topics"></a>相关主题


[正在停止微型端口适配器](halting-a-miniport-adapter.md)

[初始化微型端口适配器](initializing-a-miniport-adapter.md)

[微型端口适配器关闭](miniport-adapter-shutdown.md)

[微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md)

[暂停适配器](pausing-an-adapter.md)

[启动适配器](starting-an-adapter.md)

 

 






