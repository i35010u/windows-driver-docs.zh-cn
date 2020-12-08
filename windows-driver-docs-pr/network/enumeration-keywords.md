---
title: 枚举关键字
description: 枚举关键字
keywords:
- 安装关键字 WDK 网络，枚举关键字
- 枚举关键字 WDK NDIS 小型端口
ms.date: 4/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0fef4d7aeda6e036f0c45e45b68005646dfe2a0c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788457"
---
# <a name="enumeration-keywords"></a>枚举关键字

Ndis 6.0 和更高版本的 NDIS 为网络设备的微型端口驱动程序提供标准化的枚举关键字。 枚举关键字与显示为菜单中的列表的值相关联。

下面的示例演示了枚举关键字的 INF 文件定义。

```INF
HKR, Ndi\params\<SubkeyName>, ParamDesc, 0, "%<SubkeyName>%"
HKR, Ndi\params\<SubkeyName>, Type, 0, "enum"
HKR, Ndi\params\<SubkeyName>, Default, 0, "3"
HKR, Ndi\params\<SubkeyName>, Optional, 0, "0"
HKR, Ndi\params\<SubkeyName>\enum, "0", 0, "%Disabled%"
HKR, Ndi\params\<SubkeyName>\enum, "1", 0, "%Tx Enabled%"
HKR, Ndi\params\<SubkeyName>\enum, "2", 0, "%Rx Enabled%"
HKR, Ndi\params\<SubkeyName>\enum, "3", 0, "%Rx & Tx Enabled%"
```

一般的枚举关键字包括：

<a href="" id="-speedduplex"></a>**\*SpeedDuplex**  
设备支持的速度和双工设置。 设备 INF 文件应仅列出关联设备支持的设置。 也就是说，对于只能支持全双工模式的以太网10/100 设备，不应在关联的 INF 文件中列出千兆位或更高的速度或半双工的设置。

对于未明确定义的值，值为0到10的枚举值可能设置为值，该值是直接以 Mbps 为单位的值。  直接值必须至少为 1000 Mbps (1 Gbps) 和更高版本。  下面是用于直接指定速度的几个示例：

| SpeedDuplex 值 | 最终速度 |
| ---| ---|
| 1,000 | 1 Gbps |
| 10,000 | 10 Gbps |
| 25,000 | 25 Gbps |
| 50,000 | 50 Gbps |
| 100,000 | 100 Gbps |

<a href="" id="-flowcontrol"></a>**\*FlowControl**  
设备在发送或接收路径中启用或禁用流控制的能力。

**注意**  
现在，以太网设备支持流控制，默认情况下，适用于 LAN 的 Windows 8 内置驱动程序已启用流控制。 当内核调试器附加到其中一个 LAN 适配器时，NIC 将开始将流控制暂停帧推送到网络。 大多数网络交换机会通过暂时关闭连接到同一集线器的所有其他计算机的网络来做出反应。 这是一种常见的开发方案，最终用户体验既不需要也不难诊断。

**注意**  
客户端和服务器默认值不相同;请参阅下面的默认值表。

出于此原因，在 Windows 8 及更高版本中，当在计算机上启用调试时，NDIS 将自动禁用 flow 控制 (例如，通过在命令行) 键入 **bcdedit/set debug** 。 当启用内核调试并且微型端口调用 [**NdisReadConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration) 并 \* 为 *关键字* 参数传递 "FlowControl" 时，NDIS 将重写配置的值并返回零。

如果需要在调试时启用流控制，NDIS 会提供 **AllowFlowControlUnderDebugger** 注册表值，以允许执行此操作。 **AllowFlowControlUnderDebugger** 注册表值可防止 NDIS 禁用流控制，并允许 nic 保留其配置的行为。 它可在以下注册表项下找到：

**HKEY \_本地 \_ 计算机** \\ **系统** \\ **CurrentControlSet** \\ **服务** \\ **NDIS** \\ **参数**

将此注册表值设置为0x00000001。

如果该名称不存在，你可以创建一个名为 **AllowFlowControlUnderDebugger** 、类型为 **REG \_ DWORD** 的值并将其设置为0x00000001。

<a href="" id="-priorityvlantag"></a>**\*PriorityVLANTag**  
一个值，该值指示设备是否已启用或禁用为数据包优先级和虚拟 Lan (Vlan) 插入 802.1 Q 标记的功能。 此关键字不表明设备启用或禁用数据包优先级或 VLAN 标记。 相反，它描述了以下内容：

