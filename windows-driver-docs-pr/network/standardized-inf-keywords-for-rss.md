---
title: RSS 的标准化 INF 关键字
description: RSS 的标准化 INF 关键字
ms.assetid: 0ea0d6f7-0dc5-40dd-a706-4712e19dbfdb
keywords:
- 接收方缩放 WDK 网络标准化 INF 关键字
- 网络、 RSS WDK 标准化 INF 关键字
- 标准化的 INF 关键字 WDK RSS
- INF 条目 WDK RSS
ms.date: 02/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2678acbbcda42f5afd9dc6a80f8e936ec15fd421
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378625"
---
# <a name="standardized-inf-keywords-for-rss"></a>RSS 的标准化 INF 关键字

RSS 接口支持[标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)，出现在注册表和 INF 文件中指定。

以下列表显示了枚举[标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)rss:

<a href="" id="---------rss"></a> **\*RSS**  
启用或禁用 rss 微型端口适配器的支持。

<a href="" id="---------rssprofile"></a> **\*RSSProfile**  
处理器所选内容和负载平衡配置文件中。

**请注意**  更改为 **\*RSSProfile**设置需要适配器重新启动。

 

枚举标准化 INF 关键字具有以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须指定 INF 文件中的关键字的名称显示在注册表中。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

<a href="" id="value"></a>值  
在列表中每个选项与关联枚举的整数值。 此值存储在 NDI\\params\\ *SubkeyName*\\*值*。

<a href="" id="enumdesc"></a>EnumDesc  
与每个菜单中显示的值相关联的显示文本。

<a href="" id="default"></a>默认值  
菜单默认值。

下表描述了可能的 INF 项 RSS 枚举关键字。

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
<td align="left"><p><strong><em>RSS</strong></p></td>
<td align="left"><p>接收方缩放</p></td>
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
<td align="left"><p><strong></em>RSSProfile</strong></p></td>
<td align="left"><p>RSS 加载平衡配置文件</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>ClosestProcessor</strong>:默认行为是一致的 Windows Server 2008 R2。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>ClosestProcessorStatic</strong>:无动态负载平衡的分发，但不在运行时的负载平衡。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p><strong>NUMAScaling</strong>:跨以便良好的伸缩性的 NUMA 服务器运行的应用程序的每个 NUMA 节点，RSS Cpu 分配在轮循机制的基础。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p>
<p>“(默认)”</p></td>
<td align="left"><p><strong>NUMAScalingStatic</strong>:RSS 处理器选择为而无需动态负载平衡的 NUMA 可伸缩性的一样。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p><strong>ConservativeScaling</strong>:RSS 使用尽可能少的处理器来维持负载。 此选项可帮助减少中断的数量。</p></td>
</tr>
</tbody>
</table>

 

NDIS 6.30 添加了对 **\*RSSProfile**。

以下列表显示[标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)rss 可编辑的：

<a href="" id="---------rssbaseprocgroup"></a> **\*RssBaseProcGroup**  
处理器组中指定的处理器数的数字 **\*RssBaseProcNumber**关键字。

<a href="" id="---------numanodeid"></a> **\*NumaNodeId**  
网络适配器的内存分配使用首选的 NUMA 节点。 此外，操作系统将尝试使用 RSS 首先从首选 NUMA 节点的 Cpu。

PCI 扩展卡的驱动程序不应指定 ID 以静态方式在其 INF，因为在最近的节点依赖于哪些 PCI 槽卡插入到 NUMA 节点。  仅指定 **\*NumaNodeId**如果网络适配器集成到系统，NUMA 节点事先已知的并不能通过查询 ACPI 在运行时确定的节点。

**请注意**  NDIS 如果存在此关键字，并且其值小于中计算机的 NUMA 节点数，使用中的此值**PreferredNumaNode**中的成员[ **NDIS\_RSS\_处理器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_rss_processor_info)结构。

 

**请注意**  在 Windows 8  **\*NumaNodeId**如果 NIC RSS 配置文件设置为忽略值**NUMAScaling**(2) 或**NUMAScalingStatic**(3)。

 

<a href="" id="---------rssbaseprocnumber"></a> **\*RssBaseProcNumber**  
指定的组中的基本 RSS 处理器数。

<a href="" id="---------maxrssprocessors"></a> **\*MaxRssProcessors**  
最大 RSS 处理器数。

<a href="" id="---------rssmaxprocnumber"></a> **\*RssMaxProcNumber**  
RSS 接口的最大处理器数。
如果 **\*RssMaxProcNumber**指定了，则 **\*RssMaxProcGroup**还应指定。

