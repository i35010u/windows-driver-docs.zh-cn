---
title: 筛选器模块状态和操作
description: 筛选器模块状态和操作
ms.assetid: b5798865-8332-477b-b155-79a3db6ff6fa
keywords:
- 筛选器驱动程序 WDK 网络状态
- NDIS 筛选器驱动程序 WDK，状态
- 指出 WDK NDIS 筛选器
- 已分离的状态 WDK 网络
- 附加状态 WDK 网络
- 暂停的状态 WDK 网络
- 重新启动状态 WDK 网络
- 运行状态 WDK ne
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d719bde7713315e02458bef8baa2608e54dc688d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363391"
---
# <a name="filter-module-states-and-operations"></a>筛选器模块状态和操作





对驱动程序管理的每个筛选器模块 （筛选器驱动程序的实例） 的筛选器驱动程序必须支持以下操作状态：

<a href="" id="detached"></a>分离  
*Detached*状态是筛选器模块的初始状态。 NDIS 此状态筛选器模块时，可以调用筛选器驱动程序[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数来将筛选器模块附加到驱动程序堆栈。

<a href="" id="attaching"></a>附加  
在中*附加*状态中时，筛选器驱动程序正在准备将筛选器模块附加到驱动程序堆栈。

<a href="" id="paused"></a>已暂停  
在中*已暂停*状态时，筛选器驱动程序不会执行发送或接收操作。

<a href="" id="restarting"></a>重新启动  
在中*正在重新启动*状态中时，筛选器驱动程序完成重启发送和接收操作的筛选器模块所需的任何操作。

<a href="" id="running"></a>运行  
在中*运行*状态中时，筛选器驱动程序执行正常发送和接收处理筛选器模块。

<a href="" id="pausing"></a>暂停  
在中*暂停*状态中时，筛选器驱动程序完成停止发送和接收操作的筛选器模块所需的任何操作。

下表中的标题是筛选器模块状态。 第一列中列出了主要的事件。 表中的条目的其余部分指定下一个状态筛选器模块进入后处于状态发生的事件。 为空白条目表示无效的事件状态组合。

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
<th align="left">事件/状态</th>
<th align="left">Detached</th>
<th align="left">附加</th>
<th align="left">已暂停</th>
<th align="left">重新启动</th>
<th align="left">正在运行</th>
<th align="left">暂停</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>筛选器附加</p></td>
<td align="left"><p>附加</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>附加已完成</p></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>筛选器分离</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Detached</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>筛选器重新启动</p></td>
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
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>筛选器暂停</p></td>
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
<td align="left"><p>已暂停</p></td>
</tr>
<tr class="even">
<td align="left"><p>附加失败</p></td>
<td align="left"></td>
<td align="left"><p>Detached</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>重新启动失败</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>发送和接收</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>暂停</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OID 请求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"><p>重新启动</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>暂停</p></td>
</tr>
</tbody>
</table>

 

主要筛选器驱动程序事件定义，如下所示：

<a href="" id="--------filter-attach--------"></a> 筛选器附加   
NDIS 称为驱动程序的[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数来将筛选器模块附加到驱动程序堆栈。 有关附加筛选器模块的详细信息，请参阅[附加筛选器模块](attaching-a-filter-module.md)。

<a href="" id="attach-is-complete"></a>附加已完成  
当筛选器模块处于*附加*状态和筛选器驱动程序完成的所有筛选器模块要求，筛选器模块的资源将进入初始化*已暂停*状态。

<a href="" id="--------filter-detach--------"></a> 筛选器分离   
NDIS 称为驱动程序的[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)函数可分离驱动程序堆栈提供的筛选器模块。 有关详细信息，请参阅[分离筛选器模块](detaching-a-filter-module.md)。

<a href="" id="--------filter-restart--------"></a> 筛选器重新启动   
NDIS 称为驱动程序的[ *FilterRestart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)函数以重新启动暂停的筛选器模块。 有关详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

<a href="" id="restart-is-complete"></a>重启已完成  
当筛选器模块处于*正在重新启动*状态和驱动程序已准备好执行发送和接收操作，筛选器模块进入*运行*状态。

<a href="" id="--------filter-pause--------"></a> 筛选器暂停   
NDIS 称为驱动程序的[ *FilterPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)暂停筛选器模块的函数。 有关详细信息，请参阅[暂停筛选器模块](pausing-a-filter-module.md)。

<a href="" id="pause-is-complete"></a>暂停已完成  
驱动程序已完成停止发送和接收操作所需的所有操作，完成暂停操作且筛选器模块是在后*已暂停*状态。

<a href="" id="attach-failed"></a>附加失败  
如果 NDIS 调用驾[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数，并在附加操作失败 （例如，由于所需的资源不可用），该筛选器模块返回到*分离*状态。

<a href="" id="restart-failed"></a>重新启动失败  
如果 NDIS 调用驾[ *FilterRestart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_restart)函数并在重新启动尝试失败，返回到筛选器模块*已暂停*状态。

<a href="" id="send-and-receive-operations"></a>发送和接收操作  
驱动程序可以处理发送和接收中的操作*运行*并*暂停*状态。 有关详细信息大约发送和接收操作，请参阅[筛选器模块发送和接收操作](filter-module-send-and-receive-operations.md)。

<a href="" id="oid-requests"></a>OID 请求  
驱动程序可以处理中的 OID 请求*运行*，*正在重新启动*，*已暂停*，以及*暂停*状态。 有关 OID 的请求的详细信息，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

 

 





