---
title: SerCx2 I/O 事务
description: SerCx2 简化了 (IRP_MJ_READ) 读取和写入 (IRP_MJ_WRITE) 串行控制器驱动程序的请求的处理。
ms.assetid: C1B3F059-A445-4224-8316-DBF194CE6A80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c6d54870ac9a93ece45d465619404cc88add825
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349202"
---
# <a name="sercx2-io-transactions"></a>SerCx2 I/O 事务


SerCx2 简化了读取的处理 ([**IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff546883)) 和写入 ([**IRP\_MJ\_写**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) 串行控制器驱动程序的请求。 读取或写入请求的响应，SerCx2 向串行控制器驱动程序发出一个或多个 I/O 事务。 从驱动程序的角度来看，每个事务是一种简单和完成 I/O 操作。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="overview-of-sercx2-i-o-transactions.md" data-raw-source="[Overview of SerCx2 I/O Transactions](overview-of-sercx2-i-o-transactions.md)">SerCx2 I/O 事务的概述</a></p></td>
<td><p>SerCx2 通过向串行控制器驱动程序发出一个或多个 I/O 事务处理读取或写入请求从客户端。 此驱动程序将每个事务视为串行控制器与请求中的数据缓冲区之间传输数据的自包含 I/O 操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-pio-receive-transactions.md" data-raw-source="[SerCx2 PIO-Receive Transactions](sercx2-pio-receive-transactions.md)">SerCx2 PIO 接收事务</a></p></td>
<td><p>SerCx2 需要所有串行控制器驱动程序，以实现对支持接收事务使用编程 I/O (PIO)。 若要启动 PIO 接收事务，SerCx2 调用驱动程序的<a href="https://msdn.microsoft.com/library/windows/hardware/dn265214" data-raw-source="[&lt;em&gt;EvtSerCx2PioReceiveReadBuffer&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265214)"> <em>EvtSerCx2PioReceiveReadBuffer</em> </a>事件回叫函数并读取缓冲区作为参数提供。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-pio-transmit-transactions.md" data-raw-source="[SerCx2 PIO-Transmit Transactions](sercx2-pio-transmit-transactions.md)">SerCx2 PIO 传输的事务</a></p></td>
<td><p>SerCx2 需要所有串行控制器驱动程序，以实现对支持传输使用编程 I/O (PIO) 的事务。 若要启动 PIO 传输的事务，SerCx2 调用驱动程序的<a href="https://msdn.microsoft.com/library/windows/hardware/dn265223" data-raw-source="[&lt;em&gt;EvtSerCx2PioTransmitWriteBuffer&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265223)"> <em>EvtSerCx2PioTransmitWriteBuffer</em> </a>事件回叫函数并提供写入缓冲区作为参数。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-system-dma-receive-transactions.md" data-raw-source="[SerCx2 System-DMA-Receive Transactions](sercx2-system-dma-receive-transactions.md)">SerCx2 系统 DMA 接收事务</a></p></td>
<td><p>某些串行控制器驱动程序实现对支持接收使用系统 DMA 控制器的事务。 这种支持是可选的但可以提高性能，因为它使主处理器需要的用于通过编程方式设置 I/O (PIO) 的长整型数据传输。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-system-dma-transmit-transactions.md" data-raw-source="[SerCx2 System-DMA-Transmit Transactions](sercx2-system-dma-transmit-transactions.md)">SerCx2 系统 DMA 传输的事务</a></p></td>
<td><p>某些串行控制器驱动程序实现对支持传输使用系统 DMA 控制器的事务。 这种支持是可选的但可以提高性能，因为它使主处理器需要的用于通过编程方式设置 I/O (PIO) 的长整型数据传输。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-custom-receive-transactions.md" data-raw-source="[SerCx2 Custom-Receive Transactions](sercx2-custom-receive-transactions.md)">SerCx2 自定义接收事务</a></p></td>
<td><p>某些串行控制器硬件可能会实现 PIO 或系统 DMA 以外的数据传输机制，用于从串行控制器中读取数据。 串行控制器驱动程序支持自定义接收事务以 SerCx2 即可使用此数据传输机制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-custom-transmit-transactions.md" data-raw-source="[SerCx2 Custom-Transmit Transactions](sercx2-custom-transmit-transactions.md)">SerCx2 自定义传输的事务</a></p></td>
<td><p>某些串行控制器硬件可能会实现用于将数据写入串行控制器 PIO 或系统 DMA 以外的数据传输机制。 串行控制器驱动程序支持自定义传输的事务以 SerCx2 即可使用此数据传输机制。</p></td>
</tr>
</tbody>
</table>

 

 

 




