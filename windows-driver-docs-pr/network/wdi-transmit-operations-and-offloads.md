---
title: WDI 传输操作和卸载
description: WDI 中两个 Tx 模式端口队列和 PeerTID 队列之一进行操作。
ms.assetid: 9ADBDAD5-4AFA-4AFA-A829-96EB28CEBAA1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d215fbc9906b339d82d4d734636fb0472eed49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342904"
---
# <a name="wdi-transmit-operations-and-offloads"></a>WDI 传输操作和卸载


WDI 在两种 Tx 模式之一运行：端口队列和 PeerTID 队列。 目标设置具有 TargetPriorityQueueing 功能模式 （true = WDI 端口队列，false = WDI PeerTID 队列）。

宿主执行以下操作。

-   TX 分类 (仅当**TargetPriorityQueueing** = false)
-   TX 队列 （无论在端口级别或 PeerTID 级别）
-   传输计划 （计划到目标帧下载）
-   主机目标 TX 流控制

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
<th align="left">适用于所有者/卸载</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>高级别协议 （任务） 卸载</p></td>
<td align="left"><p>校验和，LSO。</p></td>
<td align="left"><p>校验和是启动时可配置卸载。 每个框架都有标志以指定适用的校验和操作。</p>
<p>如果适用，WDI 处理 LSO 分段以透明方式从谈论/目标。</p></td>
<td align="left"><p>校验和：目标将传递到 WDI 其校验和卸载功能的设备 caps 设一部分 bringup 期间。 有关功能的信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff567878" data-raw-source="[&lt;strong&gt;NDIS_TCP_IP_CHECKSUM_OFFLOAD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567878)"> <strong>NDIS_TCP_IP_CHECKSUM_OFFLOAD</strong></a>。</p>
<p>如果适用，WDI 处理 LSO 分段以透明方式从谈论/目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TX 封闭</p></td>
<td align="left"><p>更新/替换 802.11 帧标头的相应类型的泛型 802.11 标头。</p></td>
<td align="left"><p>目标/谈论</p></td>
<td align="left"><p>第一个连续的帧缓冲区有 （之前 MAC 标头） 的开始处的可用空间。 此空间取决于设备参数中指定 BackfillSize。</p>
<p>对于非 EAPOL 的数据包，第一个缓冲区包含 MAC 和 LLC/管理单元的标头，但不是有效负载。 EAPOL 数据包的第一个连续缓冲区可能包含有效负载的一部分 （或 all）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TX 分类</p></td>
<td align="left"><p>确定 TID。 确定基于单播远程协助或 DA.的收件人</p></td>
<td align="left"><p>WDI 执行分类时<strong>TargetPriorityQueueing</strong>为 false。 WDI 如果不执行分类<strong>TargetPriorityQueueing</strong>为 true。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>传输队列</p></td>
<td align="left"><p>在单独的队列中的应用商店 TX 帧。</p></td>
<td align="left"><p>如果需要 WDI 排队 TX 帧。</p></td>
<td align="left"><p>WDI 队列 TX 帧通过端口 (<strong>TargetPriorityQueueing</strong> = true) 或由收件人和流量类型 （对等互连 Id、 TID） (<strong>TargetPriorityQueueing</strong> = false)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TX 流控制</p></td>
<td align="left"><p>防止 TIL 无限大或目标 TX 帧缓冲区。</p></td>
<td align="left"><p>WDI/TIL/Target</p></td>
<td align="left"><p>在主机目标流控制，请参阅部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>计划传输</p></td>
<td align="left"><p>选择从中传输帧谈论 / 磁贴时有多个积压的队列 TX 队列。</p></td>
<td align="left"><p>如果需要队列 TX 帧，WDI。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>一个 MSDU 聚合</p></td>
<td align="left"><p>确定哪些框架可以分组到一个 MSDU 聚合必须重新传输过程中保留的。</p></td>
<td align="left"><p>谈论/目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>碎片</p></td>
<td align="left"></td>
<td align="left"><p>谈论/目标</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>WLAN 计划</p></td>
<td align="left"><p>确定哪些收件人无法传送到下一步，哪种流量类型为发送和要发送的帧数。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>加密</p></td>
<td align="left"><p>框架内容使用的安全类型和接收方 （或发件人，多播帧） 为指定的安全密钥进行加密。 添加安全封装在适用的情况。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>对于支持 FIPS 的系统，该主机软件中完成加密。 目标的加密，则跳过。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>一个 MPDU 聚合</p></td>
<td align="left"><p>确定哪些组到一个 MPDU 聚合，和在重新传输期间修改其中的帧。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>重试</p></td>
<td align="left"><p>重新传输 MPDUs nacked 或不接收方的确认。</p></td>
<td align="left"><p>目标</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="operation-in-host-implemented-fips-mode"></a>在 Host-Implemented FIPS 模式下的操作


