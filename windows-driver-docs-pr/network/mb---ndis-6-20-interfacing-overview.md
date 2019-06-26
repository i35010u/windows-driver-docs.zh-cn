---
title: MB/NDIS 6.20 接口概述
description: MB/NDIS 6.20 接口概述
ms.assetid: 6abde9b4-8ac2-4757-8db3-4f563fc5ed24
keywords:
- NDIS 6.20 WDK，移动宽带 (MB) 进行连接
- 移动宽带 (MB) WDK
- 移动宽带 (MB) WDK、 NDIS 6.20 进行连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d32345e58a98c3fddfca3002076cb51c524b3b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374815"
---
# <a name="mb--ndis-620-interfacing-overview"></a>MB/NDIS 6.20 接口概述


本主题提供有关提供足够的背景*NDIS 6.20 规范*将放入透视 MB 驱动程序模型。 它不是 NDIS 6.20 的引用。 在此内容之间的差异的情况下， *NDIS 6.20 规范*，请参阅[NDIS 6.20](introduction-to-ndis-6-20.md)文档的完整信息。

在 NDIS 6.20 MB 服务调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)问题 OID 请求到微型端口驱动程序。 然后，微型端口驱动程序调用[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)若要将数据返回到 MB 服务。

NDIS 6.20 支持以下类型的 OID 操作：

-   *设置*将数据从服务发送到微型端口驱动程序的操作。

-   *查询*请求微型端口驱动程序将数据返回给该服务的操作。

-   *方法*操作，等效于函数调用，，具有输入参数和输出参数。

最后，微型端口驱动程序可能会发送*迹象*包含数据，以通知有关 MB 设备中的状态更改的服务。

### <a name="receiving-set-and-query-requests"></a>接收*设置*并*查询*请求

MB 微型端口驱动程序实现[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request) NDIS 处理程序以响应同时*设置*并*查询*请求。

### <a name="sending-status-indications"></a>发送状态指示

微型端口驱动程序通过调用向 MB 服务提供状态指示[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)。 请参阅[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)状态指示有关的更多详细信息的结构。

### <a name="connection-state-indications"></a>连接状态指示

NDIS 6.20 微型端口驱动程序必须使用[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示通知 NDIS 和已有的基础驱动程序更改传输媒体的物理特征。

**StatusBuffer**成员的 NDIS\_状态\_指示结构[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构，它指定传输媒体的物理状态。

MB 微型端口驱动程序应避免发送 NDIS\_状态\_链接\_状态状态指示，指示是否不已在该介质的物理状态中的任何更改。 但是，微型端口驱动程序都不一定需要避免发送此状态指示。

MB 微型端口驱动程序必须报告当前连接的数据类的最大数据速率。 数据类在连接中的更改必须导致报告相应数据传输率连接状态指示。 以下是此规则的建议的实现：

1.  必须使用 MB 微型端口驱动程序符合此规范[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)以指示连接状态更改而不是 NDIS\_状态\_媒体\_CONNECT、 NDIS\_状态\_媒体\_断开连接或 NDIS\_状态\_链接\_速度\_连接状态指示，更改 （如在 NDIS 5.1)。

2.  **XmitLinkSpeed**并**RcvLinkSpeed**的成员[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构必须不报告 NDIS\_链接\_速度\_未知。 微型端口驱动程序必须通过使用下表中的信息来报告速度。

**为基于 GSM 的 MB 设备的链接速度**

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
<td align="left"><p>8 至 48 kbps</p></td>
<td align="left"><p>8 至 48 kbps</p></td>
</tr>
<tr class="even">
<td align="left"><p>EDGE</p></td>
<td align="left"><p>8 到 220 kbps</p></td>
<td align="left"><p>8 到 220 kbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UMTS</p></td>
<td align="left"><p>64 到 384 kbps</p></td>
<td align="left"><p>64 到 384 kbps</p></td>
</tr>
<tr class="even">
<td align="left"><p>HSDPA</p></td>
<td align="left"><p>64 到 5.76 mbps</p></td>
<td align="left"><p>1.8 为 14.4 mbps</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HSUPA</p></td>
<td align="left"><p>1.4 到 5.76 mbps</p></td>
<td align="left"><p>7\.2 mbps 以 64 kbps</p></td>
</tr>
</tbody>
</table>

 

**为基于 CDMA 的 MB 设备的链接速度**

| 数据类     | XmitLinkSpeed            | RcvLinkSpeed            |
|----------------|--------------------------|-------------------------|
| 1xRTT          | 115.2 kbps 到 307.2 kbps | 153.6 kbps 到 3 mbps    |
| 3xRTT          | 614 kbps 到 1.04 mbps    | 307.2 kbps 到 1.04 mbps |
| 1xEV-DO        | 153.6 kbps               | 2.4 mbps                |
| 1xEvDO 修订版 a。 | 1.8 mbps                 | 3.1 mbps                |
| 1xEV-DV        | 1.8 mbps                 | 3.1 mbps                |
| 1xEvDO 修订版 b。 | 27 mbps                  | 3.1 mbps 73.5 mbps   |

 

**请注意**  MB 设备都应报告范围内的上一个表中所示的速度的速度。

 

与不同的 NDIS 5.1 中，不同的链接状态更改指示合并到单个 NDIS\_状态\_链接\_状态指示使用 NDIS\_链接\_状态数据结构。 NDIS 5.1 指示可以映射到此结构根据下表中的信息。 在链接速度更改的情况下所指示的使用者应比较替换为以确定链接速度更改是否已发生或不是上一个指示它记录的传输和接收速度值。

**连接状态指示从 NDIS 5.1 到映射 6.x**

NDIS 5.1 指示 NDIS 6.x NDIS\_链接\_状态数据结构，参数值 NDIS\_状态\_媒体\_连接

MediaConnectState

MediaConnectStateConnected

NDIS\_状态\_媒体\_断开连接

MediaConnectState

MediaConnectStateDisconnected

NDIS\_状态\_链接\_速度\_更改

XmitLinkSpeed

传输速度 (bps)

RcvLinkSpeed

接收速度 (bps)

 

 

 





