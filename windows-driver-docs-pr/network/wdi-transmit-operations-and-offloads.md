---
title: WDI 传输操作和卸载
description: WDI 在两个 Tx 模式下的端口队列和 PeerTID 队列之一中运行。
ms.assetid: 9ADBDAD5-4AFA-4AFA-A829-96EB28CEBAA1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4af98ed7cd522ccbfa6af30248862c8fc3229a72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841715"
---
# <a name="wdi-transmit-operations-and-offloads"></a>WDI 传输操作和卸载


WDI 以两种 Tx 模式之一运行：端口队列和 PeerTID 队列。 目标设置具有 TargetPriorityQueueing 功能的模式（true = WDI 端口队列，false = WDI PeerTID 队列）。

宿主执行以下操作。

-   TX 分类（仅当**TargetPriorityQueueing** = false 时）
-   TX 队列（在端口级别或 PeerTID 级别）
-   传输计划（将帧下载到目标）
-   主机-目标 TX 流控制

下面是 TX 操作和卸载的列表。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">处理步骤</th>
<th align="left">描述</th>
<th align="left">所有者/适用的卸载</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>高级协议（任务）卸载</p></td>
<td align="left"><p>Checksum、LSO。</p></td>
<td align="left"><p>校验和是启动时可配置的卸载。 每个框架都有标志来指定适用的校验和操作。</p>
<p>如果适用，WDI 从 TAL/目标透明地处理 LSO 分段。</p></td>
<td align="left"><p>Checksum：目标会在 bringup 期间传递到 WDI 其校验和卸载功能作为设备 cap 的一部分。 有关功能信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_CHECKSUM_OFFLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)"><strong>NDIS_TCP_IP_CHECKSUM_OFFLOAD</strong></a>。</p>
<p>如果适用，WDI 从 TAL/目标透明地处理 LSO 分段。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TX encap</p></td>
<td align="left"><p>更新/将泛型802.11 标头替换为合适的802.11 帧标头类型。</p></td>
<td align="left"><p>Target/TAL</p></td>
<td align="left"><p>帧的第一个连续缓冲区包含可用空间（在 MAC 标头之前）。 此空间取决于设备参数中指定的 BackfillSize。</p>
<p>对于非 EAPOL 数据包，第一个缓冲区包含 MAC 和 LLC/SNAP 标头，但不包含有效负载。 EAPOL 数据包的第一个连续缓冲区可能包含有效负载的一部分（或全部）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TX 分类</p></td>
<td align="left"><p>确定 TID。 根据单播 RA 或 DA 确定接收方。</p></td>
<td align="left"><p>当<strong>TargetPriorityQueueing</strong>为 false 时，WDI 执行分类。 如果<strong>TargetPriorityQueueing</strong>为 true，则 WDI 不执行分类。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>TX 队列</p></td>
<td align="left"><p>将 TX 帧存储在单独的队列中。</p></td>
<td align="left"><p>如果需要，WDI 会将 TX 帧排队。</p></td>
<td align="left"><p>WDI 按端口（<strong>TargetPriorityQueueing</strong> = true）或按接收方和流量类型（PEERID，TID）（<strong>TargetPriorityQueueing</strong> = false）对帧进行 TX。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TX flow 控制</p></td>
<td align="left"><p>阻止 overrunning 和 TX 帧的等到或目标缓冲区。</p></td>
<td align="left"><p>WDI/等到/Target</p></td>
<td align="left"><p>请参阅 "主机-目标流控制" 部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>传输计划</p></td>
<td align="left"><p>如果有多个囤积队列，请选择要从中将帧传输到 TAL/等到的 TX 队列。</p></td>
<td align="left"><p>WDI 是否需要将 TX 帧排队。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>MSDU 聚合</p></td>
<td align="left"><p>确定要将哪些帧分组到 MSDU 聚合中，必须在重新传输过程中进行维护。</p></td>
<td align="left"><p>TAL/目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>碎片</p></td>
<td align="left"></td>
<td align="left"><p>TAL/目标</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>WLAN 计划</p></td>
<td align="left"><p>确定要向下传递哪个接收方、要发送的流量类型以及要发送的帧数。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>加密</p></td>
<td align="left"><p>使用为收件人（或发送方，为多播帧）指定的安全类型和安全密钥来加密帧内容。 在适用的情况下添加安全封装。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>对于支持 FIPS 的系统，可以在主机软件中进行加密。 目标的加密被绕过。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MPDU 聚合</p></td>
<td align="left"><p>确定要将哪些帧分组到 MPDU 聚合中，并可在重新传输过程中修改。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>后</p></td>
<td align="left"><p>接收方 nacked 或确认的重传 MPDUs。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="operation-in-host-implemented-fips-mode"></a>宿主实现的 FIPS 模式下的操作


