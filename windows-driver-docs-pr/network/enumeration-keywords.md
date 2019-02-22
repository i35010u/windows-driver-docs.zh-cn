---
title: 枚举关键字
description: 枚举关键字
ms.assetid: ac1fb871-7720-4497-b9f7-8f592fe19bd0
keywords:
- 安装关键字 WDK 网络，枚举关键字
- 枚举关键字 WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c76f4d1b82064fc51958ba96f0d62d4156eb416
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525835"
---
# <a name="enumeration-keywords"></a>枚举关键字





NDIS 6.0 和更高版本的 NDIS 网络设备的微型端口驱动程序提供标准化的枚举关键字。 枚举关键字是显示为菜单中的列表的值与相关联。

下面的示例显示了枚举关键字的 INF 文件定义。

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

常规枚举关键字是：

<a href="" id="-speedduplex"></a>**\*SpeedDuplex**  
速度和双工设备支持的设置。 设备 INF 文件应列出关联的设备支持的设置。 也就是说，如果对于以太网 10/100 设备可支持仅全双工模式下，，关联的 INF 文件中应不会列出千兆或更高的速度或半双工设置。

已使用 0 到 10 的枚举值不专门定义速度值可能设置为直接以 mbps 为单位的值的数字。  指示值必须至少为 1,000 Mbps (1 Gbps) 及更高版本。  下面是用于直接指定速度的几个示例：

| SpeedDuplex 值 | 生成的速度 |
| ---| ---|
| 1,000 | 1 Gbps |
| 10,000 | 10 Gbps |
| 25,000 | 25 Gbps |
| 50,000 | 50 Gbps |
| 100,000 | 100 Gbps |

<a href="" id="-flowcontrol"></a>**\*FlowControl**  
控制在发送或接收路径为设备启用或禁用流的功能。

**请注意**  以太网设备现在支持流控制和 LAN 的 Windows 8 内置驱动程序具有默认情况下启用的流控制。 当内核调试程序附加到这些 LAN 适配器之一时，NIC 将开始将流控制暂停帧推送到网络。 大多数网络交换机将通过暂时关闭的所有其他计算机连接到相同的中心的网络响应。 这是常见开发方案中，并且最终用户体验是不必要和难以进行诊断。

出于此原因，在 Windows 8 和更高版本，NDIS 将禁用流控制，自动在计算机上启用调试时 (例如，通过键入**bcdedit /set 上进行调试**在命令行)。 当启用内核调试和微型端口调用[ **NdisReadConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff564511) ，并将传递"\*FlowControl"对于*关键字*参数，NDIS 将重写的配置的值并返回零。

如果您需要调试时启用流控制，提供了 NDIS **AllowFlowControlUnderDebugger**注册表值以允许您执行该操作。 **AllowFlowControlUnderDebugger**注册表值阻止 NDIS 禁用流控制，并允许 Nic 来保持其已配置的行为。 它可以找到以下注册表项下：

**HKEY\_LOCAL\_MACHINE**\\**System**\\**CurrentControlSet**\\**Services**\\**NDIS**\\**Parameters**

将此注册表值设置为 0x00000001。

如果不存在，则可以创建值具有名称**AllowFlowControlUnderDebugger**和类型**REG\_DWORD**并将其设置为 0x00000001。

 

<a href="" id="-priorityvlantag"></a>**\*PriorityVLANTag**  
一个值，指示设备是否已启用或禁用插入 802.1Q 标记数据包优先级和虚拟 Lan (Vlan)。 此关键字不指示设备是启用还是禁用数据包优先级或 VLAN 标记。 相反，它介绍了以下任务：

-   设备是否插入 802.1Q 标记发送操作期间
-   是否 802.1Q 标记信息现已推出[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)带外 (OOB) 的信息
-   设备副本 802.1Q 标记到 OOB 期间是否接收操作

微型端口驱动程序应删除 802.1Q 中所有标头接收数据包而不考虑 **\*PriorityVLANTag**设置。 如果 802.1Q 标头会保留在一个数据包、 其他驱动程序可能无法正确分析数据包。

如果接收路径上启用了 Rx 标志，微型端口驱动程序应将复制已删除的 802.1Q 到 OOB 标头。

否则，如果禁用 Rx 标志，则微型端口驱动程序到 OOB 应不复制删除 802.1Q 标头。

如果传输路径上启用了 Tx 标志，微型端口驱动程序应执行以下操作：

-   插入 802.1Q 标头到每个传出数据包，并填充 OOB 中的数据 （如果 OOB 中存在任何非零值数据）。
-   播发适当**MacOptions**中[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923) (**NDIS\_MAC\_选项\_8021 P\_优先级**并**NDIS\_MAC\_选项\_8021Q\_VLAN**)。

否则为如果禁用 Tx 标志，然后：

-   微型端口筛选器不应接受 802.1Q OOB 中的信息 （并因此不插入任何标记）。
-   微型端口筛选器不应将播发适当**MacOptions**中[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923).

**请注意**  如果微型端口驱动程序支持 NDIS 服务质量 (QoS)，它还必须读取 **\*QOS**关键字值。 基于 **\*QOS**关键字值 **\*PriorityVLANTag**关键字值将以不同的方式解释。 有关详细信息，请参阅[NDIS QoS 的标准化 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)。

 

