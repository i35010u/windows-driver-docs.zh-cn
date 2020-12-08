---
title: 将数据记录写入 CLFS 流
description: 将数据记录写入 CLFS 流
keywords:
- 公用日志文件系统 WDK 内核，数据记录
- CLFS WDK 内核，数据记录
- 数据记录 WDK CLFS
- 保留空间 WDK CLFS
- 对齐的条目 WDK CLFS
- 写入数据记录
- 缓冲区 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0860aec911c19529becc0cdac46cf54d1fb5aaf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782599"
---
# <a name="writing-data-records-to-a-clfs-stream"></a>将数据记录写入 CLFS 流





公用日志文件系统中有两种类型的记录 (CLFS) 流：数据记录和重新启动记录。 本主题说明如何将数据记录写入到流中。 有关如何编写重新启动记录的信息，请参阅将 [重新启动记录写入到 CLFS 流](writing-restart-records-to-a-clfs-stream.md)。

必须先通过调用 [**ClfsCreateMarshallingArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)创建封送处理区域，然后才能将数据记录写入到 CLFS 流。 然后，你可以将记录追加到 () 的可变内存中的封送区，并且 CLFS 会定期将记录刷新到稳定的存储。

向流中写入数据记录有几种变化形式。 例如，可以提前保留空间，然后写入多条记录，也可以在不保留空间的情况下写入记录。 您可以请求将写入到封送区域的记录立即排队到稳定存储，也可以让 CLFS 根据记录的策略对记录进行排队。

对于写入数据记录的所有变体，请完成以下步骤。

1.  创建一个或多个 [**CLFS \_ 写入 \_ 条目**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_write_entry) 结构的数组。 每个写入条目结构都指向已使用记录数据填充的缓冲区。

2.  调用 [**ClfsReserveAndAppendLog**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog) 或 [**ClfsReserveAndAppendLogAligned**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlogaligned)。

以下小节中的表显示了如何将 **ClfsReserveAndAppendLog** 的参数设置为在将记录写入到流时有几种变化形式。

### <a name="writing-a-single-data-buffer-to-a-stream"></a>将单个数据缓冲区写入流

假设您有一个要写入到封送处理区域的数据缓冲区。 你愿意根据 CLFS 策略将记录刷新到稳定存储，并且不希望该记录成为任何记录链的一部分。 下表显示了在调用 **ClfsReserveAndAppendLog** 时如何设置参数。

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
<td><p>指向封送处理区域的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>指向 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_write_entry" data-raw-source="[&lt;strong&gt;CLFS_WRITE_ENTRY&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_write_entry)"><strong>CLFS_WRITE_ENTRY</strong></a> 结构的指针。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="even">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p>指向 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_lsn" data-raw-source="[&lt;strong&gt;CLFS_LSN&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_lsn)"><strong>CLFS_LSN</strong></a> 结构的指针。  (这是一个输出参数，用于接收所写入记录的 LSN ) </p></td>
</tr>
</tbody>
</table>

 

### <a name="reserving-space-for-a-set-of-clfs-log-records"></a>为一组 CLFS 日志记录保留空间

您可以使用 **ClfsReserveAndAppendLog** 在封送区为一组日志记录保留空间，而无需实际编写任何记录。 下表显示了如何将参数设置为保留记录空间。

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
<td><p>指向封送处理区域的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="even">
<td><p><em>cReserveRecords</em></p></td>
<td><p><em>RgcbReservation</em>指向的数组中的元素数目。</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>指向 LONGLONG 类型变量的数组的指针。 数组中的每个元素都是将保留空间的记录的大小（以字节为单位）。 请注意，这是记录的数据部分的大小;您不必包含标头或填充的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>

 

**注意**   在封送处理区域中保留空间的另一种方法是调用 [**ClfsAlignReservedLog**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsalignreservedlog) 后跟 [**ClfsAllocReservedLog**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsallocreservedlog)。

 

### <a name="writing-a-record-to-reserved-space"></a>向保留空间写入记录

假设您已经为三个记录保留了空间，这些记录的大小（以字节为单位）为100、200和300。 "封送处理" 区域的保留记录计数为3，保留空间足以保存600字节的记录数据、记录标头和对齐所需的任何填充。

现在，假设您想要将这些记录中的一个记录写入到 "封送" 区域中的保留空间。 将减少可用的保留空间，并且保留的记录计数将从3减少到2。 下表显示了在调用 **ClfsReserveAndAppendLog** 时如何设置参数。

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
<td><p>指向封送处理区域的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>指向 <strong>CLFS_WRITE_ENTRY</strong> 结构的数组的指针。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p><em>RgWriteEntries</em>指向的数组中的元素数目。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID 或撤消链中上一条记录的 LSN。 有关撤消链的详细信息，请参阅 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID 或前一个 LSN 链中以前的日志记录的 LSN。 有关前一个 LSN 链的详细信息，请参阅 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="even">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>CLFS_FLAG_USE_RESERVATION</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p>指向 <strong>CLFS_LSN</strong> 结构的指针。  (这是一个输出参数，用于接收所写入记录的 LSN ) </p></td>
</tr>
</tbody>
</table>

 

### <a name="writing-records-with-aligned-entries"></a>用对齐项写入记录

假设要编写包含三个写入项的记录。 写入条目的大小大小介于300到500字节之间，但要求每个写入条目都在512字节边界处开始。 下表显示了如何设置 **ClfsReserveAndAppendLogAligned** 函数的参数。

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
<td><p>指向封送处理区域的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>指向三个 CLFS_WRITE_ENTRY 结构的数组的指针。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p><em>cbEntryAlignment</em></p></td>
<td><p>512</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID 或撤消链中上一条记录的 LSN。 有关撤消链的详细信息，请参阅 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID 或前一个 LSN 链中以前的日志记录的 LSN。 有关前一个 LSN 链的详细信息，请参阅 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>rgcbReservation</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><em>fFlags</em></p></td>
<td><p>零个或一些指定刷新和保留首选项的标志组合。</p></td>
</tr>
<tr class="even">
<td><p><em>plsn</em></p></td>
<td><p>指向 CLFS_LSN 结构的指针。  (这是一个输出参数，用于接收所写入记录的 LSN ) </p></td>
</tr>
</tbody>
</table>

 

前面的表仅显示了在保留记录空间和将记录写入到 CLFS 流时的很多变化。 当你考虑其他变体时，请记住以下几点： **ClfsReserveAndAppendLog** (或) **ClfsReserveAndAppendLogAligned** 所执行的操作是原子的。 例如，可以对 **ClfsReserveAndAppendLog** 进行单一调用，将为记录保留空间并将记录写入流。  (保留的操作对，编写) 将作为一个整体或全部失败。

