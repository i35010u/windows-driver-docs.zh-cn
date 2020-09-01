---
title: 用于合并 TCP/IP 段的规则
description: 本部分定义用于合并微型端口驱动程序中的 TCP/IP 段的规则
ms.assetid: EC3C72EB-20A6-4D48-8E8C-F70EE4483193
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4ab768fd42b1e976edb562f21cd39e27ebae6a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206255"
---
# <a name="rules-for-coalescing-tcpip-segments"></a>合并 TCP/IP 段的规则

本节定义一些规则，这些规则指定接收段合并 (RSC) 功能的微型端口驱动程序必须为给定 TCP 连接合并段。 如果违反了任何规则，则会生成异常，而微型端口驱动程序必须中止段的合并。

微型端口驱动程序必须更新单个合并单元 (SCU) 的 IP 和 TCP 标头。 微型端口驱动程序必须通过 SCU 重新计算 TCP 和 IPv4 校验和，并链接 TCP 有效负载。

下面的两个流程图介绍了合并段和更新 TCP 标头的规则。 此流程图指的是区分有效的重复 Ack 和窗口更新的机制。 第二个流程图介绍了这些机制。

这些流程图作为参考提供，用于了解 RSC 规则。 只要保持正确，硬件实现就可以优化流程图。

流程图中使用了以下术语：

