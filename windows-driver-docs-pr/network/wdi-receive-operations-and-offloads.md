---
title: WDI 接收操作和卸载
description: 操作卸载这些主要类别是可配置。MSDU 级别接收 operationsFrame 转发 （转发决策和传动） 协议/任务卸载。
ms.assetid: 7D2648BC-05F2-4F75-BA01-E0385C83E0E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46e307638dcbfdd6648a801560c2eb1b3f86d62f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340925"
---
# <a name="wdi-receive-operations-and-offloads"></a>WDI 接收操作和卸载


操作卸载这些主要类别是可配置。

-   MSDU 级别接收操作
-   帧转发 （转发决策和传动）
-   协议/任务卸载

下面是 RX 操作和卸载的列表。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
<th align="left">所有权</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>解密</p></td>
<td align="left"><p>框架内容使用的安全类型和指定的发件人的安全密钥进行解密。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>在宿主实现 FIPS 模式下，该主机软件中完成解密。 目标的解密，则跳过。</p></td>
</tr>
<tr class="even">
<td align="left"><p>一个 MPDU deaggregation</p></td>
<td align="left"><p>将 RX A MPDU 分解为各个 MPDUs。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>一个 MSDU deaggregation</p></td>
<td align="left"><p>将 RX A MSDU 分解为各个 MSDUs。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"><p>每个 RX MSDU 放入单独的缓冲区中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MSDU 安全 decap 和 de MIC</p></td>
<td align="left"><p>对于涉及 MSDU 级别 MIC 的安全类型，验证收到的 MIC。 解封以下安全标头和页脚。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"><p>如果需要操作系统执行的对策。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx decap</p></td>
<td align="left"><p>将替换 802.11 标头，根据需要使用从初始的 MSDU subframe 802.11 标头字段为非初始 A MSDU subframe 标头。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"><p>在一个 MSDU deaggregation A MSDU 非初始 MSDUs 需要泛型 802.11 报头替换为其 802.3 标头。 WDI 始终需要 802.11 标头。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Rx 重新排序逻辑</p></td>
<td align="left"><p>对于每个 RX MPDU，确定重新排序数组的 Rx 的槽它转到。 确定何时存在一系列按顺序帧。 确定何时发布挂起的帧，即使未到达其前面的帧。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx 放弃逻辑</p></td>
<td align="left"><p>确定要放弃哪些 Rx 帧需要：</p>
<ol>
<li>如果它与任何接收数据包筛选器都不匹配。</li>
<li>如果帧进行加密，如果放弃：
<ul>
<li>密码密钥不可用来解密数据包。</li>
<li>无法成功解密数据包有效负载。</li>
<li>在数据包有效负载的 MIC 验证将失败。</li>
<li>数据包失败定义密码算法的重播机制 （请参阅 Rx PN/重播检查）。</li>
<li>为指定的数据包的这些类型定义隐私例外<strong>WDI_EXEMPT_ 始终</strong>操作。</li>
</ul></li>
<li>如果框架的未加密，如果放弃：
<ul>
<li>加密密钥是可用于解密数据包，隐私例外定义为指定的数据包的 Ethertype <strong>WDI_EXEMPT_ON_ KEY_UNAVAILABLE</strong>操作。</li>
<li>Dot11ExcludeUnencrypted MIB 设置为 true。</li>
</ul></li>
</ol></td>
<td align="left"><p>所有的目标/谈论可放弃的决策。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx PN/重播检查</p></td>
<td align="left"><p>确认每个 MPDU 具有不同的数据包数字大于先前的 PNs。</p></td>
<td align="left"><p>这是除重新排序队列与关联的流强制和始终启用卸载并重新排序队列管理未完全卸载到目标。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Chatter 卸载</p></td>
<td align="left"><p>避免中断每个可以推迟"噪声"Rx 帧的主机。 相反，组 Rx 干扰帧并使用单个中断提供所有此类框架。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>碎片整理</p></td>
<td align="left"><p>重组到其原始 MSDU 802.11 片段。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx 重新排序队列</p></td>
<td align="left"><p>存储顺序颠倒 Rx MPDUs，直到从流缺少以前 MPDUs 到达。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx 放弃时闭合</p></td>
<td align="left"><p>放弃 Rx 帧基于在目标上运行的 Rx 放弃逻辑被标记的规范。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>更高级别的协议 （任务） 卸载</p></td>
<td align="left"><p>校验和</p></td>
<td align="left"><p>校验和：启动时如果所需的可配置卸载。</p></td>
<td align="left"><p>校验和：目标将传递其校验和卸载功能的设备 caps 设一部分到 WDI 在启动过程。 有关功能的信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff567878" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_ CHECKSUM_OFFLOAD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567878)"> <strong>NDIS_TCP_IP_ CHECKSUM_OFFLOAD</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="receive-operations-in-host-implemented-fips-mode"></a>在 Host-Implemented FIPS 模式下接收操作


在此模式下，目标可能指示使用 802.11 报头或 802.3 标头接收的帧。 指示之前必须解密该框架。

如果丢弃逻辑卸载到目标，它必须满足以下条件的任何标记接收到丢弃的帧。

-   具有错误的 CRC 的帧。
-   重复的帧。
-   与配置的数据包筛选器不匹配的帧。

目标必须递增成功接收或由端口被丢弃的数据包的适当 MAC 和物理统计信息。

此外，如果卸载目标必须执行丢弃时闭合。

在宿主实现 FIPS 模式下操作时，目标不应 RX 路径上去除 802.11 标头中的 QoS 标志。 目标应指示帧，而无需修改 QoS 标头。

零碎的数据包的情况下，负载类型报告的 LE FIPS 模式下将始终**WDI\_帧\_MSDU\_片段**主机是进行碎片整理过程。 但是，在非 FIPS 模式下，报告的负载类型应该**WDI\_帧\_MSDU**目标/谈论是执行碎片整理。

## <a name="related-topics"></a>相关主题


[**NDIS\_TCP\_IP\_校验和\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567878)

[WDI 数据传输](wdi-data-transfer.md)

[**WDI\_免除\_操作\_类型**](https://msdn.microsoft.com/library/windows/hardware/dn897820)

[**WDI\_帧\_负载\_类型**](https://msdn.microsoft.com/library/windows/hardware/dn897831)

 

 






