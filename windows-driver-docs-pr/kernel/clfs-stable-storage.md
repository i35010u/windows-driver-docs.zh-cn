---
title: CLFS 稳定存储
description: CLFS 稳定存储
keywords:
- 公用日志文件系统 WDK 内核，稳定存储
- CLFS WDK 内核，稳定存储
- 稳定存储 WDK CLFS
- 存储 WDK CLFS
- 容器 WDK CLFS
- 逻辑容器 WDK CLFS
- 物理容器 WDK CLFS
- 日志 i/o 块 WDK CLFS
- 阻止 WDK CLFS
- 块偏移 WDK CLFS
- 记录 WDK CLFS
- 物理日志 WDK CLFS
- 容器标识符 WDK CLFS
- 记录序列号 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eafa329c4e1767ee9be2bfd4e6e22dd06062738e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825661"
---
# <a name="clfs-stable-storage"></a>CLFS 稳定存储





将记录写入公用日志文件系统 (CLFS) 流时，该记录将被放入日志 i/o 块 (，该块会出现在 "可变内存" 的封送) 区域中。 CLFS 会定期刷新从封送区到稳定存储（如磁盘）的日志 i/o 块。 在稳定存储设备上，日志包含一组容器，每个容器都是物理介质上的一个连续区。 构成流的稳定存储的容器集合称为 *日志* 或 *物理日志*。

下图说明了一个容器。

![阐释容器、块和记录的关系图](images/clfscontainers.gif)

上图说明了包含三个日志 i/o 块的容器。 第一个日志 i/o 块包含三条记录，第二个记录包含5条记录，第三个记录包含两条记录。 如图所示，每个日志 i/o 块的开头始终与稳定存储介质上某个扇区的开头对齐。 请注意，稳定存储上的日志 i/o 块的大小各不相同。

CLFS 使用一组三个数字来定位日志中的记录。

-   *容器标识符* 标识保存记录的容器。

-   *块偏移* 为包含记录的日志 i/o 块的开始位置提供了在容器中的字节偏移量。

-   *记录序列* 号用于标识日志 i/o 块中的记录。

CLFS 日志记录 (LSN) 的日志序列号实际上包含三条信息：容器标识符、块偏移量和记录序列号。 但是，为记录客户端提供的 Lsn 包含 *逻辑容器标识符* ，CLFS 必须映射到物理容器标识符，然后才能访问稳定存储上的记录。

CLFS 使用逻辑容器标识符，使客户端能够将日志记录写入正在进行的容器序列（事实上，实际上是回收物理容器）。

假设日志包含三个容器，且一个客户端将 CLFS 记录写入日志。 下面的方案演示如何回收容器。

1.  客户端编写足够的日志记录来填充所有三个容器。

2.  客户端通过调用 [**ClfsAdvanceLogBase**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsadvancelogbase) 或 [**ClfsWriteRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)将日志基 (设置为容器2中的其中一条记录 ) 。 这样，客户端就会说它不再需要容器1中的记录。

3.  客户端将另一条记录写入日志，并获取新写入记录的 LSN。 该 LSN 中的逻辑容器标识符是4。 将记录刷新到稳定存储时，客户端在逻辑容器4中看到的记录将会移到 "物理容器 1"。

下图说明了该方案;其中显示了如何将逻辑容器的客户端序列映射到稳定存储上的物理容器。

![阐释逻辑和物理容器的关系图](images/clfslogicalcontainers.gif)

逻辑容器标识符、块偏移量和记录序列号以这种方式存储在 LSN 中，特定流的 Lsn 始终形成严格递增的序列。 也就是说，写入到流中的日志记录的逻辑容器标识符) 的 LSN (始终大于之前写入到此同一流的日志记录的 Lsn。 Lsn 是一种双重用途： 1) 它们为流的客户端提供排序的记录标识符序列，2) 它们为 CLFS 提供稳定存储上的记录位置。

给定记录的 LSN，可以通过调用以下函数来提取逻辑容器标识符、块偏移量和记录序列号。

[**ClfsLsnContainer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsncontainer)

[**ClfsLsnBlockOffset**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnblockoffset)

[**ClfsLsnRecordSequence**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnrecordsequence)

逻辑容器标识符是一个32位的数字，因此有 2 ^ 32 个可能的逻辑容器标识符，它们在0x0 到0xFFFFFFFF 的范围内。 一个流最多可以有 2 ^ 32 个逻辑容器。

块偏移量存储在 LSN 的23位中，但 **ClfsLsnBlockOffset** 返回一个32位的数字，该数字与稳定存储介质的扇区大小相匹配。 块偏移量始终为512的倍数。 此外，块偏移量与稳定存储介质的扇区大小一致。 例如，如果扇区大小为1024字节，则块偏移将是1024的倍数。

记录序列号是一个9位数字，因此，有 2 ^ 9 (512) 可能的记录序列号，并且在0x0 到0x1FF 的范围内。 日志 i/o 块最多可以有512个记录。

 

