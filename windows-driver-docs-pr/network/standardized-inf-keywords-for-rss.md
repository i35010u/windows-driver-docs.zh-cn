---
title: RSS 的标准化 INF 关键字
description: RSS 的标准化 INF 关键字
ms.assetid: 0ea0d6f7-0dc5-40dd-a706-4712e19dbfdb
keywords:
- 接收方缩放 WDK 网络，标准化 INF 关键字
- RSS WDK 网络，标准化 INF 关键字
- 标准化 INF 关键字 WDK RSS
- INF 条目 WDK RSS
ms.date: 02/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4887f79e6ff38d20300b923dc4c11b0a2d8b37d9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214410"
---
# <a name="standardized-inf-keywords-for-rss"></a>RSS 的标准化 INF 关键字

RSS 接口支持显示在注册表中并在 INF 文件中指定的 [标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md) 。

以下列表显示了 RSS 的枚举 [标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md) ：

<a href="" id="---------rss"></a>** \* RSS**  
启用或禁用微型端口适配器的 RSS 支持。

<a href="" id="---------rssprofile"></a>** \* RSSProfile**  
处理器选择和负载平衡配置文件。

**注意**   对** \* RSSProfile**设置的更改需要重新启动适配器。

 

枚举标准化 INF 关键字具有以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定并且出现在注册表中的关键字的名称。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

<a href="" id="value"></a>负值  
与列表中的每个选项关联的枚举整数值。 此值存储在 NDI \\ params \\ *SubkeyName* \\ *值*中。

<a href="" id="enumdesc"></a>EnumDesc  
与菜单中显示的每个值相关联的显示文本。

<a href="" id="default"></a>缺省值  
菜单的默认值。

下表描述了 RSS 枚举关键字的可能的 INF 条目。

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
<td align="left"><p><strong><em>技术</strong></p></td>
<td align="left"><p>接收方缩放</p></td>
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
<td align="left"><p><strong></em>RSSProfile</strong></p></td>
<td align="left"><p>RSS 负载平衡配置文件</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>ClosestProcessor</strong>：默认行为与 Windows Server 2008 R2 的行为一致。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>ClosestProcessorStatic</strong>：没有动态负载平衡-在运行时分配但不进行负载平衡。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p><strong>NUMAScaling</strong>：在每个 NUMA 节点上以循环方式分配 RSS cpu，使在 numa 服务器上运行的应用程序可以很好地进行缩放。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p>
<p>（默认值）</p></td>
<td align="left"><p><strong>NUMAScalingStatic</strong>： RSS 处理器选择与无需动态负载平衡的 NUMA 可伸缩性相同。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p><strong>ConservativeScaling</strong>： RSS 使用尽可能少的处理器来维持负载。 此选项可帮助减少中断的数量。</p></td>
</tr>
</tbody>
</table>

 

NDIS 6.30 添加了对** \* RSSProfile**的支持。

以下列表显示了可编辑 RSS 的 [标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md) ：

<a href="" id="---------rssbaseprocgroup"></a>** \* RssBaseProcGroup**  
在** \* RssBaseProcNumber**关键字中指定的处理器编号的处理器组的数目。

<a href="" id="---------numanodeid"></a>** \* NumaNodeId**  
用于网络适配器的内存分配的首选 NUMA 节点。 此外，操作系统会首先尝试使用首选 NUMA 节点中的 Cpu 进行 RSS。

PCI 扩展卡的驱动程序不应在其 INF 中静态指定 NUMA 节点 ID，因为最近的节点取决于插入卡的 PCI 插槽。  仅当网络适配器已集成到系统中时，才指定** \* NumaNodeId** ，将提前知道 NUMA 节点，并且在运行时无法通过查询 ACPI 确定节点。

**注意**   如果此关键字存在并且其值小于计算机中 NUMA 节点的数目，NDIS 将在[**ndis \_ RSS \_ 处理器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)结构的**PreferredNumaNode**成员中使用此值。

 

**注意**   在 Windows 8 中，如果 NIC RSS 配置文件设置为**NUMAScaling** (2) 或**NUMAScalingStatic** (3) ，则会忽略** \* NumaNodeId**值。

 

<a href="" id="---------rssbaseprocnumber"></a>** \* RssBaseProcNumber**  
指定组中基本 RSS 处理器的数目。

<a href="" id="---------maxrssprocessors"></a>** \* MaxRssProcessors**  
RSS 处理器的最大数量。

