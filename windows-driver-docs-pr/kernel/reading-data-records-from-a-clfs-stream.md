---
title: 从 CLFS 流读取数据记录
description: 从 CLFS 流读取数据记录
keywords:
- 公用日志文件系统 WDK 内核，数据记录
- CLFS WDK 内核，数据记录
- 数据记录 WDK CLFS
- 读取数据记录
- 读取转发 WDK CLFS
- 向前读取 WDK CLFS
- 阅读反向 WDK CLFS
- 向后阅读 WDK CLFS
- 上一个 Lsn WDK CLFS
- 撤消-下一个 Lsn WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3134e04ebfe2d6bce1516b6721612bfdc20c604
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803791"
---
# <a name="reading-data-records-from-a-clfs-stream"></a>从 CLFS 流读取数据记录


公用日志文件系统中有两种类型的记录 (CLFS) 流：数据记录和重新启动记录。 本主题说明如何从流中读取数据记录序列。 有关如何读取重新启动记录的信息，请参阅 [从 CLFS 流中读取重新启动记录](reading-restart-records-from-a-clfs-stream.md)。

从流中读取一系列数据记录有几种不同的形式。 您可以从指定的记录读取流中的，也可以沿链接的记录链向后阅读。

对于读取数据记录序列的所有变体，请完成以下步骤。

1.  调用 [**ClfsReadLogRecord**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadlogrecord) 以获取读取上下文和序列中的第一个数据记录。

2.  将你在步骤1中获取的读取上下文传递到重复 [**ClfsReadNextLogRecord**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadnextlogrecord) 以获取序列中剩余的数据记录。

**警告**  读取上下文不是线程安全的。 客户端负责序列化对读取上下文的访问。

 

以下子主题介绍读取不同类型的记录序列和链的详细信息。

### <a name="reading-forward-from-a-specified-data-record"></a>向前读取指定的数据记录