- 在发送操作过程中，设备是否插入 802.1 Q 标记
- [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中是否有 802.1 q 标记信息（带外 (OOB) 信息）
- 设备在接收操作期间是否将 802.1 Q 标记复制到 OOB

无论 **\* PriorityVLANTag** 设置如何，微型端口驱动程序都应从所有接收数据包中删除 802.1 q 标头。 如果 802.1 Q 标头保留在包中，则其他驱动程序可能无法正确分析数据包。

如果在接收路径上启用 Rx 标志，则微型端口驱动程序应将删除的 802.1 Q 标头复制到 OOB。

否则，如果 Rx 标志被禁用，微型端口驱动程序不应将删除的 802.1 Q 标头复制到 OOB。

如果在传输路径上启用了 Tx 标志，则微型端口驱动程序应执行以下操作：

- 将 802.1 Q 标头插入到每个传出数据包中，并用 OOB (中的数据填充该标头（如果 OOB) 中存在任何非零数据）。
- 在 [**ndis 微型端口适配器中播发适当的 MacOptions \_ \_ \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes) (**NDIS \_ mac \_ 选项 \_ 8021P \_ 优先级** 和 **NDIS \_ mac \_ 选项 \_ 8021Q \_ VLAN**) 。 **MacOptions**

否则，如果禁用 Tx 标志，则：

- 小型小型筛选器不应遵循 OOB (中的 802.1 Q 信息，因此不会插入任何标记) 。
- 小型小型筛选器不应在 [**NDIS \_ 微型端口 \_ 适配器的 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)中公布适当的 **MacOptions** 。

**注意** 如果微型端口驱动程序支持 NDIS 服务 (QoS) ，则它还必须读取 **\* qos** 关键字值。 根据 **\* QOS** 关键字值， **\* PriorityVLANTag** 关键字值的解释方式有所不同。 有关详细信息，请参阅 [NDIS QoS 的标准化 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)。

 <a href="" id="-interruptmoderation"></a>**\*InterruptModeration**  
一个值，该值描述设备启用还是禁用中断裁决。 中断裁决算法依赖于设备。 设备制造商可以使用非标准化关键字来支持算法设置。 有关中断裁决的详细信息，请参阅 [中断裁决](interrupt-moderation.md)。

<a href="" id="-rss"></a>**\*技术**  
一个值，该值描述设备是否启用或禁用接收方缩放 (RSS) 。 有关 RSS 的详细信息，请参阅 [接收方缩放](./receive-side-scaling-version-2-rssv2-.md)。

<a href="" id="-headerdatasplit"></a>**\*HeaderDataSplit**  
一个值，该值描述是启用还是禁用了设备标头-数据拆分。 有关标头-数据拆分的详细信息，请参阅 [标头-数据拆分](header-data-split.md)。

以下关键字与连接卸载服务相关联：

**\*TCPConnectionOffloadIPv4**

**\*TCPConnectionOffloadIPv6**

有关连接卸载关键字的详细信息，请参阅 [使用注册表值启用和禁用连接卸载](using-registry-values-to-enable-and-disable-connection-offloading.md)。

以下关键字与任务卸载服务相关联：

**\*IPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv6**

**\*UDPChecksumOffloadIPv4**

**\*UDPChecksumOffloadIPv6**

**\*LsoV1IPv4**

**\*LsoV2IPv4**

**注意** 对于同时支持大型发送卸载版本 1 (LSOv1) 和 IPv4 上的 LSOv2 的设备，在 INF 文件和注册表值中只应使用 **\* LsoV2IPv4** 关键字。 例如，如果 **\* LsoV2IPv4** 关键字显示在 INF 文件中，并且 **\* LsoV1IPv4** 关键字显示在注册表 (中，反之亦然) ，则 **\* LsoV2IPv4** 关键字始终优先。

 **\*LsoV2IPv6**

**\*IPsecOffloadV1IPv4**

**\*IPsecOffloadV2**

**\*IPsecOffloadV2IPv4**

**\*TCPUDPChecksumOffloadIPv4**

**\*TCPUDPChecksumOffloadIPv6**

有关 TCP/IP 卸载关键字的详细信息，请参阅 [使用注册表值启用和禁用任务卸载](using-registry-values-to-enable-and-disable-task-offloading.md)。

本主题末尾的表中的列描述了用于枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定并且出现在注册表中的关键字的名称。

<a href="" id="paramdesc"></a>ParamDesc  
与 **SubkeyName** 关联的显示文本。

<a href="" id="value"></a>“值”  
与列表中的每个选项关联的枚举整数值。 此值存储在 **NDI \\ params \\**<em>SubkeyName</em> **\\** <em>值</em>中。

<a href="" id="enumdesc"></a>EnumDesc  
与菜单中显示的每个值相关联的显示文本。

<a href="" id="default"></a>默认  
菜单的默认值。

下表列出了所有关键字，并说明了驱动程序必须用于前面的特性的值。 有关关键字的详细信息，请在 WDK 文档中搜索关键字。

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
<th align="left">“值”</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>SpeedDuplex</strong></p></td>
<td align="left"><p>速度 & 双工</p></td>
<td align="left"><p>0（默认值）</p></td>
<td align="left"><p>自动协商</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10 Mbps 半双工</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10 Mbps 全双工</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p>100 Mbps 半双工</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>100 Mbps 全双工</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1.0 Gbps 半双工</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>6</p></td>
<td align="left"><p>1.0 Gbps 全双工</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>7</p></td>
<td align="left"><p>10 Gbps 全双工</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>8</p></td>
<td align="left"><p>20 Gbps 全双工</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>9</p></td>
<td align="left"><p>40 Gbps 全双工</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>10</p></td>
<td align="left"><p>100 Gbps 全双工</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>FlowControl</strong></p></td>
<td align="left"><p>流控制</p></td>
<td align="left"><p>0 (服务器默认值) </p></td>
<td align="left"><p>已禁用 Tx & Rx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (客户端默认) </p></td>
<td align="left"><p>Rx & Tx 已启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>自动协商</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>PriorityVLANTag</strong></p></td>
<td align="left"><p>数据包优先级 & VLAN</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>禁用了包优先级 & VLAN</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用数据包优先级</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 VLAN</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>启用了包优先级 & VLAN</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>InterruptModeration</strong></p></td>
<td align="left"><p>中断调解</p></td>
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
<td align="left"><p><strong></em>HeaderDataSplit</strong></p></td>
<td align="left"><p>标头数据拆分</p></td>
<td align="left"><p>0（默认值）</p></td>
<td align="left"><p>禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPConnectionOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 连接卸载 (IPv4) </p></td>
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
<td align="left"><p><strong></em>TCPConnectionOffloadIPv6</strong></p></td>
<td align="left"><p> (IPv6) 的 TCP 连接卸载</p></td>
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
<td align="left"><p><strong><em>IPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>IPv4 校验和卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>Rx & Tx 已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 校验和卸载 (IPv4) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>Rx & Tx 已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 校验和卸载 (IPv6) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>Rx & Tx 已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>UDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>UDP 校验和卸载 (IPv4) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>Rx & Tx 已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>UDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>UDP 校验和卸载 (IPv6) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>Rx & Tx 已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV1IPv4</strong></p></td>
<td align="left"><p>大型发送卸载版本 1 (IPv4) </p></td>
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
<td align="left"><p><strong><em>LsoV2IPv4</strong></p></td>
<td align="left"><p>大型发送卸载版本 2 (IPv4) </p></td>
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
<td align="left"><p><strong></em>LsoV2IPv6</strong></p></td>
<td align="left"><p>大型发送卸载版本 2 (IPv6) </p></td>
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
<td align="left"><p><strong><em>IPsecOffloadV1IPv4</strong></p></td>
<td align="left"><p>IPsec 卸载版本 1 (IPv4) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>身份验证标头已启用 & ESP</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>IPsecOffloadV2</strong></p></td>
<td align="left"><p>IPsec 卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>身份验证标头已启用 & ESP</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPsecOffloadV2IPv4</strong></p></td>
<td align="left"><p>IPsec 卸载 (仅 IPv4) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>身份验证标头已启用 & ESP</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPUDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP/UDP 校验和卸载 (IPv4) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>已启用 Tx 和 Rx</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*TCPUDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP/UDP 校验和卸载 (IPv6) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用 Tx</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 Rx</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>已启用 Tx 和 Rx</p></td>
</tr>
</tbody>
</table>
