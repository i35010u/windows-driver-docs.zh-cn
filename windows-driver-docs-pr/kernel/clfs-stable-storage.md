---
title: CLFS 稳定存储
description: CLFS 稳定存储
ms.assetid: d0ee4f22-9fba-47da-a9c9-eaf3a21feb36
keywords:
- 常见日志文件系统 WDK 内核，稳定存储
- CLFS WDK 内核，稳定存储
- 稳定的存储 WDK CLFS
- 存储 WDK CLFS
- 容器 WDK CLFS
- WDK CLFS 的逻辑容器
- 物理容器，WDK CLFS
- 日志 I/O 块 WDK CLFS
- 块 WDK CLFS
- 块偏移量 WDK CLFS
- 记录 WDK CLFS
- 物理日志 WDK CLFS
- 容器标识符 WDK CLFS
- 记录序列号 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1845d10b75f80205290b987b695c4dd17d32e691
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383342"
---
# <a name="clfs-stable-storage"></a>CLFS 稳定存储





公用日志文件系统 (CLFS) 流中写入一条记录，记录是易失性内存中放置在日志 I/O 块 （在封送处理的区域） 中。 我们会定期 CLFS 刷新日志从封送处理区域到稳定存储，如磁盘 I/O 块。 在稳定存储设备上，日志都包含一组容器，其中每个是物理介质上的连续区。 窗体的流的稳定存储容器的集合称为*日志*，或*物理日志*。

下图说明了一个容器。

![关系图演示容器、 块和记录](images/clfscontainers.gif)

上图说明了保存三个日志 I/O 块的容器。 第一个日志 I/O 块包含三条记录，第二个包含五个记录和第三个包含两条记录。 如图所示，每个日志 I/O 块的开头是始终符合稳定存储媒体上的扇区的开头。 请注意在稳定存储上的日志 I/O 块的大小不同。

CLFS 使用三个数字一组要在日志中查找一条记录。

-   *容器标识符*标识包含该记录的容器。

-   *块偏移量*提供保存记录的日志 I/O 块的开头的容器中的字节偏移量。

-   *记录序列*号标识日志 I/O 块中的记录。

CLFS 日志记录的日志序列号 (LSN) 实际上它拥有这三个条信息： 容器标识符、 块偏移量和记录的序列号。 但是，包含提供给客户端日志 Lsn*逻辑容器标识符*CLFS 必须映射到物理容器标识符然后才能访问稳定存储中的记录。

CLFS 使用逻辑容器标识符以使客户端日志记录的视图正写入时，容器，事实上，一个正在进行序列的物理容器正在进行更新。

假设日志中的三个容器，并且单个客户端 CLFS 记录写入日志。 以下方案说明如何回收可能是一个容器。

1.  客户端将写入足够的日志记录来填充所有三个容器。

2.  客户端设置的日志基 (通过调用[ **ClfsAdvanceLogBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsadvancelogbase)或[ **ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)。) 到一个容器中的记录2。 这样一来，客户端会说它不再需要容器 1 中的记录。

3.  客户端会向日志写入另一条记录，并获取返回新写入记录的 LSN。 该 LSN 中的逻辑容器标识符为 4。 当记录刷新到稳定存储中时，在客户端看到逻辑容器 4 中的记录将转到物理容器 1。

下图说明了方案;它显示如何的客户端一系列的逻辑容器映射到稳定存储上的物理容器。

![说明逻辑和物理容器的关系图](images/clfslogicalcontainers.gif)

逻辑容器标识符、 块偏移量和记录的序列号存储在中，为特定 Lsn 流始终窗体严格递增的序列的方式的 LSN。 也就是说，（与逻辑容器标识符） 的 LSN 的日志记录写入到流始终是大于以前写入到该相同的流的日志记录的 Lsn。 Lsn，然后，有双重用途：1），它们给了流的客户端记录标识符，一个有序的序列，并 2） 提供 CLFS 稳定存储上的记录的位置。

给定的一条记录的 LSN，可以通过调用以下函数提取的逻辑容器标识符、 块偏移量，并记录序列号。

[**ClfsLsnContainer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsncontainer)

[**ClfsLsnBlockOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsnblockoffset)

[**ClfsLsnRecordSequence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfslsnrecordsequence)

逻辑容器标识符是一个 32 位数字，因此没有 2 ^32 的可能的逻辑容器标识符，并且它们位于通过 0xFFFFFFFF 的范围内 0x0。 流最多可以有 2 ^32 的逻辑容器。

块偏移量存储在 23 位 LSN，但**ClfsLsnBlockOffset**返回稳定的存储介质的扇区大小与对齐的 32 位数字。 块偏移量始终是 512 的倍数。 此外，与稳定的存储介质的扇区大小对齐块偏移量。 例如，如果扇区大小为 1024 个字节，块偏移量将是 1024年的倍数。

记录序列号是一个 9 位数字，因此没有 2 ^9 (512) 可能记录的序列号，并且它们处于范围内通过 0x1FF 0x0。 日志 I/O 块可以有最多 512 记录。

 

 




