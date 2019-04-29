---
title: 规则合并 TCP/IP 段
description: 本部分中定义的规则合并 TCP/IP 段微型端口驱动程序中
ms.assetid: EC3C72EB-20A6-4D48-8E8C-F70EE4483193
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b65e9adced45cbd7a55ca24bbb84ce24005905b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359751"
---
# <a name="rules-for-coalescing-tcpip-segments"></a>合并 TCP/IP 段的规则


本部分将定义时接收段合并 (RSC) 指定的规则-支持的微型端口驱动程序必须合并给定的 TCP 连接的段。 如果违反了任何规则，则会生成异常，并且微型端口驱动程序必须中止段的合并。

微型端口驱动程序必须更新单个合并单元 (SCU) 的 IP 和 TCP 标头。 微型端口驱动程序必须重新 TCP 和 IPv4 校验和计算通过 SCU 和链接在 TCP 有效负载。

以下两个流程图的第一个描述用于合并段和更新的 TCP 标头的规则。 此流程图是指用于区分有效重复用于确认和窗口更新的机制。 第二个流程图描述了这些机制。

这些流程图了解 RSC 规则用作参考。 硬件实现可以优化流程图，只要保持正确性。

流程图中使用以下术语：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SEG.SEQ</strong></p></td>
<td align="left"><p>传入的段的序列号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.SEQ</strong></p></td>
<td align="left"><p>当前跟踪 SCU 的序列号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG.ACK</strong></p></td>
<td align="left"><p>传入的段的确认号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.ACK</strong></p></td>
<td align="left"><p>确认当前跟踪 SCU 数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG.WND</strong></p></td>
<td align="left"><p>传入的段由播发的窗口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.WND</strong></p></td>
<td align="left"><p>由当前跟踪 SCU 播发的窗口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG.LEN</strong></p></td>
<td align="left"><p>TCP 有效负载的传入的段的长度。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.LEN</strong></p></td>
<td align="left"><p>当前跟踪 SCU TCP 有效负载长度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SEG.NXT</strong></p></td>
<td align="left"><p>总和<strong>SEG。SEQ</strong>和<strong>SEG。LEN</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>H.NXT</strong></p></td>
<td align="left"><p>总和<strong>H.SEQ</strong>并<strong>H.LEN</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>H.DupAckCount</strong></p></td>
<td align="left"><p>已合并到 SCU 的重复用于确认数。 此数字应该为 0。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SEG.Tsval</strong></p></td>
<td align="left"><p><strong>时间戳</strong>当前接收的段中的值。 中定义此值的格式<a href="http://www.ietf.org/rfc/rfc1323.txt" data-raw-source="[RFC 1323](http://www.ietf.org/rfc/rfc1323.txt)">RFC 1323</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>H.Tsval</strong></p></td>
<td align="left"><p><strong>时间戳</strong>当前跟踪 SCU 中的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SEG.TSecr</strong></p></td>
<td align="left"><p><strong>时间戳回送答复</strong>当前接收的段中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>H.TSecr</strong></p></td>
<td align="left"><p><strong>时间戳回送答复</strong>当前跟踪 SCU 中。</p></td>
</tr>
</tbody>
</table>

 

![说明合并段和更新 tcp 标头的规则的流程图](images/rsc-rules1.png)

![说明用于区分有效重复用于确认和窗口更新机制的流程图](images/rsc-rules2.png)

流程图显示微型端口驱动程序可能会合并具有不同的 ACK 数量的段。 但是，微型端口驱动程序必须遵循关于 ACK 数字的以下规则，如上面的第一个流程图中所示：

-   执行序列号检查之后, 传入纯 ACK 可能会合并到当前跟踪 SCU 如果一种或两个以下条件：

    -   **H.ACK** == **SEG。ACK**。
    -   正在跟踪合并段中的重复确认计数为零。 换而言之， **H.DupAckCount** = = 0。

    换而言之，不是重复的 ACK 或窗口更新任何纯 ACK 触发异常并不合并。 所有此类纯确认必须表示为各个段。 此规则可确保，RSC 不影响行为或 Windows TCP 拥塞控制算法的性能。

-   传入的数据段 (**SEG。ACK** == **H.ACK**) 或传入背载 ACK (**SEG。ACK** &gt; **H.ACK**) 可能合并到当前跟踪 SCU 中，如果满足两个以下条件：

    -   段是连续到 SCU 序列空间中。 换而言之， **SEG。SEQ** == **H.NXT**。
    -   正在跟踪合并段中的重复确认计数为零。 换而言之， **H.DupAckCount** = = 0。

## <a name="additional-notes-on-duplicate-ack-coalescing"></a>有关重复确认合并的其他说明


### <a name="duplicate-ack-behavior"></a>重复的 ACK 行为

微型端口驱动程序应将等效于纯 ACK 重复 ACK 段并不将合并。 在这种情况下，它必须完成指示当前 SCU （如果有） 并指示重复的 ACK 段作为单独的段。 因为 Windows 客户端使用选择性确认 (SACK) 默认情况下，重复的 ACK 段很可能会生成异常。 请参阅[示例的接收段合并](examples-of-receive-segment-coalescing.md)有关的示例。 如果使用的段**DupAckCount** &gt; 0 指示，NDIS 将禁用 RSC 接口上的。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-data-segments"></a>处理重复的 ACK 跟踪包含数据段 SCU 时