<a href="" id="---------rssmaxprocnumber"></a> **\*NumRSSQueues**  
RSS 队列数目。

<a href="" id="---------rssmaxprocgroup"></a> **\*RssMaxProcGroup** RSS 接口的最大处理器组。

**\*RssBaseProcGroup**连同 **\*RssBaseProcNumber**形成标识可用于 RSS 最小处理器数的 PROCESSOR_NUMBER 结构。
**\*RssMaxProcGroup**连同 **\*RssMaxProcNumber**形成标识可用于 RSS 的最大处理器数的 PROCESSOR_NUMBER 结构。

例如，假设 **\*RssBaseProcGroup**设置为 1，  **\*RssBaseProcNumber**设置为 16，  **\*RssMaxProcGroup**是设置为 3，并 **\*RssMaxProcNumber**设置为 8。
使用<group>:<processor>表示法，基处理器为 1:16 和最大处理器为 3:8。
然后处理器 0:0，0:32，1:0 和 1:15 不会被视为适合添加到 RSS，因为它们是以下基的处理器数。
处理器 1:16，1:31，2:0、 2:63，3:0 到 3:8 会被视为适合添加到 RSS，因为它们都不在范围 1:16 至 3:8。
处理器 3:9，3:31，4:0 将不会被视为候选项 rss，因为它们超出最大处理器数。

NDIS 6.20 添加了对 **\*RssBaseProcGroup**，  **\*NumaNodeId**，  **\*RssBaseProcNumber**，和 **\*MaxRssProcessors**关键字。

NDIS 6.30 添加了对 **\*RssMaxProcNumber**，和 **\*NumRSSQueues**关键字。

[标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)可以编辑具有以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须指定 INF 文件中的关键字的名称显示在注册表中。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

<a href="" id="type"></a>Type  
可编辑的值的类型。 值可以是数字 (Int) 或文本可编辑 （编辑）。

<a href="" id="default-value"></a>默认值  
整数或文本的默认值。 &lt;IHV 定义&gt;指示的值是与特定的独立硬件供应商 (IHV) 要求相关联。

<a href="" id="min"></a>最小值  
允许整数的最小值。 &lt;IHV 定义&gt;表示的最小值与特定的 IHV 要求相关联。

<a href="" id="max"></a>最大值  
允许整数的最大值。 &lt;IHV 定义&gt;表示的最小值与特定的 IHV 要求相关联。

下表介绍了所有可编辑的 RSS 关键字。

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
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">默认值</th>
<th align="left">最小</th>
<th align="left">最大</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcGroup</strong></p></td>
<td align="left"><p>RSS 基本处理器组</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>NumaNodeId</strong></p></td>
<td align="left"><p>首选的 NUMA 节点</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>65535 （任何节点）</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统而异-不能超过 65534</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssBaseProcNumber</strong></p></td>
<td align="left"><p>RSS 基的处理器数</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>MaxRssProcessors</strong></p></td>
<td align="left"><p>RSS 处理器最大数目</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>Windows Server 2008 的默认值：</p>
<p>8 1g 或速度较慢的适配器，16 个 10g 适配器</p>
<p>Windows 8 的默认值：</p>
<p>对于不带任何 MSI X 支持-2 个 1GbE 或速度较慢的适配器，4 表示 10 千兆以太网适配器的 Nic。</p>
<p>对于 MSI X 支持-4 1GbE 或速度较慢的适配器，16 个 10 GbE 适配器使用的 Nic。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_SYSTEM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>RssMaxProcNumber</strong></p></td>
<td align="left"><p>最大 RSS 处理器数</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1 （默认值）</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_PROC_PER_GROUP-1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>NumRSSQueues</strong></p></td>
<td align="left"><p>RSS 队列的最大数目</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>特定于设备</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>特定于设备</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*RSSMaxProcGroup</strong></p></td>
<td align="left"><p>RSS 最大处理器组</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MAXIMUM_GROUPS-1</p></td>
</tr>
</tbody>
</table>

 

**请注意**  虽然的有效范围 **\*RssBaseProcGroup**为零到最大值\_组 1，在 Windows 7 它必须为零。 否则，TCP/IP 协议不会将任何处理器用于 RSS。

 

**请注意**  的默认值为 **\*NumaNodeId** (65535) 表示的网络适配器是不可知的 NUMA 节点和 NDIS 不应尝试将首选的任何节点，而另一个。
如果 **\*NumaNodeId**关键字不存在，则 NDIS 会自动选择基于 ACPI 的提示在最近的节点。


有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

 

 





