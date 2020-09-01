---
title: VMQ 的标准化 INF 关键字
description: VMQ 的标准化 INF 关键字
ms.assetid: 5DA92019-D2E0-41D9-9C31-94E464B824BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0092afb94b5c282cb584125b7a5d4db7287bb819
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214398"
---
# <a name="standardized-inf-keywords-for-vmq"></a>VMQ 的标准化 INF 关键字


定义了以下标准化 INF 关键字，以启用或禁用对虚拟机队列的支持 (VMQ) 网络适配器功能。

<a href="" id="-vmq"></a>**\*VMQ**  
一个值，该值描述设备是否已启用或禁用 VMQ 功能。

<a href="" id="-vmqlookaheadsplit"></a>**\*VMQLookaheadSplit**  
一个值，该值描述设备是否已启用或禁用将接收缓冲区拆分为预测先行缓冲区和后期预测缓冲区的能力。 微型端口驱动程序在 \_ \_ \_ \_ \_ [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的**SupportedQueueProperties**成员中报告此功能和 ndis 接收筛选器预测先行拆分支持的标志。 有关此功能的详细信息，请参阅 [接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)。

**注意**  从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 从 Windows Server 2012 开始，此 INF 关键字已过时。



<a href="" id="-vmqvlanfiltering"></a>**\*VMQVlanFiltering**  
一个值，该值描述设备是否已启用或禁用使用 media access control (MAC) 标头中的 VLAN 标识符来筛选网络数据包。 微型端口驱动程序 \_ \_ \_ \_ \_ \_ \_ 在[**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的**SupportedMacHeaderFields**成员中报告此功能和 ndis 接收筛选器 MAC 标头 VLAN ID 支持的标志。

<a href="" id="-rssorvmqpreference"></a>**\*RssOrVmqPreference**  
一个值，用于定义是否应启用 VMQ 功能，而不是接收方缩放 (RSS) 功能。

这是一个隐藏的关键字值，不得在 INF 文件中指定，并且不会显示在网络适配器的 " **高级** " 属性页中。 有关详细信息，请参阅 [处理 VMQ 和 RSS INF 关键字](#vmq-rss)。

VMQ 标准化 INF 关键字是枚举关键字。 下表描述了 VMQ 标准化 INF 关键字的可能 INF 条目。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">值</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>VMQ</strong></p></td>
<td align="left"><p>虚拟机队列</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>VMQLookaheadSplit</strong></p></td>
<td align="left"><p>VMQ 预测先行拆分</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p>
<div class="alert">
<strong>注意</strong>  从 NDIS 6.30 开始，不再支持该关键字。
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>VMQVlanFiltering</strong></p></td>
<td align="left"><p>VMQ VLAN 筛选</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>RssOrVmqPreference</strong></p></td>
<td align="left"><p>注意：此子项的 ParamDesc 和 EnumDesc 条目不能用于 INF 文件或用户界面。 有关详细信息，请参阅 <a href="#vmq-rss" data-raw-source="[Handling VMQ and RSS INF Keywords](#vmq-rss)">处理 VMQ 和 RSS INF 关键字</a>。</p></td>
<td align="left"><p>0（默认值）</p></td>
<td align="left"><div class="alert">
<strong>注意</strong>  报表 RSS 功能
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><div class="alert">
<strong>注意</strong><br/><p>报告 VMQ 功能</p>
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



此表中的列描述了用于枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称还会显示在注册表中网络适配器的**NDI** \\ **params**键下。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName INF 条目关联的显示文本。

**注意**  独立硬件供应商 (IHV) 可以定义 SubkeyName 的任何说明性文本。



<a href="" id="value"></a>负值  
与列表中的每个 SubkeyName 相关联的枚举整数值。

<a href="" id="enumdesc"></a>EnumDesc  
与显示在 " **高级** " 属性页中的每个值相关联的显示文本。

有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

### <a name="handling-vmq-and-rss-inf-keywords"></a><a href="" id="vmq-rss"></a>处理 VMQ 和 RSS INF 关键字

支持 VMQ 和接收方缩放 (RSS) 的网络适配器无法同时使用这些功能。 操作系统可通过以下方式使用 RSS 或 VMQ 功能：

-   将网络适配器绑定到 TCP/IP 堆栈后，操作将启用 RSS 功能的使用。

-   将网络适配器绑定到 Hyper-v 可扩展交换机驱动程序堆栈时，操作系统将启用 VMQ 功能。

    有关详细信息，请参阅 [Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)。

由于网络适配器未被禁用，然后在未绑定到 TCP/IP stack 时重新启用，并绑定到 Hyper-v 驱动程序堆栈 (或反向) ，因此，此类网络适配器无法自动在 VMQ 和 RSS 之间切换。

当 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，微型端口驱动程序会在向 NDIS 报告当前启用的 VMQ 或 RSS 功能之前执行以下步骤：

1.  微型端口驱动程序在将其当前启用的功能报告给 NDIS 之前，读取** \* RssOrVmqPreference**关键字。

    如果** \* RssOrVmqPreference**关键字的值为1，则为 VMQ 首选项配置微型端口驱动程序。

    如果** \* RssOrVmqPreference**关键字的值为零，或者关键字不存在，则为 RSS 首选项配置微型端口驱动程序。

2.  如果为 VMQ 首选项配置微型端口驱动程序，则必须读取** \* vmq**关键字，以确定网络适配器上是否已启用 vmq。 如果关键字设置为1，则驱动程序将报告当前启用的 VMQ 设置。 有关微型端口驱动程序如何报告 VMQ 设置的详细信息，请参阅 [确定网络适配器的 Vmq 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

    有关 VMQ 关键字的详细信息，请参阅 VMQ 的标准化 INF 关键字。

    **注意**  如果为 VMQ 首选项配置微型端口驱动程序，则不能读取任何 RSS 标准化关键字。



3.  如果为 RSS 首选项配置微型端口驱动程序，则必须阅读** \* rss**关键字，以确定是否在网络适配器上启用了 rss。 如果关键字设置为1，则驱动程序将报告当前启用的 RSS 设置。 有关微型端口驱动程序如何报告 RSS 设置的详细信息，请参阅 [Rss 配置](rss-configuration.md)。

    有关 RSS 关键字的详细信息，请参阅 [rss 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)。

    **注意**  如果为 RSS 首选项配置微型端口驱动程序，则它不能读取任何 VMQ 标准化关键字。



下表描述了微型端口驱动程序如何根据注册表关键字确定 RSS 或 VMQ 首选项和广告功能：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>RssOrVmqPreference</th>
<th align="left"></em>VMQ</th>
<th align="left">* RSS</th>
<th align="left">已公布 VMQ 或 RSS 功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>None</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>



**注意**  无需考虑这些关键字的值，微型端口驱动程序必须始终报告完整的 RSS 和 VMQ 硬件功能。 这些关键字设置只影响驱动程序报告当前启用的 RSS 和 VMQ 功能的方式。



### <a name="reserved-registry-keywords"></a>保留的注册表关键字

如果微型端口驱动程序支持 VMQ 并在网络适配器上启用 VMQ 接口，则驱动程序不得读取以下 RSS INF 条目：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS 接口的最大处理器数目。</p></td>
<td align="left"><p>0到 (MAXIMUM_PROC_PER_GROUP) ，</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS 处理器的最大数量。</p></td>
<td align="left"><p>1到 MAXIMUM_PROC_PER_SYSTEM。</p></td>
</tr>
</tbody>
</table>



支持 VMQ 的微型端口驱动程序不得读取**HKEY \_ LOCAL \_ MACHINE** \\ **SYSTEM** \\ **CurrentControlSet** \\ **services** \\ **VMSMP** \\ **Parameters**注册表项下的以下子项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<p><strong>TenGigVmqEnabled</strong></p></td>
<td align="left"><p>启用或禁用所有 (Gbps) 网络适配器上每秒10个千兆千兆位的 VMQ。</p></td>
<td align="left"><p>0 = 禁用 Windows Server 2008 R2) 的系统默认 (。</p>
<p>1 = 已启用。</p>
<p>2 = 显式禁用。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong>BelowTenGigVmqEnabled</strong></p></td>
<td align="left"><p>在支持小于 10 Gbps 的所有网络适配器上启用或禁用 VMQ。</p></td>
<td align="left"><p>0 = 禁用 Windows Server 2008 R2) 的系统默认 (。</p>
<p>1 = 已启用。</p>
<p>2 = 显式禁用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS 接口的最大处理器数目。</p></td>
<td align="left"><p>0到 (MAXIMUM_PROC_PER_GROUP) ，</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS 处理器的最大数量。</p></td>
<td align="left"><p>1到 MAXIMUM_PROC_PER_SYSTEM。</p></td>
</tr>
</tbody>
</table>