当跟踪与 SCU **H.LEN** &gt; 0 （即，合并段包含数据），如果重复确认到达下一步，则应按如下所示完成而 SCU 跟踪：

1.  应跟踪新 SCU，从开始重复确认。

2.  **DupAckCount**新 SCU 应设置为零。

3.  **DupAckCount**如果在收到其他重复确认时都会递增。

在这种情况下， **DupAckCount**将是 1，不会早于重复用于确认数。 主机堆栈将处理计数正确。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-a-pure-cumulative-ack"></a>处理重复的 ACK 跟踪包含了纯累积确认 SCU 时

跟踪包含单个的纯累积 ACK （规则禁止合并多个纯 Ack） SCU 时，如果接下来，收到重复确认，然后**DupAckCount**应递增 SCU 的跟踪。 它也应在收到其他重复确认如果将递增。 在这种情况下， **DupAckCount**将等于重复用于确认合并数。

### <a name="when-the-first-segment-that-is-received-in-a-dpc-is-a-duplicate-ack"></a>DPC 中收到的第一个段时重复确认

在这种情况下，NIC 无法确定接收到的段是否重复确认，因为它不维护任何状态。 因此段应被视为纯 ACK 改为按如下所示：

1.  应跟踪新 SCU，开始此段。

2.  **DupAckCount**新 SCU 应设置为零。

3.  **DupAckCount**为收到的每个其他重复确认加 1。

在这种情况下， **DupAckCount**将等于 1 小于重复用于确认的实际数目。 主机堆栈将处理计数正确。

### <a name="duplicate-ack-exemption"></a>重复的 ACK 例外

微型端口驱动程序可能将重复的 ACK 段等效于纯确认并不将合并。 在这种情况下，它必须完成指示当前 SCU （如果有） 并指示重复的 ACK 段作为单独的段。 因为 Windows 客户端默认情况下使用 SACK，重复的 ACK 段很可能会生成异常。 有关示例，请参阅[示例的接收段合并](examples-of-receive-segment-coalescing.md)。 此例外不适用于窗口更新段。

## <a name="coalescing-segments-with-the-timestamp-option"></a>使用时间戳选项合并段


TCP 时间戳选项是唯一可能合法合并的选项。 合并段与此选项保留为特定于实现的决策。 如果微型端口驱动程序将合并有时间戳选项段，它必须遵循以下流程图中所述的规则：

![描述规则使用 tcp 时间戳选项合并段的流程图](images/rsc-rules3.png)

**请注意**  检查**SEG。TSval** &gt; =  **H.TSval**必须使用类似于使用 TCP 序列号为 232 取模算术执行。 请参阅[RFC 793](http://www.ietf.org/rfc/rfc793.txt)，第 3.3 部分。

 

时，该值指示合并的段，必须按如下所示指示以下带外信息通过设置**NetBufferListInfo**的成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)描述合并的段结构：

-   已合并的段数必须存储到**NetBufferListInfo**\[**TcpRecvSegCoalesceInfo**\]。**CoalescedSegCount**成员。 此数字仅表示已合并的数据段。 纯 ACK 合并禁止的窗口更新段必须不被视为此字段的一部分。

-   重复的 ACK 计数必须存储到**NetBufferListInfo**\[**TcpRecvSegCoalesceInfo**\]。**DupAckCount**成员。 上面的第一个流程图说明了如何计算此值。

-   当使用 TCP 时间戳选项的段是否已合并时， **NetBufferListInfo**\[**RscTcpTimestampDelta** \]必须使用之间的最早的绝对增量填充和合并的段的序列中看到的最新 TCP 时间戳值组成 SCU。 SCU 本身应包含合并的段的序列中看到的最新 TCP 时间戳值。

**DupAckCount**并**RscTcpTimestampDelta**成员进行解释，当且仅当**CoalescedSegCount**成员是大于零。 如果**CoalescedSegCount**为零，段被视为非合并非-RSC 段。

有关的内容信息**NetBufferListInfo**成员，请参阅[ **NDIS\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566569)并[ **NDIS\_RSC\_NBL\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451655)。

PSH 位的所有合并的段应或运算。 换而言之，如果 PSH 位已设置任何单独的段中，微型端口驱动程序应在 SCU 设置 PSH 位。

正在最后完成 SCU 涉及：

-   重新计算 TCP 和，如果适用，IPv4 校验和。

-   更新 IP 标头，如中所述[更新 IP 标头的合并段](updating-the-ip-headers-for-coalesced-segments.md)。

-   在为相同的值在各个段中设置的 TCP 和 IP 标头中设置 ECN bits 和 ECN 字段。

## <a name="handling-tcpip-ipsec-segments"></a>处理 TCP/IP IPsec 段


网络卡可能会报告 RSC 和 IPsec 任务卸载功能。 (请参阅[确定网络适配器的 RSC 功能](determining-the-rsc-capabilities-of-a-network-adapter.md)。)但是，如果它支持的 IPsec 任务卸载，它必须尝试合并由 IPsec 保护的段。

 

 





