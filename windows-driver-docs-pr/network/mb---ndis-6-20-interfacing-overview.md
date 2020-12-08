---
title: MB/NDIS 6.20 接口概述
description: MB/NDIS 6.20 接口概述
keywords:
- NDIS 6.20 WDK，移动宽带 (MB) 接口
- 移动宽带 (MB) WDK
- 移动宽带 (MB) WDK，NDIS 6.20 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 948db0e73ed58d4e2c47dcad072b064e0736a40b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831331"
---
# <a name="mb--ndis-620-interfacing-overview"></a>MB/NDIS 6.20 接口概述


本主题旨在提供有关 *NDIS 6.20 规范* 的充足背景，以将 MB 驱动程序模型放入透视。 它不应作为 NDIS 6.20 的参考。 如果此内容与 *ndis 6.20 规范* 之间的差异，请参阅 [NDIS 6.20](introduction-to-ndis-6-20.md) 文档获取完整的信息。

在 NDIS 6.20 中，MB 服务调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 将 OID 请求颁发给微型端口驱动程序。 然后，微型端口驱动程序调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) ，将数据返回到 MB 服务。

NDIS 6.20 支持下列类型的 OID 操作：

-   *设置* 从服务向微型端口驱动程序发送数据的操作。

-   请求微端口驱动程序以将数据返回到服务的 *查询* 操作。

-   与函数调用等效的 *方法* 操作，同时具有输入参数和输出参数。

最后，微型端口驱动程序可能会发送包含数据的 *指示* ，以通知服务在 MB 设备中发生了状态更改。

### <a name="receiving-set-and-query-requests"></a>接收 *设置* 和 *查询* 请求

MB 微型端口驱动程序实现 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) NDIS 处理程序以响应 *集* 和 *查询* 请求。

### <a name="sending-status-indications"></a>发送状态指示

微型端口驱动程序通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)向 MB 服务提供状态指示。 有关状态指示的详细信息，请参阅 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构。

### <a name="connection-state-indications"></a>连接状态指示

NDIS 6.20 微型端口驱动程序必须使用 [**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 指示，通知 ndis 和过量驱动程序已更改传输媒体的物理特性。

NDIS **StatusBuffer** \_ 状态指示结构的 StatusBuffer 成员 \_ 是一个 [**ndis \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构，它指定传输媒体的物理状态。

如果介质的物理状态没有变化，则 MB 微型端口驱动程序应避免发送 NDIS \_ 状态 \_ 链接 \_ 状态指示。 但是，不一定需要微型端口驱动程序来避免发送此状态指示。

MB 微型端口驱动程序必须报告当前连接的数据类的最大数据速率。 当连接时，数据类中的更改必须使用报告的相应数据速率来指示连接状态。 下面是此规则的推荐实现：

1.  符合此规范的 MB 微型端口驱动程序必须使用 [**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 来指示连接状态更改，而不是将 NDIS 状态 \_ \_ 媒体 \_ 连接、ndis \_ 状态 \_ 媒体 \_ 断开连接或 ndis \_ 状态 \_ 链接 \_ 速度 \_ 更改 (如 ndis 5.1) 中的连接状态指示。

2.  [**Ndis \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的 **XmitLinkSpeed** 和 **RcvLinkSpeed** 成员不能报告 ndis \_ 链接 \_ 速度 \_ UNKNOWN 未知。 微型端口驱动程序必须通过使用下表中的信息来报告速度。

**对于基于 GSM 的 MB 设备速度链接**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">数据类</th>
<th align="left">XmitLinkSpeed</th>
<th align="left">RcvLinkSpeed</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GPRS</p></td>
<td align="left"><p>8到 48 kbps</p></td>
<td align="left"><p>8到 48 kbps</p></td>
</tr>
<tr class="even">
<td align="left"><p>EDGE</p></td>
<td align="left"><p>8到 220 kbps</p></td>
<td align="left"><p>8到 220 kbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UMTS</p></td>
<td align="left"><p>64到 384 kbps</p></td>
<td align="left"><p>64到 384 kbps</p></td>
</tr>
<tr class="even">
<td align="left"><p>HSDPA</p></td>
<td align="left"><p>64到 5.76 mbps</p></td>
<td align="left"><p>1.8 到 14.4 mbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HSUPA</p></td>
<td align="left"><p>1.4 到 5.76 mbps</p></td>
<td align="left"><p>64 kbps 到 7.2 mbps</p></td>
</tr>
</tbody>
</table>

 

**对于基于 CDMA 的 MB 设备速度链接**

| 数据类     | XmitLinkSpeed            | RcvLinkSpeed            |
|----------------|--------------------------|-------------------------|
| 1xRTT          | 115.2 kbps 到 307.2 kbps | 153.6 kbps 到 3 mbps    |
| 3xRTT          | 614 kbps 到 1.04 mbps    | 307.2 kbps 到 1.04 mbps |
| 1xEV-DO        | 153.6 kbps               | 2.4 mbps                |
| 1xEvDO Rev。 | 1.8 mbps                 | 3.1 mbps                |
| 1xEV-DV        | 1.8 mbps                 | 3.1 mbps                |
| 1xEvDO | 27 mbps                  | 3.1 mbps 到 73.5 mbps   |

 

**注意**  MB 设备应报告上表中显示的速度范围。

 

与 NDIS 5.1 不同，不同的链接状态更改指示 \_ \_ \_ 通过使用 ndis \_ 链接 \_ 状态数据结构合并为单个 NDIS 状态链接状态指示。 根据下表中的信息，可以将 NDIS 5.1 指示映射到此结构。 在链接速度变化的情况下，指示的使用者应该将发射和接收速度值与它为先前指示记录的值进行比较，以确定是否发生了链接速度更改。

**从 NDIS 5.1 到 6. x 的连接状态指示**

NDIS 5.1 指示 NDIS 1.x ndis \_ 链接 \_ 状态数据结构参数值 NDIS \_ 状态 \_ 媒体 \_ 连接

MediaConnectState

MediaConnectStateConnected

NDIS \_ 状态 \_ 媒体 \_ 断开连接

MediaConnectState

MediaConnectStateDisconnected

NDIS \_ 状态 \_ 链接 \_ 速度 \_ 更改

XmitLinkSpeed

传输速度 (bps) 

RcvLinkSpeed

接收速度 (bps) 

 

 

