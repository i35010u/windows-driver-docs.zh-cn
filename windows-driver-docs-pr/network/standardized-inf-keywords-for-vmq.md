---
title: VMQ 的标准化 INF 关键字
description: VMQ 的标准化 INF 关键字
ms.assetid: 5DA92019-D2E0-41D9-9C31-94E464B824BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6f017ffae2aa165dc383e15467d8aae8bafae36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390655"
---
# <a name="standardized-inf-keywords-for-vmq"></a>VMQ 的标准化 INF 关键字


以下的标准化的 INF 关键字定义来启用或禁用对虚拟机队列 (VMQ) 功能的网络适配器的支持。

<a href="" id="-vmq"></a>**\*VMQ**  
一个值，描述该设备是否已启用或禁用 VMQ 功能。

<a href="" id="-vmqlookaheadsplit"></a>**\*VMQLookaheadSplit**  
一个值，描述该设备已启用还是禁用的功能拆分接收到预测先行缓冲区和 post 预测先行缓冲区。 微型端口驱动程序报告此功能与的 NDIS\_接收\_筛选器\_预测先行\_拆分\_中的受支持标志**SupportedQueueProperties**成员[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。 有关此功能的详细信息，请参阅[接收缓冲区中的 Shared Memory](shared-memory-in-receive-buffers.md)。

**请注意**从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 从 Windows Server 2012 开始，此 INF 关键字已过时。



<a href="" id="-vmqvlanfiltering"></a>**\*VMQVlanFiltering**  
一个值，描述设备是否已启用或禁用筛选网络数据包的功能使用 VLAN 标识符中的媒体访问控制 (MAC) 标头。 微型端口驱动程序报告此功能与的 NDIS\_接收\_筛选器\_MAC\_标头\_VLAN\_ID\_中的支持标志**SupportedMacHeaderFields**的成员[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

<a href="" id="-rssorvmqpreference"></a>**\*RssOrVmqPreference**  
一个值，用于定义是否应启用 VMQ 功能状态而不是接收方缩放 (RSS) 功能。

这是一个隐藏的关键字值不得指定 INF 文件中并不会显示在**高级**网络适配器的属性页。 有关详细信息，请参阅[处理 VMQ 和 RSS INF 关键字](#vmq-rss)。

VMQ 标准化 INF 关键字是枚举的关键字。 下表介绍可能的 INF 项 VMQ 标准化 INF 关键字。

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
<th align="left">ReplTest1</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>VMQ</strong></p></td>
<td align="left"><p>虚拟机队列</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>VMQLookaheadSplit</strong></p></td>
<td align="left"><p>VMQ 预测先行拆分</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p>
<div class="alert">
<strong>请注意</strong>从 NDIS 6.30 开始，不再支持此关键字。
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>VMQVlanFiltering</strong></p></td>
<td align="left"><p>VMQ VLAN 筛选</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>RssOrVmqPreference</strong></p></td>
<td align="left"><p>注意：此子项的 ParamDesc 和 EnumDesc 项不能使用 INF 文件或用户界面中。 有关详细信息，请参阅<a href="#vmq-rss" data-raw-source="[Handling VMQ and RSS INF Keywords](#vmq-rss)">处理 VMQ 和 RSS INF 关键字</a>。</p></td>
<td align="left"><p>0 （默认值）</p></td>
<td align="left"><div class="alert">
<strong>请注意</strong>报表 RSS 功能
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><div class="alert">
<strong>注意</strong><br/><p>报表 VMQ 功能</p>
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



此表中的列描述枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表**NDI**\\**params**关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName INF 条目关联的显示文本。

**请注意**独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。



<a href="" id="value"></a>值  
枚举的整数值与列表中每个 SubkeyName 相关联。

<a href="" id="enumdesc"></a>EnumDesc  
将出现在每个值与相关联的显示文本**高级**属性页。

有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

### <a href="" id="vmq-rss"></a>处理 VMQ 和 RSS INF 关键字

支持 VMQ 和接收方缩放 (RSS) 的网络适配器不能同时使用这些功能。 操作系统通过以下方式启用 RSS 或 VMQ 功能的使用：

-   在网络适配器绑定到 TCP/IP 堆栈的操作系统启用 RSS 功能的使用。

-   在网络适配器绑定到 HYPER-V 可扩展交换机驱动程序堆栈，操作系统将启用 VMQ 功能的使用。

    有关详细信息，请参阅[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。

因为网络适配器不是已禁用，然后重新启用 TCP/IP 堆栈之间的绑定和绑定到 HYPER-V 驱动程序堆栈 （或反之） 时，不能为此类自动切换 VMQ 和 RSS 的网络适配器。

当调用 NDIS [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，它的当前已启用 VMQ 或 RSS 功能报告到 NDIS 微型端口驱动程序按照以下步骤：

1.  微型端口驱动程序读取 **\*RssOrVmqPreference**关键字才到 NDIS 报告其当前已启用的功能。

    如果的值 **\*RssOrVmqPreference**关键字为 1，微型端口驱动程序配置为 VMQ 首选项。

    如果的值 **\*RssOrVmqPreference**关键字为零或关键字不存在，则为 RSS 首选项配置微型端口驱动程序。

2.  如果微型端口驱动程序配置为 VMQ 首选项，它必须读取 **\*VMQ**关键字来确定是否在网络适配器上启用 VMQ。 如果关键字设置为 1，驱动程序报告的当前已启用 VMQ 设置。 微型端口驱动程序报告 VMQ 设置的方式的详细信息，请参阅[确定网络适配器的 VMQ 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

    有关 VMQ 关键字的详细信息，请参阅对 VMQ 的标准化 INF 关键字。

    **请注意**如果微型端口驱动程序配置为 VMQ 首选项，它必须读取任意 RSS 标准化关键字。



3.  如果微型端口驱动程序配置为 RSS 首选项，它必须读取 **\*RSS**关键字来确定是否在网络适配器上启用了 RSS。 如果关键字设置为 1，驱动程序报告的当前已启用 RSS 设置。 微型端口驱动程序报告 RSS 设置的方式的详细信息，请参阅[RSS 配置](rss-configuration.md)。

    有关 RSS 关键字的详细信息，请参阅[RSS 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)。

    **请注意**如果微型端口驱动程序配置为 RSS 首选项，它必须读取任意 VMQ 标准化关键字。



下表描述了如何微型端口驱动程序确定 RSS 或 VMQ 首选项和播发功能基于注册表的关键字：

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
<th align="left">*RSS</th>
<th align="left">VMQ 或 RSS 功能播发</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>



**请注意**微型端口驱动程序必须始终报告而不考虑这些关键字值的完整 RSS 和 VMQ 硬件功能。 这些关键字设置只会影响该驱动程序报告的当前已启用的 RSS 和 VMQ 功能的方式。



### <a name="reserved-registry-keywords"></a>保留的注册表关键字

如果微型端口驱动程序支持 VMQ 并且网络适配器上启用 VMQ 接口，该驱动程序必须读取以下 RSS INF 条目：

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
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS 接口的最大处理器数。</p></td>
<td align="left"><p>0 到 (MAXIMUM_PROC_PER_GROUP-1)</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>最大 RSS 处理器数。</p></td>
<td align="left"><p>1 到 MAXIMUM_PROC_PER_SYSTEM。</p></td>
</tr>
</tbody>
</table>



支持 VMQ 的微型端口驱动程序必须读取以下子项**HKEY\_本地\_机**\\**系统**\\ **CurrentControlSet**\\**services**\\**VMSMP**\\**参数**注册表键。

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
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<p><strong>TenGigVmqEnabled</strong></p></td>
<td align="left"><p>启用或禁用 VMQ 上所有 10 千兆比特 / 秒 (Gbps) 网络适配器。</p></td>
<td align="left"><p>0 = 系统默认值 （适用于 Windows Server 2008 R2 已禁用）。</p>
<p>1 = 已启用。</p>
<p>2 = 显式禁用。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong>BelowTenGigVmqEnabled</strong></p></td>
<td align="left"><p>启用或禁用 VMQ 支持不超过 10 Gbps 的所有网络适配器上。</p></td>
<td align="left"><p>0 = 系统默认值 （适用于 Windows Server 2008 R2 已禁用）。</p>
<p>1 = 已启用。</p>
<p>2 = 显式禁用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>RSS 接口的最大处理器数。</p></td>
<td align="left"><p>0 到 (MAXIMUM_PROC_PER_GROUP-1)</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>最大 RSS 处理器数。</p></td>
<td align="left"><p>1 到 MAXIMUM_PROC_PER_SYSTEM。</p></td>
</tr>
</tbody>
</table>











