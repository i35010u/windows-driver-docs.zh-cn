---
title: Bug 检查 0x15E BUGCODE_NDIS_DRIVER_LIVE_DUMP
description: BUGCODE_NDIS_DRIVER_LIVE_DUMP bug 代码具有 0x0000015E 值。 此错误代码指示 NDIS 已捕获的实时内核转储。 NDIS 不在此情况下生成的 bug 检查。
ms.assetid: 3663A955-A1D7-4880-BD83-0976012F2CB1
keywords:
- Bug 检查 0x15E BUGCODE_NDIS_DRIVER_LIVE_DUMP
- BUGCODE_NDIS_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_NDIS_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e98fcf1099ed5daaf66c261fd9f27a899dabb74e
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903403"
---
# <a name="bug-check-0x15e-bugcodendisdriverlivedump"></a>Bug 检查 0x15E：BUGCODE\_NDIS\_驱动程序\_LIVE\_转储


BUGCODE\_NDIS\_驱动程序\_LIVE\_转储错误代码的值为 0x0000015E。 此错误代码指示 NDIS 已捕获的实时内核转储。 NDIS 不在此情况下生成的 bug 检查。

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
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FATAL_ERROR</p>
<p>微型端口驱动程序已遇到错误并且已请求重新枚举。</p></td>
<td align="left"><p>微型端口块的地址。 运行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd.minidriver</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>地址的微型端口的物理设备对象 (PDO)</p></td>
<td align="left"><p>导致要执行此实时转储的致命错误。 可能值：</p>
<ol>
<li>70:引起用户模式</li>
<li>71:引起 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff563661" data-raw-source="[NdisMRemoveMiniport](https://msdn.microsoft.com/library/windows/hardware/ff563661)">NdisMRemoveMiniport</a></strong></li>
<li>72:引起<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562727" data-raw-source="[NdisIMInitializeDeviceInstanceEx](https://msdn.microsoft.com/library/windows/hardware/ff562727)">NdisIMInitializeDeviceInstanceEx</a></strong>失败</li>
<li>73:引起<em><a href="https://msdn.microsoft.com/library/windows/hardware/ff559435" data-raw-source="[MiniportRestart](https://msdn.microsoft.com/library/windows/hardware/ff559435)">MiniportRestart</a></em>失败</li>
<li>74:引起的失败<a href="https://msdn.microsoft.com/library/windows/hardware/ff569780" data-raw-source="[OID_PNP_SET_POWER (D0)](https://msdn.microsoft.com/library/windows/hardware/ff569780)">OID_PNP_SET_POWER (D0)</a>请求</li>
<li>75:引起的失败<a href="https://msdn.microsoft.com/library/windows/hardware/ff569780" data-raw-source="[OID_PNP_SET_POWER (Dx)](https://msdn.microsoft.com/library/windows/hardware/ff569780)">OID_PNP_SET_POWER (Dx)</a>请求</li>
</ol></td>
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
<td align="left"><p>参数 4 的值取决于参数 2 的值。 此列表中的每个数字对应于参数 2 中的相同编号。</p>
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
<td align="left"><p>0x30</p></td>
<td align="left"><p>NDIS_BUGCHECK_STUCK_NBL</p>
<p>微型端口驱动程序未返回 NBL 回堆栈段时间。</p></td>
<td align="left"><p>微型端口块的地址。 运行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd.minidriver</a></strong>与此地址用于的详细信息。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

参数 1 指示 BUGCODE 的特定原因\_NDIS\_驱动程序\_LIVE\_转储错误检查。

<a name="remarks"></a>备注
-------

NDIS 已检测到并从另一个网络驱动程序中的严重问题中恢复。 尽管系统不会被暂停，但此问题可能更高版本会导致连接问题或致命执行错误检查。

仅在 Windows 8.1 和更高版本的 Windows 中会出现此错误代码。

 

 




