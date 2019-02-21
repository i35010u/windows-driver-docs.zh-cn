---
title: CLFS 日志序列号
description: CLFS 日志序列号
ms.assetid: 4637fa0c-2f19-4f0c-bf13-f4ccac2e7284
keywords:
- 常见日志文件系统 WDK 内核，日志序列号
- CLFS WDK 内核，日志序列号
- 日志序列号 WDK CLFS
- Lsn WDK CLFS
- 基 Lsn WDK CLFS
- 最后一个 Lsn WDK CLFS
- 上一个 Lsn WDK CLFS
- 撤消的下一步 Lsn WDK CLFS
- 活动流部分 WDK CLFS
- 流的活动部分 WDK CLFS
- 流 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 144fe5b98a359c4e6ee01c50674c8b9d7e6e2950
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534868"
---
# <a name="clfs-log-sequence-numbers"></a>CLFS 日志序列号





在公用日志文件系统 (CLFS)，由一个日志序列号 (LSN) 唯一标识给定流中的每个日志记录。 当向流写入一条记录时，你获得标识以供将来参考该记录的 LSN。

为特定流窗体创建严格递增序列 Lsn。 即，分配到给定流中的日志记录的 LSN 大于始终分配给日志记录之前写入该同一个流 Lsn。 以下函数是可用于比较给定流中的日志记录 Lsn。

[**ClfsLsnNull**](https://msdn.microsoft.com/library/windows/hardware/ff541609)

[**ClfsLsnEqual**](https://msdn.microsoft.com/library/windows/hardware/ff541590)

[**ClfsLsnGreater**](https://msdn.microsoft.com/library/windows/hardware/ff541595)

[**ClfsLsnLess**](https://msdn.microsoft.com/library/windows/hardware/ff541608)

常量 CLFS\_LSN\_为 NULL 且 CLFS\_LSN\_无效是所有有效的 Lsn 的下限和上限边界。 任何有效的 LSN 是大于或等于 CLFS\_LSN\_NULL。 此外，任何有效的 LSN 都是严格小于 CLFS\_LSN\_无效。 请注意该 CLFS\_LSN\_NULL 是有效的 LSN，而 CLFS\_LSN\_无效不是有效的 LSN。 即便如此，您可以比较 CLFS\_LSN\_无效而其他 Lsn，在前面的列表中使用的功能。

对于每个流，CLFS 跟踪的两个特殊 Lsn： 基准 LSN 和最后一个 LSN。 此外，每个单独的日志记录具有两个特殊 Lsn （上一个 LSN 和撤消的下一步 LSN），可用于创建链的相关的日志记录。 以下部分介绍了这些特殊的 Lsn，在详细信息。

### <a name="base-lsn"></a>基准 LSN

当客户端写入流中的第一条记录时，CLFS 设置基准 LSN 与该第一个记录的 LSN。 直到客户端更改它，基准 LSN 保持不变。 当流的客户端不再需要在流中的某个特定点之前记录时，他们可以通过调用更新基准 LSN [ **ClfsAdvanceLogBase** ](https://msdn.microsoft.com/library/windows/hardware/ff540773)或[ **ClfsWriteRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541770)。 例如，如果客户端不再需要的前五个日志记录，它们可以设置基准 LSN 为第六个记录的 LSN。

### <a name="last-lsn"></a>最后一个 LSN

由于客户端将记录写入流，CLFS 会调整的最后一个 LSN，以便它始终写入的最后一个记录的 LSN。 如果客户端不再需要记录在流中的某个特定点后他们可以通过调用更新最后一个 LSN [ **ClfsSetEndOfLog**](https://msdn.microsoft.com/library/windows/hardware/ff541753)。 例如，如果客户端不再需要写入的第十个记录的任何记录，它们可以通过设置为第十个记录的 LSN 的最后一个 LSN 截断流。

### <a name="active-portion-of-a-stream"></a>流的活动部分

*活动部分*流是一个流，其中包含该记录指向的基准 LSN 开始的部分，以记录指向最后一个 LSN 的结尾。 下图说明了如何基准 LSN 和最后一个 LSN 描述流的活动部分。

![说明 clfs 流的活动部分的关系图](images/clfsactivelog.gif)

**请注意**  如果流已存档尾数据，流的活动部分开始指向的基准 LSN 或存档尾数据的记录，两者中较小。 有关存档的详细信息，请参阅[CLFS 支持存档](clfs-support-for-archiving.md)。

 

### <a name="previous-lsn"></a>上一个 LSN

假设两个活动数据库事务 （事务 A 和事务 B） 在同一时间记录写入相同的流。 每次 a 记录的事务的写入，它将设置记录的上一个 LSN 为写入事务 A.的上一个日志记录的 LSN该窗体日志记录，属于事务 A，可以按相反的顺序遍历的链。 链结尾写入由事务 A 已设置为 CLFS 其上一个 LSN 的第一个日志记录\_LSN\_无效。 类似地，事务 B 通过设置它将写入每条日志记录的上一个 LSN 创建其自己的日志记录链。

下图中的箭头说明日志记录的上一个 LSN 如何指向属于特定事务链中的上一个记录。

![说明上一个 lsn 指针的关系图](images/clfsrecordchains.gif)

### <a name="undo-next-lsn"></a>Undo-next LSN

假设事务使易失性内存中的数据对象的五个更新将回滚的第四个和第五个更新，并将更新第六个。 事务进行了更新，因为它将写入日志记录 1、 2、 3、 4、 5，5、 4 和 6。 日志记录 1 至 5 描述更新 1 至步骤 5 所做的更改。 记录 5 介绍了在 update 5，回滚所做的更改并记录 4 介绍了在更新 4 回滚所做的更改。 最后，记录 6 介绍了更新 6 所做的更改。 请注意，数字 1、 2、 3、 4、 5，5、 4 和 6 不是 Lsn 的日志记录中。它们只是用于命名在本讨论中的日志记录的数字。

日志记录 5，并 4，描述回滚，请调用补偿日志记录 (Clr)。 前身 （在由事务写入的记录） 的事务集的每个 CLR 撤消的下一步 LSN 的日志记录的更新时只需回滚 （撤消）。 在此示例中，记录 5 的撤消的下一步 LSN 是 4，记录的 LSN 和记录 4 的撤消的下一步 LSN 是第三条记录的 LSN。

普通的日志记录 （那些不是 Clr），必须设置为上一个日志记录由事务写入其撤消下一个 Lsn。 也就是说，对于普通的记录，撤消下一个 LSN 和上一个 LSN 是相同的。

现在，假设存在在系统出现故障，重新启动恢复过程，整个事务必须回滚。 恢复代码读取日志记录 6。 记录 6 中的数据指示记录 6 是普通的记录 (不 CLR)，因此恢复代码将回滚更新 6。 然后恢复代码会检查记录 6 的撤消的下一步 LSN，并发现它指向记录 4。 记录 4 中的数据指示它是一个 CLR，因此恢复代码不会回滚 update 4。 相反，它会检查记录 4 的撤消的下一步 LSN，并查找指向第三条记录。 第三条记录不是一个 CLR，因此恢复代码将回滚更新 3。 5 和 4 的更新不会回滚在恢复期间由于他们已回滚在普通的前向处理过程。 恢复代码将回滚最后更新 2 和 1。

下图中的箭头说明如何撤消的下一步 LSN 提供一种机制，可以使用恢复代码跳过已返回回滚其更新的记录。

![说明上一个 lsn 和撤消的下一步 lsn 指针的关系图](images/clfsundonext.gif)

 

 