|术语|说明|
|----|----|
|**SEG.序列**|传入段的序列号。|
|**H。**|当前跟踪的 SCU 的序列号。|
|**SEG.ACK**|传入段的确认号。|
|**H。**|当前跟踪的 SCU 的确认号。|
|**SEG.WND**|传入段播发的窗口。|
|**WND**|当前跟踪的 SCU 所播发的窗口。|
|**SEG.长度**|传入段的 TCP 负载长度。|
|**H。**|当前跟踪的 SCU 的 TCP 负载长度。|
|**SEG.NXT**|SEG 的总和 **。SEQ** 和 **SEG。LEN**。|
|**H。**|**H. SEQ**和 **.h**的总和。|
|**DupAckCount**|已合并到 SCU 中的重复 Ack 的数目。 此数字应该为 0。|
|**SEG.Tsval**|当前接收段中的 **时间戳** 值。 此值的格式在 [RFC 1323](https://www.ietf.org/rfc/rfc1323.txt)中定义。|
|**Tsval**|当前跟踪的 SCU 中的 **时间戳** 值。|
|**SEG.TSecr**|当前接收的段中的 **时间戳回显回复** 。|
|**TSecr**|当前跟踪的 SCU 中的 **时间戳回显回复** 。|

![描述合并段和更新 tcp 标头的规则的流程图](images/rsc-rules1.png)

![介绍用于区分有效重复 ack 和窗口更新的机制的流程图](images/rsc-rules2.png)

流程图显示微型端口驱动程序可以合并具有不同 ACK 编号的段。 但是，微型端口驱动程序必须遵守有关 ACK 号码的以下规则，如以上第一个流程图中所示：

- 执行序列号检查后，如果传入的纯确认满足以下一个或两个条件，则可以将其合并到当前跟踪的 SCU 中：

  - **H.**  == **SEG。ACK**。
  - 正在跟踪的合并段中的重复确认计数为零。 换句话说， **DupAckCount** = = 0。

    换句话说，任何不是重复确认或窗口更新的纯确认都将触发异常，且不能合并。 所有此类纯确认都必须表示为各个段。 此规则可确保 RSC 不会影响 Windows TCP 拥塞控制算法的行为或性能。

- 传入的数据段 (**SEG。Ack**  ==  **H.ACK**) 或传入的非法携带支持的 ack (**SEG。** &gt; 如果同时满足以下两个条件，则可能会将 ack **.h**) 合并到当前跟踪的 SCU 中：

  - 段与序列空间中的 SCU 是连续的。 换句话说， **SEG。SEQ**  ==  **.H**。
  - 正在跟踪的合并段中的重复确认计数为零。 换句话说， **DupAckCount** = = 0。

## <a name="additional-notes-on-duplicate-ack-coalescing"></a>有关重复确认合并的其他说明

### <a name="duplicate-ack-behavior"></a>重复确认行为

微型端口驱动程序应将重复的 ACK 段与纯确认视为等效，而不是合并。 在这种情况下，如果有任何) 用于指示并将重复的确认段指示为单独段，则它必须完成当前的 SCU (。 由于 Windows 客户端使用选择性确认 (SACK) 默认情况下，重复的确认段可能会产生异常。 有关示例，请参阅 [接收段合并的示例](examples-of-receive-segment-coalescing.md) 。 如果指示了包含 **DupAckCount** &gt; 0 的段，则 NDIS 将在接口上禁用 RSC。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-data-segments"></a>跟踪包含数据段的 SCU 时处理重复的确认

当跟踪 **SCU 为** &gt; 0 (换言之，包含数据) 的合并段（如果下一个重复的确认到达），则应按如下所示完成跟踪 SCU：

1. 应跟踪新的 SCU，从重复的确认开始。

2. 新 SCU 的 **DupAckCount** 应设置为零。

3. 如果接收到其他重复的 Ack，则应增加 **DupAckCount** 。

在这种情况下， **DupAckCount** 将比重复确认次数小1。 宿主堆栈会正确地处理计数。

### <a name="handling-duplicate-ack-when-tracking-a-scu-consisting-of-a-pure-cumulative-ack"></a>跟踪由纯累计确认组成的 SCU 时的重复确认

如果跟踪的 SCU 包含单个纯累计确认 (规则禁止合并多个纯确认) ，则如果重复确认到达，则跟踪 SCU 的 **DupAckCount** 应增加。 如果接收到其他重复的 Ack，还应增加。 在这种情况下， **DupAckCount** 将等于合并的重复 ack 的数目。

### <a name="when-the-first-segment-that-is-received-in-a-dpc-is-a-duplicate-ack"></a>当 DPC 中收到的第一段是重复确认时

在这种情况下，NIC 无法确定接收的段是否是重复的确认，因为它不维护任何状态。 因此应将段视为纯确认，如下所示：

1. 应跟踪新的 SCU，从此段开始。

2. 新 SCU 的 **DupAckCount** 应设置为零。

3. 对于收到的每个额外的重复确认， **DupAckCount** 应递增1。

在这种情况下， **DupAckCount** 将等于1，小于重复确认的实际数量。 宿主堆栈会正确地处理计数。

### <a name="duplicate-ack-exemption"></a>确认免除重复

微型端口驱动程序可能会将重复的 ACK 段视为纯确认，而不是合并。 在这种情况下，如果有任何) 用于指示并将重复的确认段指示为单独段，则它必须完成当前的 SCU (。 由于 Windows 客户端在默认情况下使用 SACK，因此重复的确认段可能会产生异常。 有关示例，请参阅 [接收段合并的示例](examples-of-receive-segment-coalescing.md)。 此例外不适用于窗口更新段。

## <a name="coalescing-segments-with-the-timestamp-option"></a>用 Timestamp 选项合并段

TCP 时间戳选项是可以进行合法合并的唯一选项。 使用此选项的合并段将保留为特定于实现的决策。 如果微型端口驱动程序将段与 timestamp 选项合并在一起，则必须遵循以下流程图中所述的规则：

![描述用于将段与 tcp 时间戳选项合并的规则的流程图](images/rsc-rules3.png)

>[!NOTE]
>检查**SEG。** &gt; =  **H.TSval**必须使用类似于用于 TCP 序列号的232的模数算法来执行 TSval。 请参阅 [RFC 793](https://www.ietf.org/rfc/rfc793.txt)，第3.3 节。

当指示合并段时，通过设置用于描述合并段的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的**NetBufferListInfo**成员，必须将以下带外信息指示如下：

- 已合并的段数必须存储到**NetBufferListInfo** \[ **TcpRecvSegCoalesceInfo**中 \] 。**CoalescedSegCount**成员。 此数字仅表示已合并的数据段。 禁止纯确认合并，并且不能将窗口更新段计为此字段的一部分。

- 重复的确认计数必须存储到**NetBufferListInfo** \[ **TcpRecvSegCoalesceInfo**中 \] 。**DupAckCount**成员。 上面的第一个流程图说明了如何计算此值。

- 当带有 TCP 时间戳选项的段合并在**NetBufferListInfo**一起时， \[ **RscTcpTimestampDelta** \] 必须用与 SCU 组成的合并段序列中的最早和最晚 TCP 时间戳值之间的绝对增量来填充 NetBufferListInfo RscTcpTimestampDelta。 SCU 本身应包含合并段序列中看到的最新 TCP 时间戳值。

当且仅当**CoalescedSegCount**成员大于零时，才会解释**DupAckCount**和**RscTcpTimestampDelta**成员。 如果 **CoalescedSegCount** 为零，则会将段视为未合并的非 RSC 段。

有关 **NetBufferListInfo** 成员内容的详细信息，请参阅 " [**ndis \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ne-ndis-_ndis_net_buffer_list_info) " 和 " [**ndis \_ RSC \_ NBL \_ info**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_rsc_nbl_info)"。

对于所有合并段，PSH 位应为运算。 换句话说，如果在任何单个段中设置了 PSH 位，微型端口驱动程序应在 SCU 中设置 PSH 位。

完成 SCU 涉及：

- 重新计算 TCP，如果适用，则重新计算 IPv4 校验和。

- 更新 IP 标头，如 [更新合并段的 Ip 标头](updating-the-ip-headers-for-coalesced-segments.md)中所述。

- 将 TCP 和 IP 标头中的 ECN 位和 ECN 字段设置为在各个段中设置的相同值。

## <a name="handling-tcpip-ipsec-segments"></a>处理 TCP/IP IPsec 段

网卡可能会报告 RSC 和 IPsec 任务卸载功能。  (参阅 [确定网络适配器的 RSC 功能](determining-the-rsc-capabilities-of-a-network-adapter.md)。 ) 不过，如果它支持 ipsec 任务卸载，则它不能尝试合并受 ipsec 保护的段。