---
title: 从 CLFS 流读取数据记录
description: 从 CLFS 流读取数据记录
ms.assetid: 46e583c5-9f12-4f05-8f11-683ac428313a
keywords:
- 常见日志文件系统 WDK 内核，数据记录
- CLFS WDK 内核，数据记录
- 数据记录 WDK CLFS
- 读取数据记录
- 读取前向 WDK CLFS
- 转发读取 WDK CLFS
- 读取向后 WDK CLFS
- 向后读取 WDK CLFS
- 上一个 Lsn WDK CLFS
- 撤消的下一步 Lsn WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a83d13ff1d5dfac77e0dd5e9430f0510124a1c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378754"
---
# <a name="reading-data-records-from-a-clfs-stream"></a>从 CLFS 流读取数据记录


有两种类型的公用日志文件系统 (CLFS) 流中的记录： 数据记录，并重新开始记录。 本主题说明如何从流中读取的数据记录的序列。 有关如何读取重新启动记录的信息，请参阅[读取重新启动记录从 CLFS Stream](reading-restart-records-from-a-clfs-stream.md)。

有多个变体从流读取的数据记录的序列。 可以指定记录从流中向前读取，也可以向后阅读链的链接的记录。

对于阅读一系列数据记录的所有变体，完成以下步骤。

1.  调用[ **ClfsReadLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadlogrecord)获取读取的上下文和序列中的第一个数据记录。

2.  传递到步骤 1 中获取的读取的上下文[ **ClfsReadNextLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadnextlogrecord)重复以获取序列中的剩余数据记录。

**谨慎**  读取上下文不是线程安全。 客户端负责序列化上下文的读取权限。

 

以下子主题讨论读取不同类型的记录序列和链的详细信息。

### <a name="reading-forward-from-a-specified-data-record"></a>从指定的数据记录向前读取

若要读取前滚中 CLSF 流 （从所选的数据记录），必须创建具有其模式的读取的上下文设置为**ClfsContextForward**。 若要创建读取的上下文和读取 （在您阅读的集） 的第一个记录，请调用**ClfsReadLogRecord**下表中所示。

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
<td><p>提供你想要读取的第一个记录的 LSN。 这必须是数据记录，而不重新开始记录的 LSN。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p>提供的值<strong>ClfsContextForward</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>接收的记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>收到的记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>收到的记录类型。 此值是一组指示该记录的各种功能的标志。 记录是一个数据记录，因此，你收到的值应具有 ClfsDataRecord 标志设置且 ClfsRestartRecord 标志清除。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录撤消的下一步的 LSN。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的上一个 LSN。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>接收到不透明的读取上下文的指针。 使用读取的上下文读取后面的记录。</p></td>
</tr>
</tbody>
</table>

 

获取读取的上下文和第一条记录后，你可以通过调用获取流中的后续记录**ClfsReadNextLogRecord**重复。 在流中，有更多的数据记录时**ClfsReadNextLogRecord**将返回状态\_最终\_OF\_文件。 下表显示了如何设置和解释参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数名称</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvReadContext</em></p></td>
<td><p>提供指向从收到的读取上下文<strong>ClfsReadLogRecord</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>接收的记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbBuffer</em></p></td>
<td><p>收到的记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>提供的值<strong>ClfsDataRecord</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录的撤消的下一步 LSN 字段。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的上一个 LSN 字段。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>接收已读取的数据记录的 LSN。</p></td>
</tr>
</tbody>
</table>

 

### <a name="reading-a-chain-of-data-records-linked-by-the-previous-lsn"></a>上一个 LSN 读取的数据记录的链链接

CLFS 流中写入的数据记录，可以将数据记录的上一个 LSN 设为以前向流写入任何记录的 LSN。 通过设置上一个 LSN，可以创建更高版本可以按相反的顺序遍历的相关记录的链。 例如，假设您正在执行数据库事务，您必须编写几个 CLFS 日志记录来描述该事务所做的更新。 每次写入一条描述事务更新的日志记录可以设置的记录的上一个 LSN 为描述该事务所做的更新的上一个日志记录的 LSN。

