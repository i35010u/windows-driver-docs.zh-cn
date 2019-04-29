---
title: Bug 检查 0x7C BUGCODE_NDIS_DRIVER
description: BUGCODE_NDIS_DRIVER bug 检查具有 0x0000007C 值。 此 bug 检查表示操作系统检测到的网络驱动程序错误。
ms.assetid: 0f2c2e9c-2889-4d99-b653-0ee1d4c2be0e
keywords:
- Bug 检查 0x7C BUGCODE_NDIS_DRIVER
- BUGCODE_NDIS_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_NDIS_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bc18ba456481541387fad7d89252866eae24cd5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367372"
---
# <a name="bug-check-0x7c-bugcodendisdriver"></a>Bug 检查 0x7C：BUGCODE\_NDIS\_驱动程序


BUGCODE\_NDIS\_驱动程序 bug 检查的值为 0x0000007C。 此 bug 检查表示操作系统检测到的网络驱动程序错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="bugcodendisdriver-parameters"></a>BUGCODE\_NDIS\_驱动程序参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。 如果参数的值为"0"，这意味着不使用它。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />

</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 1 值和错误的原因</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>NDIS_BUGCHECK_ALLOCATE_SHARED_MEM_HIGH_IRQL</p>
<p>驱动程序调用<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562782" data-raw-source="[NdisMAllocateSharedMemory](https://msdn.microsoft.com/library/windows/hardware/ff562782)">NdisMAllocateSharedMemory</a></strong>在引发 irql 下完成。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>请求的共享内存的长度</p></td>
<td align="left"><p>当前 IRQL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>NDIS_BUGCHECK_SHARED_MEM_CORRUPTION</p>
<p>在调用期间 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562782" data-raw-source="[NdisMAllocateSharedMemory](https://msdn.microsoft.com/library/windows/hardware/ff562782)">NdisMAllocateSharedMemory</a></strong>，NDIS 检测到以前分配共享的内存页已损坏。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>共享的内存页已损坏</p></td>
<td align="left"><p>跟踪驱动程序的共享的内存分配 NDIS_WRAPPER_CONTEXTE 的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>NDIS_BUGCHECK_FREE_INVALID_SHARED_MEM</p>
<p>微型端口驱动程序调用<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff563589" data-raw-source="[NdisMFreeSharedMemory](https://msdn.microsoft.com/library/windows/hardware/ff563589)">NdisMFreeSharedMemory</a></strong> (<strong>异步</strong>) 使用的共享的内存地址的已释放。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>从其分配此共享的内存的页</p></td>
<td align="left"><p>共享内存的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNLOAD_DRIVER_INVALID_PARAMETER</p>
<p><strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[AddDevice](https://msdn.microsoft.com/library/windows/hardware/ff540521)">AddDevice</a></strong> 调用所使用的驱动程序，不在向注册的 NDIS 驱动程序的列表。</p>
<p>启用仅在特殊检测 NDIS 上。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK 的地址</p></td>
<td align="left"><p>DRIVER_OBJECT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_STACK_LOCATION</p>
<p>以太网驱动程序指示它收到使用当前正在使用的协议堆栈的数据包描述符的数据包。</p>
<p>捕获了检查堆栈数据包位置。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 运行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd.pkt</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>包含此数据包描述符数据包数组的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_REF_COUNT</p>
<p>以太网驱动程序指示它收到使用当前正在使用的协议堆栈的数据包描述符的数据包。</p>
<p>捕获了检查数据包引用计数。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 运行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd.pkt</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>包含此数据包描述符数据包数组的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>FDDI 驱动程序指示它使用当前正在使用的协议堆栈的数据包描述符收到的数据包。</p>
<p>捕获了检查引用计数。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 运行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd.pkt</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>包含此数据包描述符数据包数组的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>微型端口驱动程序未取消它的中断注册在终止过程。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_CANCEL_TIMER</p>
<p>微型端口驱动程序不成功取消所有计时器情况下停止。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>微型端口驱动程序的计时器队列 (NDIS_MINIPORT_TIMER) 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>NDIS_BUGCHECK_DRIVER_UNLOAD_UNEXPECTED</p>
<p>微型端口驱动程序是获取过早卸载。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK 的地址</p></td>
<td align="left"><p>DRIVER_OBJECT 的地址</p></td>
<td align="left"><p>微型端口驱动程序的引用计数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>微型端口驱动程序将其初始化失败而无需取消注册它的中断。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_CANCEL_TIMER</p>
<p>微型端口驱动程序失败且不会成功取消所有计时器其初始化。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>微型端口驱动程序的计时器队列 (NDIS_MINIPORT_TIMER) 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>微型端口驱动程序未取消它的中断注册在终止过程。</p>
<p>停止从初始化例程微型端口驱动程序从其初始化处理程序返回成功消息后调用。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_CANCEL_TIMER</p>
<p>微型端口驱动程序不成功取消所有计时器情况下停止。</p>
<p>停止从初始化例程微型端口驱动程序从其初始化处理程序返回成功消息后调用。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>微型端口驱动程序的计时器队列 (NDIS_MINIPORT_TIMER) 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>NDIS_BUGCHECK_RESET_COMPLETE_UNEXPECTED</p>
<p>微型端口驱动程序调用<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff563663" data-raw-source="[NdisMResetComplete](https://msdn.microsoft.com/library/windows/hardware/ff563663)">NdisMResetComplete</a></strong>没有任何挂起的重置请求。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>重置状态</p></td>
<td align="left"><p>AddressingReset (BOOLEAN)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_INT_DEREGISTER</p>
<p>从低功耗状态恢复后的微型端口驱动程序失败且不会取消它的中断其初始化。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_CANCEL_TIMER</p>
<p>从低功耗状态恢复后的微型端口驱动程序失败且不会成功取消所有计时器其初始化。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>微型端口驱动程序的计时器队列 (NDIS_MINIPORT_TIMER) 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>NDIS_BUGCHECK_NFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>微型端口驱动程序指示它收到使用当前正在使用的协议堆栈的数据包描述符的数据包。</p>
<p>捕获了检查数据包引用计数。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 运行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd.pkt</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>包含此数据包描述符数据包数组的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>NDIS_BUGCHECK_TFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>令牌环微型端口驱动程序指示它收到使用当前正在使用的协议堆栈的数据包描述符的数据包。</p>
<p>捕获了检查数据包引用计数。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 运行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd.pkt</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>包含此数据包描述符数据包数组的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>NDIS_BUGCHECK_WAIT_EVENT_HIGH_IRQL</p>
<p>名为的 NDIS 驱动程序<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff564651" data-raw-source="[NdisWaitEvent](https://msdn.microsoft.com/library/windows/hardware/ff564651)">NdisWaitEvent</a></strong>非法的 IRQL 在</p></td>
<td align="left"><p>实际 IRQL</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_NDIS5_CALL</p>
<p>微型端口驱动程序的较旧的驱动程序调用 API 保留。 该驱动程序应只调用 NDIS 6.x Api。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OPEN_IN_BIND_CONTEXT</p>
<p>协议驱动程序在绑定期间未正确打开适配器。</p></td>
<td align="left"><p>特定协议的地址。 运行<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">！ ndiskd.protocol</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>分配的协议驱动程序的上下文区域的地址。</p>
<p>强制转换为 ndis ！NDIS_BIND_CONTEXT。</p></td>
<td align="left"><p>打开的句柄的地址。 运行<strong><a href="-ndiskd-mopen.md" data-raw-source="[!ndiskd.mopen](-ndiskd-mopen.md)">！ ndiskd.mopen</a></strong>与此地址用于的详细信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>NDIS_BUGCHECK_IFPROVIDER_DEREGISTER_UNEXPECTED</p>
<p>接口提供程序调用<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562703" data-raw-source="[NdisIfDeregisterProvider](https://msdn.microsoft.com/library/windows/hardware/ff562703)">NdisIfDeregisterProvider</a></strong>而不必首先删除其所有接口。</p></td>
<td align="left"><p>接口提供程序句柄的地址。 运行<strong><a href="-ndiskd-ifprovider.md" data-raw-source="[!ndiskd.ifprovider](-ndiskd-ifprovider.md)">！ ndiskd.ifprovider</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>NDIS_BUGCHECK_IF_STACK_TABLE_LOOP</p>
<p>驱动程序试图将接口添加到 ifStackTable，但这样做会导致一个循环。 IfStackTable 不能周期。 运行<strong><a href="-ndiskd-ifstacktable.md" data-raw-source="[!ndiskd.ifstacktable](-ndiskd-ifstacktable.md)">！ ndiskd.ifstacktable</a></strong>若要查看当前的表 (在此调用之前 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562693" data-raw-source="[NdisIfAddIfStackEntry](https://msdn.microsoft.com/library/windows/hardware/ff562693)">NdisIfAddIfStackEntry</a></strong>)。</p></td>
<td align="left"><p>添加到表 HigherLayerIfIndex</p></td>
<td align="left"><p>添加到表 LowerLayerIfIndex</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FAILED_OID_WHICH_MUST_SUCCEED</p>
<p>微型端口驱动程序失败，必须成功的 OID 请求。 执行此操作将会泄漏内存或其他资源。</p></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>已失败的 OID。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd.help</a></strong>若要查找此 OID 的名称。</p></td>
<td align="left"><p>失败状态代码 (NDIS_STATUS_XXX) 与其 OID 请求已完成</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>NDIS_BUGCHECK_OID_REQUEST_INVALID_BUFFER</p>
<p>微型端口驱动程序或筛选器驱动程序已非法完成 OID 请求。 检查 BytesWritten 不大于缓冲区的整个长度。</p></td>
<td align="left"><p>特定的微型端口适配器或筛选器模块块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>或<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd.filter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>指向的地址<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)">NDIS_OID_REQUEST</a></strong>非法已完成。 检查其与 <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">！ ndiskd.oid</a></strong>。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>NDIS_BUGCHECK_REFCOUNT_IMBALANCE</p>
<p>NDIS 内部引用计数中检测到错误。 这可能导致通过 （更多取消引用比引用） 的引用计数下溢，或标记不匹配。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>内部句柄。 使用<strong><a href="-ndiskd-ndisref.md" data-raw-source="[!ndiskd.ndisref](-ndiskd-ndisref.md)">！ ndiskd.ndisref</a></strong>或强制转换到 ndis ！NDIS_REFCOUNT_BLOCK。</p></td>
<td align="left"><p>当前 reftag 值</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION</p>
<p>微型端口驱动程序完成非法状态转换。</p></td>
<td align="left"><p>失败。 可能值：</p>
<ol>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_PAUSE_COMPLETE</p>
<p>微型端口称为<strong>NdisMPauseComplete</strong>但没有任何挂起的暂停操作。</p></li>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_RESTART_COMPLETE</p>
<p>微型端口称为<strong>NdisMRestartComplete</strong>但没有任何挂起的重新启动操作。</p></li>
</ol></td>
<td align="left"><p>特定的微型端口适配器块的地址。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>NDIS_BUGCHECK_STATUS_INDICATION_INVALID_BUFFER</p>
<p>微型端口驱动程序或筛选器驱动程序指示非法 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff567373" data-raw-source="[NDIS_STATUS_INDICATION](https://msdn.microsoft.com/library/windows/hardware/ff567373)">NDIS_STATUS_INDICATION</a></strong>。</p></td>
<td align="left"><p>状态指示的类型。 运行<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd.help</a></strong> ，此代码的详细信息。</p></td>
<td align="left"><p>指示此非法状态指示的驱动程序实例的句柄。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>或<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd.filter</a></strong>与此有关的详细信息的句柄。</p></td>
<td align="left"><p>状态指示负载的地址。 其解释取决于状态指示的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OBJECT_HEADER</p>
<p>驱动程序创建一个无效 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff566588" data-raw-source="[NDIS_OBJECT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff566588)">NDIS_OBJECT_HEADER</a></strong>。</p></td>
<td align="left"><p>所指示的非法状态指示驱动程序的句柄。 运行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd.minidriver</a></strong>或<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">！ ndiskd.filterdriver</a></strong>与此有关的详细信息的句柄。</p></td>
<td align="left"><p>具有格式不正确的标头的对象。 其解释取决于要调用的 API。 例如，如果该驱动程序调用<strong>NdisAllocateCloneOidRequest</strong>，然后将对象转换为 ndis ！NDIS_OID_REQUEST。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_NET_PNP_EVENT</p>
<p>微型端口驱动程序或筛选器驱动程序指示非法 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff568752" data-raw-source="[NET_PNP_EVENT_NOTIFICATION](https://msdn.microsoft.com/library/windows/hardware/ff568752)">NET_PNP_EVENT_NOTIFICATION</a></strong>。</p></td>
<td align="left"><p>所指示的非法状态指示驱动程序的句柄。 运行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd.minidriver</a></strong>或<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">！ ndiskd.filterdriver</a></strong>与此有关的详细信息的句柄。</p></td>
<td align="left"><p>强制转换为 NET_PNP_EVENT_NOTIFICATION</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>NDIS_BUGCHECK_PD_ERROR</p>
<p>Packet Direct 数据路径中检测到错误。</p></td>
<td align="left"><p>检测的错误子类型。 可能值：</p>
<ol>
<li><p>NDIS_BUGCHECK_PD_ERROR_EC_THREAD_MISMATCH</p>
<p>错误的线程上调用 API 时。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_BY_CLIENT</p>
<p>PD 客户端尝试 arm 处于非法状态提供程序。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION</p>
<p>PD 提供程序非法触发漏通知，虽然它不有。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION_VIA_ISR</p>
<p>PD 提供程序非法触发 ISR 漏通知，虽然它不有。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_THUNK_BY_LWF</p>
<p>筛选器驱动程序试图干扰 Packet Direct 数据路径。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_BM_GROUP_REQUEST</p>
<p>非法尝试从缓冲区管理器组中删除自身 PD 提供程序。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_PD_BUFFER_SETUP</p>
<p>PD 缓冲区设置请求的格式不正确。</p></li>
</ol></td>
<td align="left"><p>参数 3 的值取决于参数 2 的值。 此列表中的每个数字对应于参数 2 中的相同编号。</p>
<ol>
<li>强制转换为 NDIS_PD_EC</li>
<li>强制转换为 NDIS_PD_QUEUE_TRACKER</li>
<li>强制转换为 NDIS_PD_QUEUE_TRACKER</li>
<li>强制转换为 NDIS_PD_QUEUE_TRACKER</li>
<li>特定筛选器模块的句柄。 运行<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd.filter</a></strong>与此有关的详细信息的句柄。</li>
<li>缓冲区管理器组，如果已知</li>
<li>源 PD_MEMORY_HANDLE 或 PD_BUFFER</li>
</ol></td>
<td align="left"><p>参数 4 的值取决于参数 2 的值。 此列表中的每个数字对应于参数 2 中的相同编号。</p>
<ol>
<li>应有 ETHREAD</li>
<li>句柄 PD 客户端</li>
<li>句柄 PD 提供程序。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此有关的详细信息的句柄。</li>
<li>句柄 PD 提供程序。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此有关的详细信息的句柄。</li>
<li>句柄 PD 提供程序。 运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此有关的详细信息的句柄。</li>
<li><p>如果参数 3 为 0，这是提供程序句柄。</p>
<p>如果参数 3 为非零，PD 客户端，不释放所有分配，这是 PD 客户端句柄。</p></li>
<li>目标 PD_BUFFER</li>
</ol></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNEXPECTED_FAILURE</p>
<p>内部操作意外失败。 这是可能需要 NDIS 中的 bug。SYS 本身。</p></td>
<td align="left"><p>失败的操作。 可能值：</p>
<p>0x01:NDIS_BUGCHECK_UNEXPECTED_FAILURE_KEWAITFORSINGLEOBJECT</p>
<p>Kewaitforsingleobject 的调用失败。</p></td>
<td align="left"><p>失败状态代码</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>NDIS_BUGCHECK_WATCHDOG</p>
<p>尝试管理网络堆栈花费的时间太长。 当 NDIS 连接到其他驱动程序时，NDIS 启动监视程序计时器以确保在调用立即完成。 如果调用时间太长，NDIS 注入错误检查。</p>
<p>原因可能是简单的死锁。 查找具有"！ 堆栈 2 ndis"或类似于任何线程查看可疑。 应特别注意从 NDIS_WATCHDOG_TRIAGE_BLOCK PrimaryThread。</p>
<p>这可能引起丢失功能的 Nbl，在这种情况下<strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">！ ndiskd.pendingnbls</a></strong>可能帮助。 检查使用停滞的 Oid  <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">！ ndiskd.oid</a></strong>。</p></td>
<td align="left"><p>该操作的时间太长。 可能值：</p>
<ul>
<li><p>0x01:NDIS_BUGCHECK_WATCHDOG_PROTOCOL_PAUSE</p>
<p>暂停协议驱动程序时出现超时。</p></li>
<li><p>0x02:NDIS_BUGCHECK_WATCHDOG_PROTOCOL_NETPNPEVENT</p>
<p>同时提供了 NET_PNP_EVENT_NOTIFICATION 对协议驱动程序时出现超时。</p></li>
<li><p>0x03:NDIS_BUGCHECK_WATCHDOG_PROTOCOL_STATUS_INDICATION</p>
<p>同时提供了对协议驱动程序的状态指示出现超时。</p></li>
<li><p>0x04:NDIS_BUGCHECK_WATCHDOG_PROTOCOL_UNBIND</p>
<p>取消绑定协议驱动程序时出现超时。</p></li>
<li><p>0x11:NDIS_BUGCHECK_WATCHDOG_FILTER_PAUSE</p>
<p>暂停筛选器驱动程序时出现超时。</p></li>
<li><p>0x12:NDIS_BUGCHECK_WATCHDOG_FILTER_NETPNPEVENT</p>
<p>同时提供了 NET_PNP_EVENT_NOTIFICATION 对筛选器驱动程序时出现超时。</p></li>
<li><p>0x13:NDIS_BUGCHECK_WATCHDOG_FILTER_STATUS_INDICATION</p>
<p>同时提供了对筛选器驱动程序的状态指示出现超时。</p></li>
<li><p>0x14:NDIS_BUGCHECK_WATCHDOG_FILTER_DETACH</p>
<p>分离筛选器驱动程序时出现超时。</p></li>
<li><p>0x21:NDIS_BUGCHECK_WATCHDOG_MINIPORT_PAUSE</p>
<p>暂停的微型端口适配器时超时。</p></li>
<li><p>0x22:NDIS_BUGCHECK_WATCHDOG_MINIPORT_HALT</p>
<p>正在停止微型端口适配器时超时。</p></li>
<li><p>0x23:NDIS_BUGCHECK_WATCHDOG_MINIPORT_OID</p>
<p>同时提供给微型端口适配器 OID 请求时出现超时。</p></li>
<li><p>0x24:NDIS_BUGCHECK_WATCHDOG_FILTER_OID</p>
<p>同时提供了对筛选器驱动程序的 OID 请求时出现超时。</p></li>
<li><p>15000x25:NDIS_BUGCHECK_WATCHDOG_MINIPORT_IDLE</p>
<p>空闲的微型端口适配器时超时。</p></li>
<li><p>0x26:NDIS_BUGCHECK_WATCHDOG_CANCEL_IDLE</p>
<p>正在取消微型端口适配器上的空闲请求时超时。</p></li>
</ul></td>
<td align="left"><p>强制转换为 ndis ！NDIS_WATCHDOG_TRIAGE_BLOCK。 一些有用的字段：</p>
<ul>
<li><strong>StartTime</strong>显示什么时间开始操作，在 100ns 个单位由 KeQueryInterruptTime 返回。</li>
<li><strong>TimeoutMilliseconds</strong>显示了多长时间 NDIS 等待时，至少之前触发此错误检查。</li>
<li><strong>TargetObject</strong>是协议、 筛选器模块或微型端口适配器的 NDIS 正在等待的句柄。 运行 <strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">！ ndiskd.protocol</a></strong>，  <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd.filter</a></strong>，或 <strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd.netadapter</a></strong>与此有关的详细信息的句柄。</li>
<li><strong>PrimaryThread</strong>是在其中 NDIS 启动该操作的线程。 通常情况下，这是首先要查看，尽管该线程可能出现了其他位置如果要以异步方式处理该操作。</li>
</ul></td>
<td align="left"><p>参数 4 的值取决于参数 2 的值。 此列表中的每个数字对应于参数 2 中的十六进制值相同。</p>
<ul>
<li>0x01:0</li>
<li>0x02:卡滞事件 NET_PNP_EVENT_CODE。 有关这些代码的详细信息，请参阅 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff568751" data-raw-source="[NET_PNP_EVENT](https://msdn.microsoft.com/library/windows/hardware/ff568751)">NET_PNP_EVENT</a></strong>...</li>
<li>0x03:卡滞指示 NDIS_STATUS 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd.help</a></strong>若要对其进行解码。</li>
<li>0x04:0</li>
<li>0x11:0</li>
<li>0x12:卡滞事件 NET_PNP_EVENT_CODE。 有关可能的值，请参阅前面的项 2 此列表中值的列表。</li>
<li>0x13:卡滞指示 NDIS_STATUS 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd.help</a></strong>若要对其进行解码。</li>
<li>0x14:0</li>
<li>0x21:0</li>
<li>0x22:0</li>
<li>0x23:卡滞请求的 OID 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd.help</a></strong>若要对其进行解码。</li>
<li>0x24:卡滞请求的 OID 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd.help</a></strong>若要对其进行解码。</li>
<li>15000x25:0</li>
<li>0x26:0</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OID_COMPLETION</p>
<p>微型端口驱动程序已尝试完成当前未挂起的 OID 请求该微型端口驱动程序。 原因可能是尝试完成不止一次的同一请求的驱动程序。</p></td>
<td align="left"><p>微型端口驱动程序句柄，导致检测的错误。 运行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd.minidriver</a></strong>与此有关的详细信息的句柄。</p></td>
<td align="left"><p>NDIS OID 请求微型端口驱动程序已尝试完成。 你可以尝试运行<strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">！ ndiskd.oid</a></strong>与此请求，但内存可能不是有效此时。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>NDIS_BUGCHECK_LEAKED_NBL</p>
<p>驱动程序已泄露<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff568388" data-raw-source="[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)">NET_BUFFER_LIST</a></strong>结构。 请咨询<strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">！ ndiskd.pendingnbls</a></strong>若要查看任何功能的 Nbl 仍然挂起该是 on 此驱动程序。</p></td>
<td align="left"><p>在其中检测到泄漏。 可能值：</p>
<ul>
<li><p>0x01:泄漏检测到的 NBL 跟踪器。 当前正在取消注册或取消绑定的驱动程序是最可能的原因。 看一下 bugchecking 线程的调用堆栈。 不能取消绑定或取消注册时它们仍然适用活动功能的 Nbl 驱动程序。</p></li>
</ul></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

参数 1 指示 BUGCODE 的特定原因\_NDIS\_驱动程序 bug 检查。

<a name="remarks"></a>备注
-------

BUGCODE\_NDIS\_网络驱动程序中的驱动程序检测错误 indendifies 问题。 通常情况下，问题是由 NDIS 微型端口驱动程序引起的。 可以通过获取 NDIS 微型端口驱动程序的完整列表[ **！ ndiskd.netadapter**](-ndiskd-netadapter.md)。 可以获取与网络堆栈的更大图片概述[ **！ ndiskd.netreport**](-ndiskd-netreport.md)。

仅在 Microsoft Windows Server 2003 和更高版本的 Windows 上会出现此 bug 检查代码。 在 Windows 2000 和 Windows XP 中，相应的代码是[ **bug 检查 0xD2** ](bug-check-0xd2--bugcode-id-driver.md) (BUGCODE\_ID\_驱动程序)。

 

 