若要从所选) 的数据记录开始 (在 CLSF 流中进行读取，必须创建将其模式设置为 **ClfsContextForward** 的读取上下文。 若要创建读取上下文并读取已选择读取的集合中的第一条记录 () ，请调用 **ClfsReadLogRecord** ，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数名称</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvMarshalContext</em></p></td>
<td><p>提供指向封送处理区域的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnFirst</em></p></td>
<td><p>提供要读取的第一条记录的 LSN。 这必须是数据记录的 LSN，而不是重新启动记录。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p>提供值 <strong>ClfsContextForward</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>接收记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>接收记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>接收记录类型。 此值是一组指示记录的各种功能的标志。 记录是数据记录，因此，接收的值应设置 ClfsDataRecord 标志，并清除 ClfsRestartRecord 标志。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录的后向后 LSN。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的前一个 LSN。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>接收指向不透明读取上下文的指针。 使用读取上下文读取后续记录。</p></td>
</tr>
</tbody>
</table>

 

获取读取上下文和第一条记录后，可以通过重复调用 **ClfsReadNextLogRecord** 来获取流中的后续记录。 如果流中没有更多的数据记录， **ClfsReadNextLogRecord** 将返回 \_ \_ 文件的状态结尾 \_ 。 下表显示了如何设置和解释参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数名称</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvReadContext</em></p></td>
<td><p>提供一个指向从 <strong>ClfsReadLogRecord</strong>收到的读取上下文的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>接收记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbBuffer</em></p></td>
<td><p>接收记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>提供 <strong>ClfsDataRecord</strong>的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录的 "撤消-下一个 LSN" 字段。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的前 LSN 字段。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>接收读取的数据记录的 LSN。</p></td>
</tr>
</tbody>
</table>

 

### <a name="reading-a-chain-of-data-records-linked-by-the-previous-lsn"></a>读取前面的 LSN 链接的数据链

向 CLFS 流写入数据记录时，可以将数据记录的前一个 LSN 设置为之前写入到流中的任何记录的 LSN。 通过设置前一个 LSN，你可以创建一个可在以后反向遍历的相关记录链。 例如，假设您要执行数据库事务，并且您必须编写多个 CLFS 日志记录，以描述由事务进行的更新。 每次编写描述事务更新的日志记录时，都可以将记录的前一个 LSN 设置为之前的日志记录的 LSN，该记录描述了同一事务所做的更新。

假设您已经编写了一个由其上一个 Lsn 链接的数据记录链。 若要读取记录链，必须创建将其模式设置为 **ClfsContextPrevious** 的读取上下文。 若要创建读取上下文并读取该链中的第一条记录，请调用 **ClfsReadLogRecord** ，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数名称</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvMarshalContext</em></p></td>
<td><p>提供指向封送处理区域的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnFirst</em></p></td>
<td><p>提供链中第一条记录的 LSN。 这必须是数据记录的 LSN，而不是重新启动记录。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p>提供 <strong>ClfsContextPrevious</strong>的值。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>接收记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>接收记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>接收记录类型。 此值是一组指示记录的各种功能的标志。 记录是数据记录，因此，接收的值应设置 ClfsDataRecord 标志，并清除 ClfsRestartRecord 标志。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录的后向后 LSN。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的前一个 LSN。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>接收指向不透明读取上下文的指针。 使用读取上下文读取链中的以前记录。</p></td>
</tr>
</tbody>
</table>

 

获得读取上下文和第一条记录后，可以通过重复调用 **ClfsReadNextLogRecord** 来读取该链中的其余记录。 下表显示了如何设置和解释参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数名称</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvReadContext</em></p></td>
<td><p>提供一个指向从 <strong>ClfsReadLogRecord</strong>收到的读取上下文的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>接收记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbBuffer</em></p></td>
<td><p>接收记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>提供 <strong>ClfsDataRecord</strong>的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录的后向后 LSN。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的前一个 LSN。 不需要此值即可继续读取链，因此可将其忽略。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>接收读取的数据记录的 LSN。</p></td>
</tr>
</tbody>
</table>

 

当你重复调用 **ClfsReadNextLogRecord** 时，你的调用序列将以下列方式之一结束。

-   最终，将读取其前一个 LSN 设置为 CLFS LSN 无效的数据 \_ 记录 \_ 。 下一次调用 **ClfsReadNextLogRecord** 时，它将返回 \_ \_ 文件的状态结尾 \_ 。

-   最终，您将读取一个数据记录，其中的前一个 LSN 小于流的基本 LSN 和流的 [*存档结尾*](clfs-terminology.md#kernel-clfs-term-archive-tail) 。 下一次调用 **ClfsReadNextLogRecord** 时，它将返回 \_ \_ 日志的状态日志开头 \_ \_ 。

### <a name="reading-a-chain-of-data-records-linked-by-the-undo-next-lsn"></a>读取由 "撤消下一个" LSN 链接的数据记录链

向 CLFS 流写入数据记录时，可以将数据记录的 "撤消-下一个" LSN 设置为之前写入到流中的任何记录的 LSN。 通过设置 "撤消下一步" LSN，可以创建可按相反顺序进行遍历的一系列相关记录。 有关创建和解释 "撤消下一步" 链的详细信息，请参阅 [CLFS 日志序列号](clfs-log-sequence-numbers.md)。

假设您已经编写了一系列由其 Lsn 链接的数据记录。 若要读取记录链，必须调用 [**ClfsReadLogRecord**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadlogrecord) 来创建其模式设置为 **ClfsContextUndoNext** 的读取上下文。 之后，此过程与读取前面 (本主题中所述的上一个 Lsn) 链接的链完全相同。

### <a name="reading-a-chain-of-data-records-linked-by-the-user-lsn"></a>读取用户 LSN 链接的数据记录链

除了由上一个 Lsn 和 undo Lsn 链接的链，你还可以创建你自己的 Lsn 的链接，并将其嵌入到记录数据中。

假设您已经编写了一个数据链，这些数据记录由存储在记录数据本身中的 Lsn 链接。 若要读取记录链，必须创建将其模式设置为 **ClfsContextPrevious** 或 **ClfsContextUndoNext** 的读取上下文。 通过调用 [**ClfsReadLogRecord**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadlogrecord)创建读取上下文并在链中获取最新写入的记录。 然后，重复调用 [**ClfsReadNextLogRecord**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadnextlogrecord) 以获取链中的前一条记录。 每次调用 **ClfsReadNextLogRecord** 时，请将 *plsnUser* 参数设置为链中上一条记录的 LSN。 在 *plsnUser* 中提供的 LSN 会重写存储在当前记录的前一个 lsn 或 UNDO next lsn 字段中的所有值。

请注意，在调用 **ClfsReadNextLogRecord** 读取记录链时，只能在流中向后移动。 在 *plsnUser* 中提供的 lsn 必须小于链中当前记录的 lsn。

 

