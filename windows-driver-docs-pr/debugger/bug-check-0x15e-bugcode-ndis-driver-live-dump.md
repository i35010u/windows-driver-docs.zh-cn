---
title: Bug 检查 0x15E BUGCODE_NDIS_DRIVER_LIVE_DUMP
description: BUGCODE_NDIS_DRIVER_LIVE_DUMP bug 代码的值为0x0000015E。 此错误代码指示 NDIS 已捕获实时内核转储。 在这种情况下，NDIS 不会生成 bug 检查。
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
ms.openlocfilehash: 9eaa78f3d89f85e63406ffdfbd25bafe6a934e33
ms.sourcegitcommit: d2dab8b8bf335835d0341ca3f0a36eab0ec028f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72892688"
---
# <a name="bug-check-0x15e-bugcode_ndis_driver_live_dump"></a>Bug 检查0x15E： BUGCODE\_NDIS\_驱动程序\_实时\_转储


BUGCODE\_NDIS\_驱动程序\_实时\_转储错误代码的值为0x0000015E。 此错误代码指示 NDIS 已捕获实时内核转储。 在这种情况下，NDIS 不会生成 bug 检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="bugcode_ndis_driver-parameters"></a>BUGCODE\_NDIS\_驱动程序参数


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
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FATAL_ERROR</p>
<p>微型端口驱动程序遇到错误，请求重新枚举。</p></td>
<td align="left"><p>微型端口块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>微型端口的物理设备对象（PDO）的地址</p></td>
<td align="left"><p>导致执行此实时转储的严重错误。 可能值：</p>
<ol>
<li>70：由用户模式引起</li>
<li>71：由 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismremoveminiport" data-raw-source="[NdisMRemoveMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismremoveminiport)">NdisMRemoveMiniport</a>导致</strong></li>
<li>72： <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex" data-raw-source="[NdisIMInitializeDeviceInstanceEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)">NdisIMInitializeDeviceInstanceEx</a></strong>失败</li>
<li>73： <em><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart" data-raw-source="[MiniportRestart](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)">MiniportRestart</a></em>失败</li>
<li>74： <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER (D0)](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER （D0）</a>请求失败导致</li>
<li>75： <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER (Dx)](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER （Dx）</a>请求失败导致</li>
</ol></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>NDIS_BUGCHECK_WATCHDOG</p>
<p>尝试管理网络堆栈花费了太长时间。 当 NDIS 调用其他驱动程序时，NDIS 会启动监视程序计时器，以确保调用立即完成。 如果调用时间过长，NDIS 将注入错误检测。</p>
<p>这可能是由简单的死锁引起的。 查找 "！ stack 2 ndis" 或类似的，以查看是否有任何线程看起来可疑。 请特别注意 NDIS_WATCHDOG_TRIAGE_BLOCK 的 PrimaryThread。</p>
<p>这可能是由于丢失 Nbl 导致的，在这种情况下， <strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">ndiskd pendingnbls</a></strong>可能会有所帮助。 使用<strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">！ ndiskd</a></strong>检查是否粘滞了 oid。</p></td>
<td align="left"><p>花费了太长时间的操作。 可能值：</p>
<ul>
<li><p>0x01： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_PAUSE</p>
<p>暂停协议驱动程序时超时。</p></li>
<li><p>0x02： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_NETPNPEVENT</p>
<p>将 NET_PNP_EVENT_NOTIFICATION 传递到协议驱动程序时超时。</p></li>
<li><p>0x03： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_STATUS_INDICATION</p>
<p>向协议驱动程序传递状态指示时出现超时。</p></li>
<li><p>0x04： NDIS_BUGCHECK_WATCHDOG_PROTOCOL_UNBIND</p>
<p>取消绑定协议驱动程序时超时。</p></li>
<li><p>0x11 : NDIS_BUGCHECK_WATCHDOG_FILTER_PAUSE</p>
<p>暂停筛选器驱动程序时超时。</p></li>
<li><p>0x12 : NDIS_BUGCHECK_WATCHDOG_FILTER_NETPNPEVENT</p>
<p>将 NET_PNP_EVENT_NOTIFICATION 传递到筛选器驱动程序时超时。</p></li>
<li><p>0x13： NDIS_BUGCHECK_WATCHDOG_FILTER_STATUS_INDICATION</p>
<p>向筛选器驱动程序传递状态指示时出现超时。</p></li>
<li><p>0x14： NDIS_BUGCHECK_WATCHDOG_FILTER_DETACH</p>
<p>分离筛选器驱动程序时超时。</p></li>
<li><p>0x21 : NDIS_BUGCHECK_WATCHDOG_MINIPORT_PAUSE</p>
<p>暂停微型端口适配器时超时。</p></li>
<li><p>0x22： NDIS_BUGCHECK_WATCHDOG_MINIPORT_HALT</p>
<p>停止微型端口适配器时超时。</p></li>
<li><p>0x23 : NDIS_BUGCHECK_WATCHDOG_MINIPORT_OID</p>
<p>向微型端口适配器传递 OID 请求时出现超时。</p></li>
<li><p>0x24： NDIS_BUGCHECK_WATCHDOG_FILTER_OID</p>
<p>向筛选器驱动程序传递 OID 请求时出现超时。</p></li>
<li><p>0x25： NDIS_BUGCHECK_WATCHDOG_MINIPORT_IDLE</p>
<p>置于空闲状态微型端口适配器时出现超时。</p></li>
<li><p>0x26： NDIS_BUGCHECK_WATCHDOG_CANCEL_IDLE</p>
<p>在微型端口适配器上取消空闲请求时出现超时。</p></li>
</ul></td>
<td align="left"><p>强制转换为 ndis！NDIS_WATCHDOG_TRIAGE_BLOCK. 有用字段：</p>
<ul>
<li><strong>StartTime</strong>以100ns 为单位显示操作开始的时间，KeQueryInterruptTime 返回。</li>
<li><strong>TimeoutMilliseconds</strong>显示了在触发此错误检测之前，NDIS 至少等待多长时间。</li>
<li><strong>TargetObject</strong>是 NDIS 正在等待的协议、筛选器模块或微型端口适配器的句柄。 有关详细信息，请运行<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">！ ndiskd</a></strong>、 <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">！ ndiskd</a></strong>或带有此句柄的<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">get-netadapter！ ndiskd。</a></strong></li>
<li><strong>PrimaryThread</strong>是 NDIS 启动操作的线程。 通常，这是要查找的第一个位置，但如果异步处理操作，则线程可能已在其他位置。</li>
</ul></td>
<td align="left"><p>参数4的值取决于参数2的值。 此列表中的每个数字对应于参数2中的相同数字。</p>
<ul>
<li>0x01：0</li>
<li>0x02：停滞事件的 NET_PNP_EVENT_CODE。 有关这些代码的详细信息，请参阅<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event" data-raw-source="[NET_PNP_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)">NET_PNP_EVENT</a></strong>。</li>
<li>0x03：停滞指示的 NDIS_STATUS 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong>对其进行解码。</li>
<li>0x04：0</li>
<li>0x11：0</li>
<li>0x12：停滞事件的 NET_PNP_EVENT_CODE。 有关可能的值，请参阅此列表中的项2的先前值列表。</li>
<li>0x13：停滞指示的 NDIS_STATUS 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong>对其进行解码。</li>
<li>0x14：0</li>
<li>0x21：0</li>
<li>0x22：0</li>
<li>0x23：停滞请求的 OID 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong>对其进行解码。</li>
<li>0x24：停滞请求的 OID 代码。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">！ ndiskd</a></strong>对其进行解码。</li>
<li>0x25：0</li>
<li>0x26：0</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>0x30</p></td>
<td align="left"><p>NDIS_BUGCHECK_STUCK_NBL</p>
<p>小型端口驱动程序已有一段时间未将 NBL 返回到堆栈。</p></td>
<td align="left"><p>微型端口块的地址。 有关详细信息，请运行带此地址的<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">！ ndiskd。</a></strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

[ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 参数1指示 BUGCODE\_NDIS\_驱动程序\_实时\_转储错误检查的具体原因。

<a name="remarks"></a>备注
-------

NDIS 已检测到另一个网络驱动程序中的严重问题，并已将其恢复。 尽管系统未暂停，但以后可能会导致连接问题或致命错误检测。

此错误代码仅出现在 Windows 8.1 和更高版本的 Windows 中。

 

 




