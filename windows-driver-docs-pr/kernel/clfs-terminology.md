---
title: CLFS 术语
description: 以下列表提供了公用日志文件系统 (CLFS) 文档中使用的关键术语的定义。
Robots: noindex, nofollow
keywords:
- 公用日志文件系统 WDK 内核，术语
- CLFS WDK 内核，术语
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57940b6304fc5fc5b501f62cfc1df6374c71fd05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838577"
---
# <a name="clfs-terminology"></a>CLFS 术语


以下列表提供了公用日志文件系统 (CLFS) 文档中使用的关键术语的定义。 这些定义适用于讨论 CLFS，但可能不适用。 其中的许多术语在其他技术的上下文中具有一般含义或含义，这些技术不同于此处提供的定义。

<a href="" id="kernel-clfs-term-container"></a>**容器**  
物理磁盘或其他稳定存储介质上的连续区。 例如，容器可能是一个连续的磁盘文件。

<a href="" id="kernel-clfs-term-sector"></a>**过**  
物理存储介质上的原子 i/o 单元。 扇区的大小是特定存储设备的属性。 例如，硬盘的扇区大小可能为512字节。

<a href="" id="kernel-clfs-term-log"></a>**日志**  
基本文件和一组逻辑上排序的容器。 基本文件包含日志的元数据，容器保存日志记录。 所有容器的大小都相同。

<a href="" id="kernel-clfs-term-client"></a>**机**  
使用 CLFS 日志的应用程序、驱动程序、线程或其他软件单元。

<a href="" id="kernel-clfs-term-record"></a>**记录**  
客户端可追加到日志或从日志中读取的数据单元。

<a href="" id="kernel-clfs-term-stream"></a>**流**  
日志中记录的排序子集。 一个日志可以有一个或多个流。 客户端将记录追加到特定流并从中读取记录。 您可以比较给定流中的记录，以确定它们的写入顺序。 不能比较不同流中的记录。 给定的流可以有多个客户端。 例如，多个线程可能会将记录追加到单个流。 对于客户端，流看起来就像是整个日志。

<a href="" id="kernel-clfs-term-dedicated-log"></a>**专用日志**  
只能有一个流的日志。

<a href="" id="kernel-clfs-term-multiplexed-log"></a>**多路复用日志**  
可以有多个流的日志。

<a href="" id="kernel-clfs-term-log-i-o-block"></a>**日志 i/o 块**  
一个缓冲区，其中 CLFS 收集一组以原子方式写入到稳定存储中的记录。

<a href="" id="kernel-clfs-term-marshalling-area"></a>**封送区**  
一组由 CLFS 客户端创建、维护和计划的日志 i/o 块，用于收集日志记录并将日志记录写入稳定的存储。 在易失内存中为特定的封送区分配的日志 i/o 块的大小都相同。

**注意**   即使所有日志 i/o 块 (在易失性内存中) 对于特定的封送处理区域大小相同，从该封送处理区 (写入稳定存储的日志 i/o 块) 大小不同。 例如，如果在日志已满之前强制将某个日志 i/o 块强制用于稳定的存储，则只会将该块的已使用部分写入到稳定的存储中。

 

<a href="" id="kernel-clfs-term-log-sequence-number--lsn"></a>**LSN)  (日志序列号**  
一个不透明的结构，它包含唯一标识给定流中的日志记录的值。 当客户端向流中写入记录时，它将返回一个可用于在将来标识记录的 LSN。 CLFS 分配给流中的记录的 Lsn 形成了一个递增的序列。 也就是说，分配给流中的记录的 LSN 总是大于分配给先前写入到同一流的记录的 LSN。

**注意**   流间的记录不可比较。 也就是说，不能比较不同流中的两个记录的 Lsn，以确定首先编写的记录。

 

<a href="" id="kernel-clfs-term-base-lsn"></a>**基本 LSN**  
流的客户端仍需要的流中最早记录的 LSN。 客户端负责更新基本 LSN。

<a href="" id="kernel-clfs-term-last-lsn"></a>**最后一个 LSN**  
流的客户端仍需要的流中的最年轻记录的 LSN。 通常，这是最近写入到流中的记录，但客户端可以选择手动设置最后一个 LSN，使之指向流中的某个早期记录。 将最后一个 LSN 手动设置为较早的记录称为 *截断* 流。

<a href="" id="kernel-clfs-term-archive-tail"></a>**存档结尾**  
日志中未进行存档的最早记录的 LSN。 并非每个日志都有存档结尾。 没有存档尾的日志称为 " *暂时*"，具有存档结尾的日志称为 " *不临时*"。 当客户端指定日志具有存档尾时，客户端负责更新存档结尾。

<a href="" id="kernel-clfs-term-active-portion-of-a-stream"></a>**流的活动部分**  
当前由其客户端使用的流部分。 活动部分以基本 LSN 或存档尾所指向的记录开始，以较小者为准。 活动部分以最后一个 LSN 指向的记录结束。

 

 




