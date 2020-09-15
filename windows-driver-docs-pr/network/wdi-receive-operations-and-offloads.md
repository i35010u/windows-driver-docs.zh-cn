---
title: WDI 接收操作和卸载
description: 操作卸载的主要类别是可配置的。MSDU operationsFrame 转发 (转发决策和传动) 协议/任务卸载。
ms.assetid: 7D2648BC-05F2-4F75-BA01-E0385C83E0E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe9f633734f7e770a5a3ce94db71ff9ae1fbf21
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102414"
---
# <a name="wdi-receive-operations-and-offloads"></a>WDI 接收操作和卸载


操作卸载的主要类别是可配置的。

-   MSDU 级别接收操作
-   帧转发 (转发决策和传动) 
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
<th align="left">说明</th>
<th align="left">所有权</th>
<th align="left">备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>解密</p></td>
<td align="left"><p>使用为发送方指定的安全类型和安全密钥来解密帧内容。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>在主机实现的 FIPS 模式下，解密是在主机软件中完成的。 目标的解密被绕过。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MPDU deaggregation</p></td>
<td align="left"><p>将 RX MPDU 分解为单个 MPDUs。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>MSDU deaggregation</p></td>
<td align="left"><p>将 RX MSDU 分解为单个 MSDUs。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"><p>每个 RX MSDU 都放置在单独的缓冲区中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MSDU Security decap and 反麦克风</p></td>
<td align="left"><p>对于涉及 MSDU 级 MIC 的安全类型，请验证收到的 MIC。 解封以下安全标头和表尾。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"><p>操作系统会根据需要执行对策。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx decap</p></td>
<td align="left"><p>根据需要，使用初始 MSDU subframe 中的802.11 标头字段将非初始 MSDU subframe 标头替换为802.11 标头。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"><p>在 MSDU deaggregation 过程中，MSDU 的非初始 MSDUs 需要将802.3 标头替换为通用802.11 标头。 WDI 始终需要802.11 标头。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Rx 重新排序逻辑</p></td>
<td align="left"><p>对于每个 RX MPDU，确定它所转到的 Rx 重新排序数组的槽。 确定存在一系列按序的帧的时间。 确定何时释放挂起帧（即使它们前面的帧尚未到达）。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx 丢弃逻辑</p></td>
<td align="left"><p>确定需要丢弃的 Rx 帧：</p>
<ol>
<li>如果它与任何接收数据包筛选器都不匹配，则为。</li>
<li>如果帧已加密，请在以下情况下丢弃：
<ul>
<li>密码密钥不可用于解密数据包。</li>
<li>数据包有效负载未能成功解密。</li>
<li>数据包有效负载无法通过 MIC 验证。</li>
<li>该数据包无法找到为密码算法定义的重播机制 (请参阅 Rx PN/replay 检查) 。</li>
<li>为数据包的网类型定义隐私例外，该类型指定 <strong>WDI_EXEMPT_ 始终</strong> 操作。</li>
</ul></li>
<li>如果未加密帧，则丢弃：
<ul>
<li>加密密钥可用于解密数据包，并为数据包的 Ethertype 定义了一个隐私例外，用于指定 <strong>WDI_EXEMPT_ON_ KEY_UNAVAILABLE</strong> 操作。</li>
<li>Dot11ExcludeUnencrypted MIB 设置为 true。</li>
</ul></li>
</ol></td>
<td align="left"><p>Target/TAL 做出所有放弃决定。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx PN/replay 检查</p></td>
<td align="left"><p>确认每个 MPDU 都有一个大于先前 PNs 的不同数据包号。</p></td>
<td align="left"><p>这是一个必需且始终启用的卸载，但与重新排序队列关联的流除外，而且不会完全脱离目标队列管理。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Chatter 卸载</p></td>
<td align="left"><p>避免中断每个延迟的 "噪声" Rx 帧的主机。 相反，将 Rx 干扰帧分组并使用单个中断来提供所有此类帧。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>碎片</p></td>
<td align="left"><p>将802.11 碎片重组为其原始 MSDU。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>Rx 重新排序队列</p></td>
<td align="left"><p>在流到达之前，存储有序 Rx MPDUs，直到丢失之前的 MPDUs。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>Rx 丢弃传动</p></td>
<td align="left"><p>根据 Rx 丢弃逻辑标记的规范（在目标上运行）丢弃 Rx 帧。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>高级协议 (任务) 卸载</p></td>
<td align="left"><p>校验和</p></td>
<td align="left"><p>Checksum：在启动时可配置的卸载（如果需要）。</p></td>
<td align="left"><p>校验和：在启动过程中，目标会将其校验和卸载功能作为设备 cap 的一部分传递到 WDI。 有关功能的信息，请参阅 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_ CHECKSUM_OFFLOAD&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)"><strong>NDIS_TCP_IP_ CHECKSUM_OFFLOAD</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="receive-operations-in-host-implemented-fips-mode"></a>宿主实现的 FIPS 模式下的接收操作


在此模式下，目标可能会指示收到的帧具有802.11 标头或802.3 标头。 在指示之前，不能对帧进行解密。

如果放弃逻辑被卸载到目标，则必须将接收的帧标记为在满足以下任一条件时丢弃。

-   具有错误 CRC 的帧。
-   重复的帧。
-   与配置的数据包筛选器不匹配的帧。

目标必须为该端口成功接收或丢弃的数据包增加适当的 MAC 和 PHY 统计信息。

此外，如果已卸载，则目标必须执行弃用传动。

在主机实现的 FIPS 模式下操作时，目标不应从 RX 路径上的802.11 标头中去除 QoS 标志。 目标应指示帧，而不修改 QoS 标头。

对于零碎的数据包，由 LE 为 FIPS 模式报告的负载类型总是 **WDI \_ 帧 \_ MSDU \_ 片段** ，因为主机正在执行碎片整理过程。 但是，在非 FIPS 模式下，报告的负载类型应为 **WDI \_ 帧 \_ MSDU** ，因为目标/TAL 正在执行碎片整理。

## <a name="related-topics"></a>相关主题


[**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)

[WDI 数据传输](wdi-data-transfer.md)

[**WDI \_ 豁免 \_ 操作 \_ 类型**](/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_exemption_action_type)

[**WDI \_ 帧 \_ 负载 \_ 类型**](/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_frame_payload_type)

