---
title: Bug 检查 0x7C BUGCODE_NDIS_DRIVER
description: BUGCODE_NDIS_DRIVER bug 检查的值为0x0000007C。 此错误检查表明操作系统检测到网络驱动程序中的错误。
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
ms.openlocfilehash: 7cde5e7411d8f1016b0d7b3870c8864d4fa5e9ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840847"
---
# <a name="bug-check-0x7c-bugcode_ndis_driver"></a>Bug 检查0x7C： BUGCODE \_ NDIS \_ 驱动程序


BUGCODE \_ NDIS \_ 驱动程序 bug 检查的值为0x0000007C。 此错误检查表明操作系统检测到网络驱动程序中的错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="bugcode_ndis_driver-parameters"></a>BUGCODE \_ NDIS \_ 驱动程序参数


参数1指示违规类型。 其他参数的意义取决于参数1的值。 如果参数的值为 "0"，则表示未使用该参数。

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
<th align="left">参数1值和错误原因</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>NDIS_BUGCHECK_ALLOCATE_SHARED_MEM_HIGH_IRQL</p>
<p>在出现 IRQL 时调用 <strong><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory" data-raw-source="[NdisMAllocateSharedMemory](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)">NdisMAllocateSharedMemory</a></strong> 的驱动程序。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>请求的共享内存的长度</p></td>
<td align="left"><p>当前 IRQL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>NDIS_BUGCHECK_SHARED_MEM_CORRUPTION</p>
<p>在调用 <strong><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory" data-raw-source="[NdisMAllocateSharedMemory](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)">NdisMAllocateSharedMemory</a></strong>期间，NDIS 检测到以前分配的共享内存页面已损坏。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>已损坏的共享内存页</p></td>
<td align="left"><p>跟踪驱动程序的共享内存分配的 NDIS_WRAPPER_CONTEXTE 地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>NDIS_BUGCHECK_FREE_INVALID_SHARED_MEM</p>
<p>一个名为 <strong><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory" data-raw-source="[NdisMFreeSharedMemory](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)">NdisMFreeSharedMemory</a></strong> (<strong>Async</strong>) 的微型端口驱动程序，其共享内存地址已被释放。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>从中分配此共享内存的页</p></td>
<td align="left"><p>共享内存的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNLOAD_DRIVER_INVALID_PARAMETER</p>
<p>使用不在使用 NDIS 注册的驱动程序列表的驱动程序调用<strong><a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[AddDevice](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)">AddDevice</a></strong> 。</p>
<p>仅在特殊检测的 NDIS 上启用。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK 的地址</p></td>
<td align="left"><p>DRIVER_OBJECT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_STACK_LOCATION</p>
<p>以太网驱动程序指示它使用当前正在由协议堆栈使用的数据包描述符接收到数据包。</p>
<p>通过检查堆栈数据包位置捕获。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>包含此数据包描述符的数据包数组的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_REF_COUNT</p>
<p>以太网驱动程序指示它使用当前正在由协议堆栈使用的数据包描述符接收到数据包。</p>
<p>通过检查数据包引用计数来捕获。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>包含此数据包描述符的数据包数组的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>FDDI 驱动程序指示它通过使用当前正在由协议堆栈使用的数据包描述符接收到了数据包。</p>
<p>通过检查引用计数来捕获。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>包含此数据包描述符的数据包数组的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>小型端口驱动程序未在暂停过程中取消注册其中断。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_CANCEL_TIMER</p>
<p>微型端口驱动程序已停止，但未成功取消其所有计时器。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>微型端口驱动程序的计时器队列的地址 (NDIS_MINIPORT_TIMER) </p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>NDIS_BUGCHECK_DRIVER_UNLOAD_UNEXPECTED</p>
<p>已提前卸载微型端口驱动程序。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK 的地址</p></td>
<td align="left"><p>DRIVER_OBJECT 的地址</p></td>
<td align="left"><p>微型端口驱动程序的引用计数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>小型小型驱动程序初始化失败，无需注销其中断。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_CANCEL_TIMER</p>
<p>小型小型驱动程序初始化失败，未成功取消其所有计时器。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>微型端口驱动程序的计时器队列的地址 (NDIS_MINIPORT_TIMER) </p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>小型端口驱动程序未在暂停过程中取消注册其中断。</p>
<p>当微型端口驱动程序从其初始化处理程序返回 success 后，从初始化例程调用了该停止。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_CANCEL_TIMER</p>
<p>微型端口驱动程序已停止，但未成功取消其所有计时器。</p>
<p>当微型端口驱动程序从其初始化处理程序返回 success 后，从初始化例程调用了该停止。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>微型端口驱动程序的计时器队列的地址 (NDIS_MINIPORT_TIMER) </p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>NDIS_BUGCHECK_RESET_COMPLETE_UNEXPECTED</p>
<p>名为 <strong><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete" data-raw-source="[NdisMResetComplete](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)">NdisMResetComplete</a></strong> 的小型小型驱动程序，没有任何挂起的重置请求。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>重置状态</p></td>
<td align="left"><p>AddressingReset (布尔) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_INT_DEREGISTER</p>
<p>从低功耗状态恢复后，微型端口驱动程序无法在不注销其中断的情况下初始化。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT 的地址</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_CANCEL_TIMER</p>
<p>从低功耗状态恢复后，微型端口驱动程序无法初始化，而不会成功取消其所有计时器。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>微型端口驱动程序的计时器队列的地址 (NDIS_MINIPORT_TIMER) </p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>NDIS_BUGCHECK_NFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>微型端口驱动程序指示它使用当前正在由协议堆栈使用的数据包描述符接收到数据包。</p>
<p>通过检查数据包引用计数来捕获。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>包含此数据包描述符的数据包数组的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>NDIS_BUGCHECK_TFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>Token-Ring 微型端口驱动程序指示它使用当前正在由协议堆栈使用的数据包描述符接收到数据包。</p>
<p>通过检查数据包引用计数来捕获。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>驱动程序使用的数据包描述符的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>包含此数据包描述符的数据包数组的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>NDIS_BUGCHECK_WAIT_EVENT_HIGH_IRQL</p>
<p>名为 <strong><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent" data-raw-source="[NdisWaitEvent](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent)">NdisWaitEvent</a></strong> 的 NDIS 驱动程序在非法 IRQL</p></td>
<td align="left"><p>实际的 IRQL</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_NDIS5_CALL</p>
<p>一个小型小型驱动程序，称为用于旧驱动程序的 API。 驱动程序应只调用 NDIS 1.x Api。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OPEN_IN_BIND_CONTEXT</p>
<p>协议驱动程序在绑定过程中未正确地打开适配器。</p></td>
<td align="left"><p>特定协议的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>协议驱动程序分配的上下文区域的地址。</p>
<p>强制转换为 ndis！NDIS_BIND_CONTEXT。</p></td>
<td align="left"><p>打开句柄的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-mopen.md" data-raw-source="[!ndiskd.mopen](-ndiskd-mopen.md)">！ ndiskd。</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>NDIS_BUGCHECK_IFPROVIDER_DEREGISTER_UNEXPECTED</p>
<p>一个名为 <strong><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider" data-raw-source="[NdisIfDeregisterProvider](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider)">NdisIfDeregisterProvider</a></strong> 的接口提供程序，无需先删除其所有接口。</p></td>
<td align="left"><p>接口提供程序句柄的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-ifprovider.md" data-raw-source="[!ndiskd.ifprovider](-ndiskd-ifprovider.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>NDIS_BUGCHECK_IF_STACK_TABLE_LOOP</p>
<p>驱动程序尝试将接口添加到 ifStackTable，但这样做会导致循环。 IfStackTable 不能具有周期。 在调用<strong><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifaddifstackentry" data-raw-source="[NdisIfAddIfStackEntry](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifaddifstackentry)">NdisIfAddIfStackEntry</a></strong>) 之前，请运行<strong><a href="-ndiskd-ifstacktable.md" data-raw-source="[!ndiskd.ifstacktable](-ndiskd-ifstacktable.md)">ndiskd</a></strong> ，以查看当前表 (。</p></td>
<td align="left"><p>要添加到表中的 HigherLayerIfIndex</p></td>
<td align="left"><p>要添加到表中的 LowerLayerIfIndex</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FAILED_OID_WHICH_MUST_SUCCEED</p>
<p>微型端口驱动程序失败，OID 请求不能失败。 这样做会泄漏内存或其他资源。</p></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>已失败的 OID。 使用 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong> 查找此 OID 的名称。</p></td>
<td align="left"><p>完成 OID 请求 NDIS_STATUS_XXX)  (失败状态代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>NDIS_BUGCHECK_OID_REQUEST_INVALID_BUFFER</p>
<p>微型端口驱动程序或筛选器驱动程序已非法完成 OID 请求。 检查 BytesWritten 是否不大于缓冲区的整个长度。</p></td>
<td align="left"><p>特定微型端口适配器或筛选器模块块的地址。 请运行 <strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd. get-netadapter</a></strong> 或 <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd</a></strong> ，以获取详细信息。</p></td>
<td align="left"><p>已非法完成的 <strong><a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)">NDIS_OID_REQUEST</a></strong> 的地址。 请检查 <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">！ ndiskd</a></strong>。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>NDIS_BUGCHECK_REFCOUNT_IMBALANCE</p>
<p>NDIS 在内部引用计数中检测到错误。 这可能是由于引用计数下溢 (比引用) 更多的取消引用，或者标记不匹配造成的。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>内部句柄。 使用 <strong><a href="-ndiskd-ndisref.md" data-raw-source="[!ndiskd.ndisref](-ndiskd-ndisref.md)">！ ndiskd. ndisref</a></strong> 或强制转换为 ndis！NDIS_REFCOUNT_BLOCK。</p></td>
<td align="left"><p>当前 reftag 值</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION</p>
<p>小型端口驱动程序已以非法状态转换完成状态转换。</p></td>
<td align="left"><p>失败的内容。 可能的值：</p>
<ol>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_PAUSE_COMPLETE</p>
<p>小型端口称为 <strong>NdisMPauseComplete</strong> ，但没有挂起的暂停操作。</p></li>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_RESTART_COMPLETE</p>
<p>小型端口称为 <strong>NdisMRestartComplete</strong> ，但没有挂起的重启操作。</p></li>
</ol></td>
<td align="left"><p>特定微型端口适配器块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>NDIS_BUGCHECK_STATUS_INDICATION_INVALID_BUFFER</p>
<p>微型端口驱动程序或筛选器驱动程序指示一个非法 <strong><a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication" data-raw-source="[NDIS_STATUS_INDICATION](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)">NDIS_STATUS_INDICATION</a></strong>。</p></td>
<td align="left"><p>状态指示的类型。 有关详细信息，请运行 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">ndiskd。</a></strong> 有关此代码的帮助。</p></td>
<td align="left"><p>指示此非法状态指示的驱动程序实例的句柄。 有关详细信息，请运行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">ndiskd！ get-netadapter</a></strong>或<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>状态指示负载的地址。 其解释取决于状态指示的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OBJECT_HEADER</p>
<p>驱动程序创建的 <strong><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header" data-raw-source="[NDIS_OBJECT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)">NDIS_OBJECT_HEADER</a></strong>无效。</p></td>
<td align="left"><p>指示非法状态指示的驱动程序的句柄。 有关详细信息，请运行带此句柄的<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd. 微型驱动程序</a></strong>或<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>标头格式不正确的对象。 其解释取决于所调用的 API。 例如，如果驱动程序名为 <strong>NdisAllocateCloneOidRequest</strong>，则将对象强制转换为 ndis！NDIS_OID_REQUEST。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_NET_PNP_EVENT</p>
<p>微型端口驱动程序或筛选器驱动程序指示一个非法 <strong><a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification" data-raw-source="[NET_PNP_EVENT_NOTIFICATION](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)">NET_PNP_EVENT_NOTIFICATION</a></strong>。</p></td>
<td align="left"><p>指示非法状态指示的驱动程序的句柄。 有关详细信息，请运行带此句柄的<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd. 微型驱动程序</a></strong>或<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>强制转换为 NET_PNP_EVENT_NOTIFICATION</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>NDIS_BUGCHECK_PD_ERROR</p>
<p>数据包直接数据路径中检测到错误。</p></td>
<td align="left"><p>错误检查的子类型。 可能的值：</p>
<ol>
<li><p>NDIS_BUGCHECK_PD_ERROR_EC_THREAD_MISMATCH</p>
<p>在错误的线程上调用了 API。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_BY_CLIENT</p>
<p>PD 客户端尝试在处于非法状态时对提供程序进行 arm。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION</p>
<p>当未提供时，PD 提供程序会非法触发排出通知。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION_VIA_ISR</p>
<p>当未提供 ISR 排出通知时，它会对它进行非法触发。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_THUNK_BY_LWF</p>
<p>筛选器驱动程序尝试干扰 Packet Direct 数据路径。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_BM_GROUP_REQUEST</p>
<p>PD 提供程序从缓冲区管理器组中非法尝试删除其自身。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_PD_BUFFER_SETUP</p>
<p>PD 缓冲区安装请求格式不正确。</p></li>
</ol></td>
<td align="left"><p>参数3的值取决于参数2的值。 此列表中的每个数字对应于参数2中的相同数字。</p>
<ol>
<li>强制转换为 NDIS_PD_EC</li>
<li>强制转换为 NDIS_PD_QUEUE_TRACKER</li>
<li>强制转换为 NDIS_PD_QUEUE_TRACKER</li>
<li>强制转换为 NDIS_PD_QUEUE_TRACKER</li>
<li>特定筛选器模块的句柄。 有关详细信息，请运行 ndiskd 和此句柄的<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">筛选器。</a></strong></li>
<li>缓冲管理器组（如果已知）</li>
<li>源 PD_MEMORY_HANDLE 或 PD_BUFFER</li>
</ol></td>
<td align="left"><p>参数4的值取决于参数2的值。 此列表中的每个数字对应于参数2中的相同数字。</p>
<ol>
<li>预期的 ETHREAD</li>
<li>PD 客户端的句柄</li>
<li>PD 提供程序的句柄。 有关详细信息，请运行包含此句柄的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></li>
<li>PD 提供程序的句柄。 有关详细信息，请运行包含此句柄的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></li>
<li>PD 提供程序的句柄。 有关详细信息，请运行包含此句柄的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">！ ndiskd。</a></strong></li>
<li><p>如果参数3是0，则这是提供程序句柄。</p>
<p>如果参数3为非零，则 PD 客户端尚未释放所有分配，这是 PD 客户端句柄。</p></li>
<li>目标 PD_BUFFER</li>
</ol></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNEXPECTED_FAILURE</p>
<p>内部操作意外失败。 这可能是 NDIS.SYS 本身中的 bug。</p></td>
<td align="left"><p>失败的操作。 可能的值：</p>
<p>0x01： NDIS_BUGCHECK_UNEXPECTED_FAILURE_KEWAITFORSINGLEOBJECT</p>
<p>对 KeWaitForSingleObject 的调用失败。</p></td>
<td align="left"><p>失败状态代码</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>NDIS_BUGCHECK_WATCHDOG</p>
<p>尝试管理网络堆栈花费了太长时间。 当 NDIS 调用其他驱动程序时，NDIS 会启动监视程序计时器，以确保调用立即完成。 如果调用时间过长，NDIS 将注入错误检测。</p>
<p>这可能是由简单的死锁引起的。 查找 "！ stack 2 ndis" 或类似的，以查看是否有任何线程看起来可疑。 请特别注意 NDIS_WATCHDOG_TRIAGE_BLOCK 的 PrimaryThread。</p>
<p>这可能是由于丢失 Nbl 导致的，在这种情况下， <strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">ndiskd pendingnbls</a></strong> 可能会有所帮助。 使用 <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">！ ndiskd</a></strong>检查是否粘滞了 oid。</p></td>
<td align="left"><p>花费了太长时间的操作。 可能的值：</p>
<ul>
<li><p>0x01： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_PAUSE</p>
<p>暂停协议驱动程序时超时。</p></li>
<li><p>0x02： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_NETPNPEVENT</p>
<p>将 NET_PNP_EVENT_NOTIFICATION 传递到协议驱动程序时超时。</p></li>
<li><p>0x03： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_STATUS_INDICATION</p>
<p>向协议驱动程序传递状态指示时出现超时。</p></li>
<li><p>0x04： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_UNBIND</p>
<p>取消绑定协议驱动程序时超时。</p></li>
<li><p>0x11： NDIS_BUGCHECK_WATCHDOG_FILTER_PAUSE</p>
<p>暂停筛选器驱动程序时超时。</p></li>
<li><p>0x12： NDIS_BUGCHECK_WATCHDOG_FILTER_NETPNPEVENT</p>
<p>将 NET_PNP_EVENT_NOTIFICATION 传递到筛选器驱动程序时超时。</p></li>
<li><p>0x13： NDIS_BUGCHECK_WATCHDOG_FILTER_STATUS_INDICATION</p>
<p>向筛选器驱动程序传递状态指示时出现超时。</p></li>
<li><p>0x14： NDIS_BUGCHECK_WATCHDOG_FILTER_DETACH</p>
<p>分离筛选器驱动程序时超时。</p></li>
<li><p>0x21： NDIS_BUGCHECK_WATCHDOG_MINIPORT_PAUSE</p>
<p>暂停微型端口适配器时超时。</p></li>
<li><p>0x22： NDIS_BUGCHECK_WATCHDOG_MINIPORT_HALT</p>
<p>停止微型端口适配器时超时。</p></li>
<li><p>0x23： NDIS_BUGCHECK_WATCHDOG_MINIPORT_OID</p>
<p>向微型端口适配器传递 OID 请求时出现超时。</p></li>
<li><p>0x24： NDIS_BUGCHECK_WATCHDOG_FILTER_OID</p>
<p>向筛选器驱动程序传递 OID 请求时出现超时。</p></li>
<li><p>0x25： NDIS_BUGCHECK_WATCHDOG_MINIPORT_IDLE</p>
<p>置于空闲状态微型端口适配器时出现超时。</p></li>
<li><p>0x26： NDIS_BUGCHECK_WATCHDOG_CANCEL_IDLE</p>
<p>在微型端口适配器上取消空闲请求时出现超时。</p></li>
</ul></td>
<td align="left"><p>强制转换为 ndis！NDIS_WATCHDOG_TRIAGE_BLOCK。 有用字段：</p>
<ul>
<li><strong>StartTime</strong> 以100ns 为单位显示操作开始的时间，KeQueryInterruptTime 返回。</li>
<li><strong>TimeoutMilliseconds</strong> 显示了在触发此错误检测之前，NDIS 至少等待多长时间。</li>
<li><strong>TargetObject</strong> 是 NDIS 正在等待的协议、筛选器模块或微型端口适配器的句柄。 有关详细信息，请运行<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">！ ndiskd</a></strong>、 <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd</a></strong>或带有此句柄的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">get-netadapter！ ndiskd。</a></strong></li>
<li><strong>PrimaryThread</strong> 是 NDIS 启动操作的线程。 通常，这是要查找的第一个位置，但如果异步处理操作，则线程可能已在其他位置。</li>
</ul></td>
<td align="left"><p>参数4的值取决于参数2的值。 此列表中的每个数字对应于参数2中的相同十六进制值。</p>
<ul>
<li>0x01：0</li>
<li>0x02：停滞事件的 NET_PNP_EVENT_CODE。 有关这些代码的详细信息，请参阅 <strong><a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event" data-raw-source="[NET_PNP_EVENT](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)">NET_PNP_EVENT</a></strong>。</li>
<li>0x03：停滞指示的 NDIS_STATUS 代码。 使用 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong> 对其进行解码。</li>
<li>0x04：0</li>
<li>0x11：0</li>
<li>0x12：停滞事件的 NET_PNP_EVENT_CODE。 有关可能的值，请参阅此列表中的项2的先前值列表。</li>
<li>0x13：停滞指示的 NDIS_STATUS 代码。 使用 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong> 对其进行解码。</li>
<li>0x14：0</li>
<li>0x21：0</li>
<li>0x22：0</li>
<li>0x23：停滞请求的 OID 代码。 使用 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong> 对其进行解码。</li>
<li>0x24：停滞请求的 OID 代码。 使用 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong> 对其进行解码。</li>
<li>0x25：0</li>
<li>0x26：0</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OID_COMPLETION</p>
<p>微型端口驱动程序试图完成当前未在该微型端口驱动程序上挂起的 OID 请求。 这可能是由于驱动程序尝试多次完成同一个请求而导致的。</p></td>
<td align="left"><p>导致错误检测的微型端口驱动程序句柄。 有关详细信息，请运行包含此句柄的<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>正在尝试完成微型端口驱动程序的 NDIS OID 请求。 可以尝试用此请求运行 <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">！ ndiskd</a></strong> ，但此时内存可能无效。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>NDIS_BUGCHECK_LEAKED_NBL</p>
<p>驱动程序已泄漏 <strong><a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list" data-raw-source="[NET_BUFFER_LIST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)">NET_BUFFER_LIST</a></strong> 结构。 查看 <strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">！ ndiskd. pendingnbls</a></strong> 以查看此驱动程序上仍处于挂起状态的任何 nbl。</p></td>
<td align="left"><p>检测到泄漏的位置。 可能的值：</p>
<ul>
<li><p>0x01： NBL 跟踪器检测到泄漏。 当前正在取消注册或取消绑定的驱动程序是最可能的原因。 查看 bugchecking 线程的调用堆栈。 驱动程序在仍保持活动 Nbl 时不能取消绑定或取消注册。</p></li>
</ul></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

参数1指示 BUGCODE \_ NDIS \_ 驱动程序 bug 检查的特定原因。

<a name="remarks"></a>备注
-------

BUGCODE \_ NDIS \_ 驱动程序错误检查 indendifies 网络驱动程序中的问题。 通常，问题是由 NDIS 微型端口驱动程序引起的。 可以通过使用 [**！ ndiskd. get-netadapter**](-ndiskd-netadapter.md)获取 NDIS 微型端口驱动程序的完整列表。 使用 [**！ ndiskd**](-ndiskd-netreport.md)，可以更深入地了解网络堆栈。

此 bug 检查代码仅发生在 Microsoft Windows Server 2003 和更高版本的 Windows 上。 在 Windows 2000 和 Windows XP 中，对应的代码为 [**bug 检查 0xD2**](bug-check-0xd2--bugcode-id-driver.md) (BUGCODE \_ ID \_ 驱动程序) 。