如果主机为给定的连接提供了 FIPS (主机 FIPS 模式设置为 true [ **WDI\_TLV\_连接\_设置**](https://msdn.microsoft.com/library/windows/hardware/dn926261))，主机对数据包进行加密之前提交到目标。 目标传输无需进行其他更改影响数据完整性的数据包的数据包。 例如，目标必须执行传输 MSDU 聚合在此模式下。

中的更常见情况下主机 FIPS 模式未启用 （目标实现加密模式），标头 802.11 标头后面是未加密的有效负载数据。 如果包需要在传输之前加密，目标对数据包进行加密。 它还执行 QoS 优先顺序的数据包，并可能会执行 TCP 层卸载操作 （如校验和或大量发送）。 为此发送处理，目标可能需要将其他标头添加到数据包 (例如，QoS，HT 标头或 IV)。

## <a name="tx-encapsulation-population-of-80211-tx-frame-headers"></a>TX 封装：802.11 TX 框架标头的填充


网络数据提交到的端口 （目标设备） 的 802.11 数据包格式。 每个传输的帧开始 802.11 MAC 报头。 主机设置的某些 MAC 标头的字段时目标设置其他字段。 下表描述了 802.11 MAC 报头和密码标头的哪些字段填充的主机，并应通过目标设备对其进行填充。

<table>
<tr><th>字段名称</th><th>子字段名称</th><th colspan="2">目标实现加密模式</th><th colspan="2">宿主实现 FIPS 模式</th>
</tr>
    <tr><th></th><th></th><th>由主机设置</th><th>由目标设置</th><th>由主机设置</th><th>由目标设置</th></tr>
    <tr><td>Frame 控件</td><td>协议版本</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>Frame 控件</td><td>在任务栏的搜索框中键入</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>Frame 控件</td><td>子类型</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>Frame 控件</td><td>到 DS</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>Frame 控件</td><td>从 DS</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>Frame 控件</td><td>多个片段</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>Frame 控件</td><td>重试</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>Frame 控件</td><td>电源管理</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>Frame 控件</td><td>更多的数据</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>Frame 控件</td><td>受保护的帧</td><td></td><td>X</td><td>X</td><td></td></tr>
    <tr><td>Frame 控件</td><td>顺序</td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>持续时间/Id</td><td></td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>地址 1</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>地址 2</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>地址为 3</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>序列控制</td><td>片段数</td><td>X</td><td></td><td></td><td>X</td></tr>
    <tr><td>序列控制</td><td>序列号</td><td></td><td>X</td><td></td><td>X</td></tr>
    <tr><td>地址 4</td><td></td><td>X</td><td></td><td>X</td><td></td></tr>
    <tr><td>QoS 控件</td><td></td><td></td><td>添加/填充目标。</td><td></td><td>添加/填充在 11n QoS 关联的情况下的目标。</td></tr>
    <tr><td>超线程控件</td><td></td><td></td><td>添加/填充目标。</td><td></td><td>添加/填充目标。</td></tr>
</table>

## <a name="related-topics"></a>相关主题


[**NDIS\_TCP\_IP\_校验和\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567878)

[WDI 数据传输](wdi-data-transfer.md)

[**WDI\_TLV\_CONNECTION\_SETTINGS**](https://msdn.microsoft.com/library/windows/hardware/dn926261)

[**WDI\_TXRX\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/dn898187)

 

 