<a href="" id="-interruptmoderation"></a>**\*InterruptModeration**  
一个值，描述该设备是启用还是禁用中断裁决。 中断裁决算法是依赖于设备的。 设备制造商可以使用非标准化的关键字来支持算法设置。 有关中断裁决的详细信息，请参阅[中断裁决](interrupt-moderation.md)。

<a href="" id="-rss"></a>**\*RSS**  
一个值，描述该设备是启用还是禁用接收方缩放 (RSS)。 有关 RSS 的详细信息，请参阅[接收方伸缩](ndis-receive-side-scaling2.md)。

<a href="" id="-headerdatasplit"></a>**\*HeaderDataSplit**  
一个值，描述该设备是启用还是禁用标头数据拆分。 标头数据拆分的详细信息，请参阅[标头数据拆分](header-data-split.md)。

以下关键字是与连接卸载服务相关联：

**\*TCPConnectionOffloadIPv4**

**\*TCPConnectionOffloadIPv6**

有关连接卸载关键字的详细信息，请参阅[使用注册表值，以启用和禁用连接卸载](using-registry-values-to-enable-and-disable-connection-offloading.md)。

以下关键字是任务卸载服务与相关联：

**\*IPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv4**

**\*TCPChecksumOffloadIPv6**

**\*UDPChecksumOffloadIPv4**

**\*UDPChecksumOffloadIPv6**

**\*LsoV1IPv4**

**\*LsoV2IPv4**

**请注意**  设备的支持这两个大型发送卸载版本 1 (LSOv1) 和通过仅 IPv4 LSOv2  **\*LsoV2IPv4**应 INF 文件和注册表值中使用关键字。 例如，如果 **\*LsoV2IPv4**关键字出现在 INF 文件中并 **\*LsoV1IPv4**关键字出现在注册表中 （或相反），  **\*LsoV2IPv4**关键字始终优先。

 

**\*LsoV2IPv6**

**\*IPsecOffloadV1IPv4**

**\*IPsecOffloadV2**

**\*IPsecOffloadV2IPv4**

**\*TCPUDPChecksumOffloadIPv4**

**\*TCPUDPChecksumOffloadIPv6**

有关 TCP/IP 卸载关键字的详细信息，请参阅[使用注册表值，以启用和禁用任务卸载](using-registry-values-to-enable-and-disable-task-offloading.md)。

本主题末尾处表中的列描述枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须指定 INF 文件中的关键字的名称显示在注册表中。

<a href="" id="paramdesc"></a>ParamDesc  
与之关联的显示文本**SubkeyName**。

<a href="" id="value"></a>值  
在列表中每个选项与关联枚举的整数值。 此值存储在**NDI\\params\\**<em>SubkeyName</em>**\\**<em>值</em>。

<a href="" id="enumdesc"></a>EnumDesc  
与每个菜单中显示的值相关联的显示文本。

<a href="" id="default"></a>默认值  
菜单默认值。

下表列出的所有关键字，并说明了一个驱动程序必须用于对上述属性的值。 有关关键字的详细信息，搜索 WDK 文档中的关键字。

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
<td align="left"><p><strong><em>SpeedDuplex</strong></p></td>
<td align="left"><p>速度&amp;双工</p></td>
<td align="left"><p>0 （默认值）</p></td>
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
<td align="left"><p>100 Mbps Half Duplex</p></td>
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
<td align="left"><p>1.0 Gbps Half Duplex</p></td>
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
<td align="left"><p>为 20 Gbps 全双工</p></td>
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
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>自动协商</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>PriorityVLANTag</strong></p></td>
<td align="left"><p>数据包优先级&amp;VLAN</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>数据包优先级&amp;VLAN 已禁用</p></td>
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
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>数据包优先级&amp;已启用 VLAN</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>InterruptModeration</strong></p></td>
<td align="left"><p>中断裁决</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
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
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>HeaderDataSplit</strong></p></td>
<td align="left"><p>标头数据拆分</p></td>
<td align="left"><p>0 （默认值）</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPConnectionOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 连接卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPConnectionOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 连接卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>IPv4 校验和卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 校验和卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 校验和卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>UDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>UDP 校验和卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>UDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>UDP 校验和卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV1IPv4</strong></p></td>
<td align="left"><p>大量发送卸载版本 1 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>LsoV2IPv4</strong></p></td>
<td align="left"><p>大量发送卸载版本 2 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV2IPv6</strong></p></td>
<td align="left"><p>大量发送卸载版本 2 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPsecOffloadV1IPv4</strong></p></td>
<td align="left"><p>IPsec 卸载版本 1 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用的 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>身份验证标头&amp;ESP 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>IPsecOffloadV2</strong></p></td>
<td align="left"><p>IPsec 卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用的 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>身份验证标头&amp;ESP 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPsecOffloadV2IPv4</strong></p></td>
<td align="left"><p>IPsec 卸载 (仅 IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用的 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>身份验证标头&amp;ESP 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPUDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP/UDP 校验和卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Tx 和 Rx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*TCPUDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP/UDP 校验和卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Tx 和 Rx 启用</p></td>
</tr>
</tbody>
</table>

 

 

 





