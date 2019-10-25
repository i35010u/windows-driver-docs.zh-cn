---
title: 协议绑定状态和操作
description: 协议绑定状态和操作
ms.assetid: 669b3de1-7f6b-4e63-8943-c8eaadfa80fc
keywords:
- 协议驱动程序 WDK 网络，绑定操作状态
- NDIS 协议驱动程序 WDK，绑定操作状态
- 绑定状态 WDK 网络
- 协议驱动程序 WDK 网络，事件
- NDIS 协议驱动程序 WDK，事件
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b74e4e019b2aec5f2ae196e2d2b5c76b56b71cfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843475"
---
# <a name="protocol-binding-states-and-operations"></a>协议绑定状态和操作





对于驱动程序管理的每个绑定，NDIS 协议驱动程序必须支持以下操作状态：

<a href="" id="unbound"></a>未绑定  
未绑定状态是绑定的初始状态。 在此状态下，协议驱动程序将等待 NDIS 调用[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数。

<a href="" id="opening"></a>结  
在打开状态中，协议驱动程序为绑定分配资源并尝试打开适配器。

<a href="" id="running"></a>耗尽  
在 "正在运行" 状态下，协议驱动程序为绑定执行发送和接收处理。

<a href="" id="closing"></a>结束语  
在关闭状态下，协议驱动程序将关闭到适配器的绑定，然后释放绑定的资源。

<a href="" id="pausing"></a>暂停  
在暂停状态下，协议驱动程序完成为绑定停止发送和接收操作所需的任何操作。

<a href="" id="paused"></a>悬停  
在暂停状态下，协议驱动程序不会对绑定执行发送或接收操作。

<a href="" id="restarting"></a>重新  
在重新启动状态下，协议驱动程序将完成为绑定重新启动发送和接收操作所需的任何操作。

在下表中，标题表示绑定状态，事件列在第一列中。 表中的其余条目指定事件发生在状态中后的下一个状态。 空白条目表示无效的事件/状态组合。

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
<th align="left">未绑定</th>
<th align="left">结</th>
<th align="left">结束语</th>
<th align="left">暂停</th>
<th align="left">重新</th>
<th align="left">Running</th>
<th align="left">暂停</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ProtocolBindAdapterEx</em></p></td>
<td align="left"><p>结</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>绑定失败</p></td>
<td align="left"></td>
<td align="left"><p>未绑定</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>绑定完成</p></td>
<td align="left"></td>
<td align="left"><p>暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ProtocolUnbindAdapterEx</em></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>结束语</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>取消绑定完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>未绑定</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>PnP 暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>暂停</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>暂停完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>暂停</p></td>
</tr>
<tr class="even">
<td align="left"><p>PnP 重启</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>重新</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>重新启动已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Running</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>重新启动失败</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>暂停</p></td>
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
<td align="left"><p>Running</p></td>
<td align="left"><p>暂停</p></td>
</tr>
<tr class="even">
<td align="left"><p>OID 请求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>结束语</p></td>
<td align="left"><p>暂停</p></td>
<td align="left"><p>重新</p></td>
<td align="left"><p>Running</p></td>
<td align="left"><p>暂停</p></td>
</tr>
</tbody>
</table>

 

**请注意**，  上表中列出的事件是 NDIS 协议绑定的主要事件。 当信息可用时，附加事件将添加到此表中。

 

主绑定事件定义如下：

<a href="" id="protocolbindadapterex"></a>*ProtocolBindAdapterEx*  
在 NDIS 调用驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数后，绑定将进入打开状态。 有关详细信息，请参阅[绑定到适配器](binding-to-an-adapter.md)。

<a href="" id="bind-failed"></a>绑定失败  
如果协议驱动程序未能绑定到适配器，则绑定将返回到未绑定状态。

<a href="" id="bind-is-complete"></a>绑定完成  
如果驱动程序成功打开了适配器，则绑定进入暂停状态。 驱动程序完成绑定操作。

<a href="" id="protocolunbindadapterex"></a>*ProtocolUnbindAdapterEx*  
在 NDIS 调用驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)处理程序后，绑定将进入*关闭*状态。 有关详细信息，请参阅[从适配器解除绑定](unbinding-from-an-adapter.md)。

<a href="" id="unbind-is-complete"></a>取消绑定完成  
驱动程序完成解除绑定操作后，绑定将进入未绑定状态。

<a href="" id="pnp-pause"></a>PnP 暂停  
在 NDIS 向协议驱动程序发送网络即插即用（PnP）暂停事件通知后，该绑定将进入暂停状态。 有关详细信息，请参阅[暂停绑定](pausing-a-binding.md)。

<a href="" id="pause-is-complete"></a>暂停完成  
当驱动程序完成停止发送和接收操作所需的所有操作后，暂停操作完成并且绑定处于暂停状态。

**请注意**  驱动程序必须等待所有未完成的发送请求完成，然后才能完成暂停操作。

 

<a href="" id="pnp-restart"></a>PnP 重启  
在 NDIS 向协议驱动程序发送网络 PnP restart 事件通知后，该绑定将进入重新启动状态。 有关详细信息，请参阅[重新启动绑定](restarting-a-binding.md)。

<a href="" id="restart-is-complete"></a>重新启动已完成  
驱动程序准备好处理发送和接收操作后，重启操作将完成，并且绑定处于 "正在运行" 状态。

<a href="" id="restart-failed"></a>重新启动失败  
如果 NDIS 向协议驱动程序发送了一个网络 PnP restart 事件通知，并且重新启动尝试失败，则绑定将恢复到暂停状态。

<a href="" id="send-and-receive-operations"></a>发送和接收操作  
协议驱动程序必须在正在运行和正在暂停的状态处理发送和接收操作。 有关发送和接收操作的详细信息，请参阅[协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

<a href="" id="oid-requests"></a>OID 请求  
协议驱动程序可以启动 OID 请求来设置或查询基础驱动程序中的信息。 协议驱动程序可以从所有状态启动 OID 请求，但未绑定和打开除外。

## <a name="related-topics"></a>相关主题


[编写 NDIS 协议驱动程序](writing-ndis-protocol-drivers.md)

 

 






