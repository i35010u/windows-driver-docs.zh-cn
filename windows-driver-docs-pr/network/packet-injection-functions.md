---
title: 数据包注入函数
description: 数据包注入函数
ms.assetid: ebbcafb6-7fbf-40e6-8806-0131aa1d4df5
keywords:
- 数据包注入函数 WDK Windows 筛选平台
- 注入函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a49b70f9a63ddcec9d989b8b4fbc995e942d4d39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843712"
---
# <a name="packet-injection-functions"></a>数据包注入函数


标注驱动程序可以调用以下 WFP 函数将挂起或修改的数据包数据注入到 TCP/IP 堆栈中。 下表列出了可从中注入数据的适用层以及可能的目标。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectforwardasync0" data-raw-source="[&lt;strong&gt;FwpsInjectForwardAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectforwardasync0)"><strong>FwpsInjectForwardAsync0</strong></a></p></td>
<td align="left"><p>网络层</p></td>
<td align="left"><p>转发数据路径</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworkreceiveasync0" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkReceiveAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworkreceiveasync0)"><strong>FwpsInjectNetworkReceiveAsync0</strong></a></p></td>
<td align="left"><p>网络层</p></td>
<td align="left"><p>接收数据路径</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworksendasync0" data-raw-source="[&lt;strong&gt;FwpsInjectNetworkSendAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectnetworksendasync0)"><strong>FwpsInjectNetworkSendAsync0</strong></a></p></td>
<td align="left"><p>网络层</p></td>
<td align="left"><p>发送数据路径</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportreceiveasync0" data-raw-source="[&lt;strong&gt;FwpsInjectTransportReceiveAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportreceiveasync0)"><strong>FwpsInjectTransportReceiveAsync0</strong></a></p></td>
<td align="left"><p>传输数据、数据报数据、ICMP 错误或 ALE 层的数据包数据</p></td>
<td align="left"><p>接收数据路径</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync0" data-raw-source="[&lt;strong&gt;FwpsInjectTransportSendAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync0)"><strong>FwpsInjectTransportSendAsync0</strong></a></p></td>
<td align="left"><p>传输数据、数据报数据、ICMP 错误或 ALE 层的数据包数据</p></td>
<td align="left"><p>发送数据路径</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0" data-raw-source="[&lt;strong&gt;FwpsStreamInjectAsync0&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)"><strong>FwpsStreamInjectAsync0</strong></a></p></td>
<td align="left"><p>TCP 数据段</p></td>
<td align="left"><p>数据流</p></td>
</tr>
</tbody>
</table>

 

此外， [**FwpsQueryPacketInjectionState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)函数用于检查数据包数据的注入历史记录。

如果标注可提供注入函数所需的所有所需信息，并且 net buffer list 具有注入函数所需的格式，则将启用跨层注入。 例如，标注可以捕获转发路径中的数据包，将其目标地址修改为本地计算机的目标地址，并调用**FwpsInjectTransportReceiveAsync0**将数据包重定向到本地计算机的 tcp/ip 堆栈中。

除流（TCP 数据）注入外，注入的传入数据包将从堆栈和 WFP 层的 "底部" 重新输入，同时从堆栈和 WFP 层的 "顶部" 重新输入插入的传出数据包。 例如，注入传入数据报数据层的 UDP 数据包将重新输入堆栈，遍历网络层、传输层、ALE 接收或接受层（可选），并返回到数据报数据层。 注入到传出网络层的另一个 UDP 数据包将重新输入堆栈，并遍历 ALE （可选）、数据报数据和传输层，并返回到网络层。

**FwpsInjectTransportReceiveAsync0**会自动绕过重新插入文本数据包的 ipsec 处理，因为它以前已通过 ipsec 验证。

WFP 标注驱动程序插入的数据包将被重新指明给标注，但对数据包进行修改会导致其丢失原始筛选条件。 WFP 为标注提供**FwpsQueryPacketInjectionState0**函数，以查询该数据包是否已由标注注入（或前面插入）。 若要防止无限循环，标注应允许自注入的数据包。

在修改 IP 数据包后，标注必须调整 IP 或传输层校验和两者。 对于 UDP over IPv4 数据包，标注可以将校验和设置为0。 若要与传输层校验和卸载兼容，并相应地调整完整校验和与伪校验和计算，则标注可以使用以下逻辑：

```cpp
NDIS_TCP_IP_CHECKSUM_PACKET_INFO ChecksumInfo;
 ChecksumInfo.Value = 
 (ULONG) (ULONG_PTR)NET_BUFFER_LIST_INFO(
 NetBufferList,TcpIpChecksumNetBufferListInfo);
```

如果 NdisPacketTcpChecksum 为**TRUE**，则将卸载 TCP 发送操作 ChecksumInfo。 如果 NdisPacketUdpChecksum 为**TRUE**，则将卸载 UDP 发送操作。 ChecksumInfo

在 Windows Vista Service Pack 1 （SP1）和 Windows Server 2008 中，如果 inMetaValues-&gt;headerIncludeHeaderLength 大于0，则传出数据包是包含 IP 标头的原始发送 reinjection。 若要执行包含 Windows Vista SP1 和 Windows Server 2008 的 IP 标头的原始发送 reinjections，必须通过 inMetaValues-&gt;headerIncludeHeaderLength 中的数量撤回克隆的数据包，并将 inMetaValues&gt;headerIncludeHeader 复制到新的扩展空间。 然后，将 FwpsInjectTransportSendAsync0 用于数据包的网络缓冲区列表，并将 FWPS\_\_传输\_PARAMS0 参数设置为**NULL**。 有关网络缓冲区列表的撤回操作的详细信息，请参阅[撤回和高级操作](retreat-and-advance-operations.md)。

**注意**  对于原始发送操作，net buffer 列表必须只包含一个网络缓冲区。 如果网络缓冲区列表包含多个网络缓冲区，则必须将网络缓冲区列表转换为一系列网络缓冲区列表，而且序列中的每个都必须包含一个网络缓冲区。 有关网络缓冲区列表管理的详细信息，请参阅[net\_Buffer 体系结构](net-buffer-architecture.md)。

 

 

 





