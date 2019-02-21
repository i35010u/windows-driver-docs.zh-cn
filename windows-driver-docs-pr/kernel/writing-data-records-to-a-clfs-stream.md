---
title: 数据记录写入 CLFS Stream
description: 数据记录写入 CLFS Stream
ms.assetid: 22bd6d39-b777-4a62-85b1-3d03a7144f7a
keywords:
- 常见日志文件系统 WDK 内核，数据记录
- CLFS WDK 内核，数据记录
- 数据记录 WDK CLFS
- 保留的空间 WDK CLFS
- 对齐的项 WDK CLFS
- 编写数据记录
- 缓冲区 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f817b8406a1d5ad041ba418004b09e1ed9f13e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534463"
---
# <a name="writing-data-records-to-a-clfs-stream"></a>数据记录写入 CLFS Stream





有两种类型的公用日志文件系统 (CLFS) 流中的记录： 数据记录，并重新开始记录。 本主题说明如何将数据记录写入到流。 有关如何编写重启记录的信息，请参阅[重新启动将记录写入 CLFS Stream](writing-restart-records-to-a-clfs-stream.md)。

可以将数据记录写入 CLFS 流之前，必须通过调用创建封送处理区域[ **ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)。 然后可以将记录追加到封送处理区域 （这是在易失性内存中），和 CLFS 将定期刷新记录到稳定存储。

有多个变体向流写入数据记录。 例如，可以保留空间提前，然后写入几条记录，或者您可以编写记录，而保留空间。 你可以请求的记录写入到封送处理区域会立即排队到稳定存储中，也可以让 CLFS 队列根据其策略的记录。

对于编写数据记录的所有变体，完成以下步骤。

1.  创建一个或多个数组[ **CLFS\_编写\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff541891)结构。 写入条目的每个结构将指向的缓冲区已填充的记录数据。

2.  调用[ **ClfsReserveAndAppendLog** ](https://msdn.microsoft.com/library/windows/hardware/ff541723)或[ **ClfsReserveAndAppendLogAligned**](https://msdn.microsoft.com/library/windows/hardware/ff541726)。

以下各小节中的表显示如何设置的参数**ClfsReserveAndAppendLog**上向流写入一条记录的多个变量。

### <a name="writing-a-single-data-buffer-to-a-stream"></a>向流写入一个数据缓冲区

假设你有想要写入到封送处理区域的单个数据缓冲区。 您愿意让记录刷新到稳定存储根据 CLFS 策略，并不希望记录为记录的任何链的一部分。 下表显示了如何在调用时设置的参数**ClfsReserveAndAppendLog**。

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
<td><p>一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff541891" data-raw-source="[&lt;strong&gt;CLFS_WRITE_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541891)"> <strong>CLFS_WRITE_ENTRY</strong> </a>结构。</p></td>
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
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p>一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff541824" data-raw-source="[&lt;strong&gt;CLFS_LSN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541824)"> <strong>CLFS_LSN</strong> </a>结构。 （这是记录的一个输出参数，它接收写入的 LSN）。</p></td>
</tr>
</tbody>
</table>

 

### <a name="reserving-space-for-a-set-of-clfs-log-records"></a>保留空间的一组 CLFS 日志记录

可以使用**ClfsReserveAndAppendLog**而无需实际编写的任何记录保留一系列日志记录的封送处理区域中的空间。 下表显示了如何设置参数以保留记录的空间。

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
<td><p>NULL</p></td>
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
<td><p>指向数组中元素的数目<em>rgcbReservation</em>。</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>指向 LONGLONG 类型化的变量的数组的指针。 数组中的每个元素是记录的大小 （字节） 为其保留空间。 请注意，这是此大小的数据部分的记录;无需包括标头或填充的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

 

**请注意**  封送处理区域中保留的空间的另一个方法是调用[ **ClfsAlignReservedLog** ](https://msdn.microsoft.com/library/windows/hardware/ff540779)跟[ **ClfsAllocReservedLog**](https://msdn.microsoft.com/library/windows/hardware/ff540782).

 

### <a name="writing-a-record-to-reserved-space"></a>将一个记录写入保留空间

假设您已经保留了其大小，以字节为单位，为 100、 200 和 300 的三条记录的空间。 封送处理区域的保留的记录计数为 3 到足以保留空间以容纳 600 字节的记录数据、 记录标头和所需的对齐方式的任何填充。

现在假设你想要编写其中一个记录到封送处理区域中的保留空间。 将减少保留的可用空间，并且保留记录计数将是 3 减为 2。 下表显示了如何在调用时设置的参数**ClfsReserveAndAppendLog**。

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
<td><p>指向数组的指针<strong>CLFS_WRITE_ENTRY</strong>结构。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>指向数组中元素的数目<em>rgWriteEntries</em>。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID 或撤消链中的上一记录的 LSN。 有关撤消链的详细信息，请参阅<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID 或上一个 LSN 链中的上一个日志记录的 LSN。 有关上一个 LSN 链接的详细信息，请参阅<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="even">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>CLFS_FLAG_USE_RESERVATION</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p>一个指向<strong>CLFS_LSN</strong>结构。 （这是记录的一个输出参数，它接收写入的 LSN）。</p></td>
</tr>
</tbody>
</table>

 

### <a name="writing-records-with-aligned-entries"></a>编写具有对齐项记录

假设你想要写入的记录具有三个写入条目。 写入条目的大小介于 300 和 500 个字节之间各不相同，但您需要在 512 字节边界上开始每个写入条目。 下表显示了如何设置的参数**ClfsReserveAndAppendLogAligned**函数。

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
<td><p>指向的三个 CLFS_WRITE_ENTRY 结构数组的指针。</p></td>
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
<td><p>CLFS_LSN_INVALID 或撤消链中的上一记录的 LSN。 有关撤消链的详细信息，请参阅<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID 或上一个 LSN 链中的上一个日志记录的 LSN。 有关上一个 LSN 链接的详细信息，请参阅<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS 日志序列号</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>rgcbReservation</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="odd">
<td><p><em>fFlags</em></p></td>
<td><p>零个或一些标志，用于指定刷新和保留的首选项的组合。</p></td>
</tr>
<tr class="even">
<td><p><em>plsn</em></p></td>
<td><p>指向 CLFS_LSN 结构的指针。 （这是记录的一个输出参数，它接收写入的 LSN）。</p></td>
</tr>
</tbody>
</table>

 

前面的表显示保留记录的空间和记录写入 CLFS 流上只有几个很大差异。 您将其他变体，请记住以下几点：执行的操作**ClfsReserveAndAppendLog** (或**ClfsReserveAndAppendLogAligned**) 是原子操作。 例如，可以使调用一次**ClfsReserveAndAppendLog** ，将为一条记录保留空间并将记录写入流。 操作 （保留、 写入） 对将作为一个整体成功或失败作为一个整体。

 

 




