---
title: 数据包注入函数
description: 数据包注入函数
ms.assetid: ebbcafb6-7fbf-40e6-8806-0131aa1d4df5
keywords:
- 数据包注入函数 WDK Windows 筛选平台
- 注入函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a1bbc61b4295003cafed8be66a142552455809d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357599"
---
# <a name="packet-injection-functions"></a>数据包注入函数


标注驱动程序可以调用以下的 WFP 函数，将挂起，或者修改为 TCP/IP 堆栈的数据包数据。 下表列出了适用层从其数据可以注入，以及可能的目标。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">注入函数</th>
<th align="left">适用的层</th>
<th align="left">目标</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectforwardasync0" data-raw-source="[&lt;strong&gt;FwpsInjectForwardAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectforwardasync0)"><strong>FwpsInjectForwardAsync0</strong></a></p></td>
<td align="left"><p>网络层</p></td>
<td align="left"><p>转发数据路径</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectnetworkreceiveasync0" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkReceiveAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectnetworkreceiveasync0)"><strong>FwpsInjectNetworkReceiveAsync0</strong></a></p></td>
<td align="left"><p>网络层</p></td>
<td align="left"><p>接收数据路径</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectnetworksendasync0" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkSendAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectnetworksendasync0)"><strong>FwpsInjectNetworkSendAsync0</strong></a></p></td>
<td align="left"><p>网络层</p></td>
<td align="left"><p>发送数据路径</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjecttransportreceiveasync0" data-raw-source="[&lt;strong&gt;FwpsInjectTransportReceiveAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjecttransportreceiveasync0)"><strong>FwpsInjectTransportReceiveAsync0</strong></a></p></td>
<td align="left"><p>从传输、 数据报数据、 ICMP 错误或 ALE 层的数据包数据</p></td>
<td align="left"><p>接收数据路径</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync0" data-raw-source="[&lt;strong&gt;FwpsInjectTransportSendAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync0)"><strong>FwpsInjectTransportSendAsync0</strong></a></p></td>
<td align="left"><p>从传输、 数据报数据、 ICMP 错误或 ALE 层的数据包数据</p></td>
<td align="left"><p>发送数据路径</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsstreaminjectasync0" data-raw-source="[&lt;strong&gt;FwpsStreamInjectAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)"><strong>FwpsStreamInjectAsync0</strong></a></p></td>
<td align="left"><p>TCP 数据段</p></td>
<td align="left"><p>数据流</p></td>
</tr>
</tbody>
</table>

 

此外， [ **FwpsQueryPacketInjectionState0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)函数用于检查数据包数据的注入历史记录。

标注可以提供所有需要的信息所需的注入函数中，如果启用了跨层注入并且 net 缓冲区列表具有注入函数所需的格式。 例如，一个标注可以捕获数据包转发路径，修改的本地计算机，并调用其目标地址**FwpsInjectTransportReceiveAsync0**重定向到本地计算机的 TCP/IP 堆栈的数据包。

流 （TCP 数据） 注入，除了注入的传入数据包重新输入"底部"的堆栈和 WFP 层时注入的传出数据包重新输入"顶部"的堆栈和 WFP 层。 例如，从传入的数据报数据层注入一个 UDP 数据包将重新输入堆栈并遍历网络层，传输层，ALE 接收或接受层 （可选），并显示在数据报数据层。 从传出的网络层注入的另一个 UDP 数据包将重新输入堆栈和遍历 ALE （可选）、 数据报数据和传输层和回网络层。

**FwpsInjectTransportReceiveAsync0**自动跳过 IPsec 处理对于 reinjected 数据包，因为它以前已经过 IPsec 验证。

WFP 标注驱动程序注入的数据包将重新指定为在其中对数据包进行修改后，即可错过原始筛选器条件的事例中除标注。 WFP 提供**FwpsQueryPacketInjectionState0**数据包被注入 （或前面注入） 函数的查询的标注的标注。 若要防止无限循环，调出应允许自插入的数据包。

标注必须调整 IP 或传输层校验和，或两者后它们修改的 IP 数据包。 标注可以设置校验和为 0 的 UDP 通过 IPv4 数据包。 为兼容的传输层校验和卸载，并相应地调整与伪校验和计算完整的校验和，标注可以使用以下逻辑：

```cpp
NDIS_TCP_IP_CHECKSUM_PACKET_INFO ChecksumInfo;
 ChecksumInfo.Value = 
 (ULONG) (ULONG_PTR)NET_BUFFER_LIST_INFO(
 NetBufferList,TcpIpChecksumNetBufferListInfo);
```

如果 ChecksumInfo.Transmit.NdisPacketTcpChecksum **，则返回 TRUE**，将卸载 TCP 发送操作。 如果 ChecksumInfo.Transmit.NdisPacketUdpChecksum **，则返回 TRUE**，将卸载 UDP 发送操作。

在 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 中，如果 inMetaValues-&gt;headerIncludeHeaderLength 大于 0，将传出数据包是包含 IP 标头原始发送 reinjection。 若要执行的 Windows Vista SP1 和 Windows Server 2008 包含 IP 标头的原始发送 reinjections，您必须按 inMetaValues-amount retreat 克隆的数据包&gt;headerIncludeHeaderLength 并复制 inMetaValues-&gt;对于新扩展空间 headerIncludeHeader。 然后，针对数据包最终缓冲区列表使用 FwpsInjectTransportSendAsync0 并使 FWPS\_传输\_发送\_PARAMS0 参数设置为**NULL**。 有关参加 net 缓冲区列表操作的详细信息，请参阅[撤回和高级操作](retreat-and-advance-operations.md)。

**请注意**  对于原始发送操作，net 缓冲区列表必须包含单个 net 缓冲区。 如果 net 缓冲区列表中包含多个网络缓冲区，您必须将您的网络缓冲区列表转换为一系列 net 缓冲区列表和每个序列中必须包含单个 net 缓冲区。 有关 net 缓冲区列表管理的详细信息，请参阅[NET\_缓冲体系结构](net-buffer-architecture.md)。

 

 

 