如果主机为给定连接提供 FIPS （在[**WDI\_TLV\_连接\_设置**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connection-settings)）中，主机 FIPS 模式设置为 true，则主机会在将数据包提交到目标之前对其进行加密。 目标会传输数据包，而不会影响数据包的数据完整性的其他更改。 例如，目标不能在此模式下执行传输 MSDU 聚合。

在未启用 host FIPS 模式（目标实现的加密模式）的更常见情况下，标头802.11 标头后跟未加密的有效负载数据。 如果数据包在传输前需要加密，则目标将对数据包进行加密。 它还执行数据包的 QoS 优先级，并可能执行 TCP 层卸载操作（如校验和或大型发送）。 对于这种发送处理，目标可能需要将额外的标头添加到数据包（例如，QoS、HT 标头或 IV）。

## <a name="tx-encapsulation-population-of-80211-tx-frame-headers"></a>TX 封装：人口 802.11 TX 帧标题


以802.11 数据包格式将网络数据提交到端口（目标设备）。 每个传输的帧都以 802.11 MAC 标头开头。 主机设置 MAC 标头的某些字段，而目标则设置其他字段。 下表描述了由主机填充的 802.11 MAC 标头和密码标头的哪些字段，以及应由目标设备填充的字段。

<table>
<tr><th>字段名称</th><th>子字段名称</th><th colspan="2">目标实现的加密模式</th><th colspan="2">宿主实现的 FIPS 模式</th>
</tr>
    <tr><th></th><th></th><th>由主机设置</th><th>按目标设置</th><th>由主机设置</th><th>按目标设置</th></tr>
    <tr><td>框架控件</td><td>协议版本</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>框架控件</td><td>在任务栏的搜索框中键入</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>框架控件</td><td>类型</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>框架控件</td><td>到 DS</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>框架控件</td><td>从 DS</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>框架控件</td><td>更多片段</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>框架控件</td><td>后</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>框架控件</td><td>Pwr 管理</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>框架控件</td><td>更多数据</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>框架控件</td><td>受保护框架</td><td></td><td>X</td><td>X</td><td></td></tr>
    <tr><td>框架控件</td><td>顺序</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>持续时间/Id</td><td></td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>地址1</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>地址2</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>地址3</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>序列控件</td><td>片段号</td><td>X</td><td></td><td></td><td>X</td></tr>
    <tr><td>序列控件</td><td>序列号</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>地址4</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>QoS 控制</td><td></td><td></td><td>由目标添加/填充。</td><td></td><td>在 11n QoS 关联的情况下，按目标添加/填充。</td></tr>
    <tr><td>HT 控件</td><td></td><td></td><td>由目标添加/填充。</td><td></td><td>由目标添加/填充。</td></tr>
</table>

## <a name="related-topics"></a>相关主题


[**NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)

[WDI 数据传输](wdi-data-transfer.md)

[**WDI\_TLV\_连接\_设置**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connection-settings)

[**WDI\_TXRX\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_txrx_target_capabilities)

 

 