<a href="" id="---------rssmaxprocnumber"></a>** \* RssMaxProcNumber**  
RSS 接口的最大处理器数目。
如果指定了** \* RssMaxProcNumber** ，则还应指定** \* RssMaxProcGroup** 。

<a href="" id="---------rssmaxprocnumber"></a>** \* NumRSSQueues**  
RSS 队列的数量。

<a href="" id="---------rssmaxprocgroup"></a>** \* RssMaxProcGroup** RSS 接口的最大处理器组。

** \* RssBaseProcGroup**和** \* RssBaseProcNumber**构成一个 PROCESSOR_NUMBER 结构，该结构标识可用于 RSS 的最小处理器数。
** \* RssMaxProcGroup**和** \* RssMaxProcNumber**构成一个 PROCESSOR_NUMBER 的结构，该结构标识可与 RSS 一起使用的最大处理器数目。

例如，假设** \* RssBaseProcGroup**设置为1， ** \* RssBaseProcNumber**设置为16， ** \* RssMaxProcGroup**设置为3， ** \* RssMaxProcNumber**设置为8。
使用 <group> ： <processor> notation，基本处理器为1:16，最大处理器为3:8。
否则，不会将处理器0:0、0:32、1:0 和1:15 视为 RSS 的候选项，因为它们低于基本处理器编号。
处理器1:16、1:31、2:0、2:63、3:0 和3:8 都将被视为 RSS 的候选项，因为它们的范围是从1:16 到3:8。
处理器3:9、3:31 和4:0 不会被视为 RSS 的候选项，因为它们超过了最大处理器数目。

NDIS 6.20 添加了对** \* RssBaseProcGroup**、 ** \* NumaNodeId**、 ** \* RssBaseProcNumber**和** \* MaxRssProcessors**关键字的支持。

NDIS 6.30 添加了对** \* RssMaxProcNumber**和** \* NumRSSQueues**关键字的支持。

可以编辑的[标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)具有以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定并且出现在注册表中的关键字的名称。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

<a href="" id="type"></a>类型  
可以编辑的值的类型。 该值可以是数字 (Int) ，也可以是可 (Edit) 编辑的文本。

<a href="" id="default-value"></a>默认值  
整数或文本的默认值。 &lt;IHV 定义 &gt; 表示该值与特定的独立硬件供应商 (IHV) 要求相关联。

<a href="" id="min"></a>Min  
允许用于整数的最小值。 &lt;IHV 定义 &gt; 表示最小值与特定的 IHV 要求关联。

<a href="" id="max"></a>数量  
整数允许的最大值。 &lt;IHV 定义 &gt; 表示最小值与特定的 IHV 要求关联。

下表描述了可以编辑的所有 RSS 关键字。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">类型</th>
<th align="left">默认值</th>
<th align="left">Min</th>
<th align="left">Max</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcGroup</strong></p></td>
<td align="left"><p>RSS 基本处理器组</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>NumaNodeId</strong></p></td>
<td align="left"><p>首选 NUMA 节点</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>65535 (任何节点) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统特定-不能超过65534</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcNumber</strong></p></td>
<td align="left"><p>RSS 基础处理器编号</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS 处理器的最大数量</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>Windows Server 2008 默认值：</p>
<p>8适用于1G 或更慢的适配器，16个适用于10G 适配器</p>
<p>Windows 8 默认值：</p>
<p>对于1GbE 或慢速适配器的无 MSI-X 支持的 Nic，4个适用于 10 GbE 适配器的 Nic。</p>
<p>对于带有 MSI-X 支持的 Nic （对于1GbE 或较慢的适配器），为16，适用于 10 GbE 适配器。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_SYSTEM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>最大 RSS 处理器编号</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1 (默认) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>NumRSSQueues</strong></p></td>
<td align="left"><p>RSS 队列的最大数目</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>设备特定</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>设备特定</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*RSSMaxProcGroup</strong></p></td>
<td align="left"><p>RSS 最大处理器组</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS-1</p></td>
</tr>
</tbody>
</table>

 

**注意**   尽管** \* RssBaseProcGroup**的有效范围为0到最大 \_ 组-1，但在 Windows 7 中，它必须为零。 否则，TCP/IP 协议不会将任何处理器用于 RSS。

 

**注意**   ** \* NumaNodeId** (65535) 的默认值表示网络适配器对于 NUMA 节点是不可知的，NDIS 不应尝试使用任何节点。
如果未提供** \* NumaNodeId**关键字，NDIS 会根据 ACPI 中的提示自动选择最近的节点。


有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

 