假设您编写的数据记录，其中由其上一个 Lsn 链接链。 若要读取的记录链，必须创建具有其模式设置为的读取的上下文**ClfsContextPrevious**。 若要创建读取的上下文和读取链中的第一个记录，请调用**ClfsReadLogRecord**下表中所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数名称</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvMarshalContext</em></p></td>
<td><p>提供指向封送处理区域的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnFirst</em></p></td>
<td><p>提供链中的第一个记录的 LSN。 这必须是数据记录，而不重新开始记录的 LSN。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p>提供的值<strong>ClfsContextPrevious</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>接收的记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>收到的记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>收到的记录类型。 此值是一组指示该记录的各种功能的标志。 记录是一个数据记录，因此，你收到的值应具有 ClfsDataRecord 标志设置且 ClfsRestartRecord 标志清除。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录撤消的下一步的 LSN。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的上一个 LSN。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>接收到不透明的读取上下文的指针。 使用读取的上下文读取链中以前的记录。</p></td>
</tr>
</tbody>
</table>

 

读取的上下文和第一条记录后，可以通过调用读取链中的剩余记录**ClfsReadNextLogRecord**重复。 下表显示了如何设置和解释参数。

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
<td><p>提供指向从收到的读取上下文<strong>ClfsReadLogRecord</strong>。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>接收的记录数据。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbBuffer</em></p></td>
<td><p>收到的记录数据的大小。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>提供的值<strong>ClfsDataRecord</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>接收数据记录撤消的下一步的 LSN。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>接收数据记录的上一个 LSN。 不需要再继续阅读链，因此可以忽略此值。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>接收已读取的数据记录的 LSN。</p></td>
</tr>
</tbody>
</table>

 

在进行重复的调用**ClfsReadNextLogRecord**，您的调用的序列将通过以下方式之一结束。

-   最终将读取数据记录具有其设置为 CLFS 的上一个 LSN\_LSN\_无效。 下次调用**ClfsReadNextLogRecord**，它将返回状态\_最终\_OF\_文件。

-   最终将读取数据记录的 lsn 小于这两种基本的流的上一个 LSN 和[*存档尾数据*](clfs-terminology.md#kernel-clfs-term-archive-tail)的流。 下次调用**ClfsReadNextLogRecord**，它将返回状态\_日志\_启动\_OF\_日志。

### <a name="reading-a-chain-of-data-records-linked-by-the-undo-next-lsn"></a>读取的数据记录的链链接的撤消下一个 LSN

CLFS 流中写入的数据记录，可以将数据记录的撤消的下一步 LSN 设为以前向流写入任何记录的 LSN。 通过设置撤消的下一步 LSN，可以创建一系列可以按相反的顺序遍历的相关记录。 有关创建和解释撤消的下一步链的详细信息，请参阅[CLFS 日志序列号](clfs-log-sequence-numbers.md)。

假设您编写的数据记录，其中由其撤消的下一步 Lsn 链接链。 若要读取的记录链，必须调用[ **ClfsReadLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadlogrecord)若要创建具有模式的读取的上下文设置为**ClfsContextUndoNext**。 之后，该过程是相同的读取链接的上一个 Lsn （在本主题前面介绍） 的链。

### <a name="reading-a-chain-of-data-records-linked-by-the-user-lsn"></a>由用户 LSN 读取的数据记录的链链接

除了由上一个 Lsn 和撤消的下一步 Lsn 链接链，可以创建链接的记录数据中嵌入自己 Lsn 的链。

假设您编写的链的链接的 Lsn 已在自身的记录数据中存储的数据记录。 若要读取的记录链，必须创建具有其模式设置为的读取的上下文**ClfsContextPrevious**或**ClfsContextUndoNext**。 创建读取的上下文并通过调用获取链中的最近写入的记录[ **ClfsReadLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadlogrecord)。 然后调用[ **ClfsReadNextLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadnextlogrecord)重复以获取链中以前的记录。 每次调用**ClfsReadNextLogRecord**，请设置*plsnUser*到链中的上一记录的 LSN 的参数。 在中提供的 LSN *plsnUser*替代当前记录的上一个 LSN 或撤消的下一步 LSN 字段中存储任何值。

请注意，您可以仅向后移动在流中调用时**ClfsReadNextLogRecord**读取记录链。 在中提供的 LSN *plsnUser*必须早于链中的当前记录的 LSN。

 

 




