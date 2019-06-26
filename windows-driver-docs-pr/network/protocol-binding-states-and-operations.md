---
title: 协议绑定状态和操作
description: 协议绑定状态和操作
ms.assetid: 669b3de1-7f6b-4e63-8943-c8eaadfa80fc
keywords:
- 协议驱动程序 WDK 网络绑定的操作状态
- NDIS 协议驱动程序 WDK，绑定操作状态
- 绑定状态 WDK 网络
- 协议驱动程序 WDK 网络事件
- NDIS 协议驱动程序 WDK，事件
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a446101908e233f67e336d0ad4b235ff53791557
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385464"
---
# <a name="protocol-binding-states-and-operations"></a>协议绑定状态和操作





NDIS 协议驱动程序必须为每个驱动程序管理的绑定支持以下操作状态：

<a href="" id="unbound"></a>未绑定  
未绑定状态是绑定的初始状态。 在此状态下，协议驱动程序等待调用的 NDIS [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。

<a href="" id="opening"></a>打开  
处于打开状态，协议驱动程序绑定分配资源，并尝试打开该适配器。

<a href="" id="running"></a>运行  
处于运行状态，协议驱动程序执行发送和接收处理的绑定。

<a href="" id="closing"></a>关闭  
在关闭状态下，协议驱动程序关闭到适配器的绑定，然后释放绑定资源。

<a href="" id="pausing"></a>暂停  
在暂停状态下，协议驱动程序完成停止发送和接收操作的绑定所需的任何操作。

<a href="" id="paused"></a>已暂停  
在已暂停状态下，协议驱动程序不执行发送或接收操作的绑定。

<a href="" id="restarting"></a>重新启动  
在正在重新启动状态下，协议驱动程序完成重启发送和接收操作的绑定所需的任何操作。

下表中以标题表示绑定状态，第一列中列出了事件。 表中的条目的其余部分指定下一个状态绑定进入后处于状态发生的事件。 为空白条目表示无效的事件状态组合。

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
<th align="left">打开</th>
<th align="left">关闭</th>
<th align="left">已暂停</th>
<th align="left">重新启动</th>
<th align="left">正在运行</th>
<th align="left">暂停</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ProtocolBindAdapterEx</em></p></td>
<td align="left"><p>打开</p></td>
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
<td align="left"><p>绑定已完成</p></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
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
<td align="left"><p>关闭</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>取消绑定已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>未绑定</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>即插即用暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>暂停</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>暂停已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
</tr>
<tr class="even">
<td align="left"><p>即插即用重启</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>重新启动</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>重启已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
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
<td align="left"><p>关闭</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"><p>重新启动</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>暂停</p></td>
</tr>
</tbody>
</table>

 

**请注意**  上表中列出的事件是 NDIS 协议绑定的主要事件。 提供信息时，将向该表添加其他事件。

 

主绑定事件定义，如下所示：

<a href="" id="protocolbindadapterex"></a>*ProtocolBindAdapterEx*  
NDIS 调用驱动程序的后[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数，该绑定将进入打开状态。 有关详细信息，请参阅[绑定到适配器](binding-to-an-adapter.md)。

<a href="" id="bind-failed"></a>绑定失败  
如果协议驱动程序无法将绑定到适配器，绑定将返回到未绑定状态。

<a href="" id="bind-is-complete"></a>绑定已完成  
如果该驱动程序已成功打开该适配器，绑定将进入暂停状态。 该驱动程序完成绑定操作。

<a href="" id="protocolunbindadapterex"></a>*ProtocolUnbindAdapterEx*  
NDIS 调用驱动程序的后[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)处理程序，该绑定将进入*关闭*状态。 有关详细信息，请参阅[取消绑定从适配器](unbinding-from-an-adapter.md)。

<a href="" id="unbind-is-complete"></a>取消绑定已完成  
该驱动程序完成取消绑定操作后，该绑定将进入未绑定状态。

<a href="" id="pnp-pause"></a>即插即用暂停  
NDIS 发送协议驱动程序后网络 Plug and Play (PnP) 暂停事件通知，该绑定将进入暂停状态。 有关详细信息请参阅[暂停绑定](pausing-a-binding.md)。

<a href="" id="pause-is-complete"></a>暂停已完成  
该驱动程序所需的所有操作都完成后停止发送和接收操作、 暂停操作已完成和绑定是处于已暂停状态。

**请注意**  驱动程序必须等待所有其未完成发送请求，以完成暂停操作完成之前。

 

<a href="" id="pnp-restart"></a>即插即用重启  
NDIS 发送协议驱动程序的网络即插即用的重新启动事件通知后，该绑定将进入正在重新启动状态。 有关详细信息，请参阅[重新启动绑定](restarting-a-binding.md)。

<a href="" id="restart-is-complete"></a>重启已完成  
该驱动程序准备就绪后用于处理发送和接收操作，在重新启动操作已完成和绑定处于运行状态。

<a href="" id="restart-failed"></a>重新启动失败  
如果 NDIS 发送协议驱动程序的网络即插即用的重新启动事件通知，并且重新启动尝试失败，该绑定将返回到暂停状态。

<a href="" id="send-and-receive-operations"></a>发送和接收操作  
协议驱动程序必须处理发送和接收操作在运行和暂停状态。 有关详细信息大约发送和接收操作，请参阅[协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

<a href="" id="oid-requests"></a>OID 请求  
协议驱动程序可以启动 OID 请求以设置或查询基础驱动程序中的信息。 协议驱动程序可以启动 OID 之外未绑定和打开的所有状态请求。

## <a name="related-topics"></a>相关主题


[编写 NDIS 协议驱动程序](writing-ndis-protocol-drivers.md)

 

 






