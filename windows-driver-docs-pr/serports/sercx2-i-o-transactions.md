---
title: SerCx2 I/O 事务
description: SerCx2 简化了读取 (的处理 IRP_MJ_READ) 并 (IRP_MJ_WRITE 串行控制器驱动程序的) 请求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7f41e1cc25fe80e9066263ed735be20a2f3c2ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804967"
---
# <a name="sercx2-io-transactions"></a>SerCx2 I/O 事务

SerCx2 简化了对串行控制器驱动程序的读取 ([**irp \_ mj \_ read**](/previous-versions/ff546883(v=vs.85))) 和写入 ([**IRP \_ mj \_ 写入**](/previous-versions/ff546904(v=vs.85))) 请求的处理。 为了响应读取或写入请求，SerCx2 向串行控制器驱动程序发出一个或多个 i/o 事务。 从驱动程序的角度来看，每个事务都是一个简单且完整的 i/o 操作。

## <a name="in-this-section"></a>在本节中

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
<td><p><a href="overview-of-sercx2-i-o-transactions.md" data-raw-source="[Overview of SerCx2 I/O Transactions](overview-of-sercx2-i-o-transactions.md)">SerCx2 I/O 事务概述</a></p></td>
<td><p>SerCx2 通过向串行控制器驱动程序发出一个或多个 i/o 事务来处理来自客户端的读取或写入请求。 此驱动程序将每个事务视为自包含的 i/o 操作，该操作在串行控制器和请求中的数据缓冲区之间传输数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-pio-receive-transactions.md" data-raw-source="[SerCx2 PIO-Receive Transactions](sercx2-pio-receive-transactions.md)">SerCx2 PIO-Receive 事务</a></p></td>
<td><p>SerCx2 要求所有串行控制器驱动程序都实现对使用程控 i/o (PIO) 的接收事务的支持。 若要启动 PIO 接收事务，SerCx2 将调用驱动程序的 <a href="/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer" data-raw-source="[&lt;em&gt;EvtSerCx2PioReceiveReadBuffer&lt;/em&gt;](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)"><em>EvtSerCx2PioReceiveReadBuffer</em></a> 事件回调函数并将读取缓冲区作为参数提供。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-pio-transmit-transactions.md" data-raw-source="[SerCx2 PIO-Transmit Transactions](sercx2-pio-transmit-transactions.md)">SerCx2 PIO-Transmit 事务</a></p></td>
<td><p>SerCx2 要求所有串行控制器驱动程序实现对使用程控 i/o (PIO) 的传输事务的支持。 若要启动 PIO 传输事务，SerCx2 将调用驱动程序的 <a href="/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer" data-raw-source="[&lt;em&gt;EvtSerCx2PioTransmitWriteBuffer&lt;/em&gt;](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)"><em>EvtSerCx2PioTransmitWriteBuffer</em></a> 事件回调函数并将写入缓冲区作为参数提供。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-system-dma-receive-transactions.md" data-raw-source="[SerCx2 System-DMA-Receive Transactions](sercx2-system-dma-receive-transactions.md)">SerCx2 System-DMA-Receive 事务</a></p></td>
<td><p>某些串行控制器驱动程序实现对使用系统 DMA 控制器的接收事务的支持。 此类支持是可选的，但可以通过在长时间数据传输中免除使用程控 i/o (PIO) ，从而提高性能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-system-dma-transmit-transactions.md" data-raw-source="[SerCx2 System-DMA-Transmit Transactions](sercx2-system-dma-transmit-transactions.md)">SerCx2 System-DMA-Transmit 事务</a></p></td>
<td><p>某些串行控制器驱动程序实现对使用系统 DMA 控制器的传输事务的支持。 此类支持是可选的，但可以通过在长时间数据传输中免除使用程控 i/o (PIO) ，从而提高性能。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-custom-receive-transactions.md" data-raw-source="[SerCx2 Custom-Receive Transactions](sercx2-custom-receive-transactions.md)">SerCx2 Custom-Receive 事务</a></p></td>
<td><p>某些串行控制器硬件可能会实现 PIO 或系统 DMA 以外的数据传输机制，以便从串行控制器读取数据。 串行控制器驱动程序可以支持自定义接收事务，以使 SerCx2 可以使用此数据传输机制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-custom-transmit-transactions.md" data-raw-source="[SerCx2 Custom-Transmit Transactions](sercx2-custom-transmit-transactions.md)">SerCx2 Custom-Transmit 事务</a></p></td>
<td><p>某些串行控制器硬件可能会实现一种数据传输机制，而不是使用 PIO 或系统 DMA 向串行控制器写入数据。 串行控制器驱动程序可以支持自定义传输事务，以使 SerCx2 可以使用此数据传输机制。</p></td>
</tr>
</tbody>
</table>
