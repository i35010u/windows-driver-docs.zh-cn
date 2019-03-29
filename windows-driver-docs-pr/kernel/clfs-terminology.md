---
title: CLFS 术语
description: 以下列表提供公用日志文件系统 (CLFS) 文档中使用的重要术语的定义。
Robots: noindex, nofollow
ms.assetid: d8511c5a-0181-4c54-acdc-e8a5892bb620
keywords:
- 常见日志文件系统 WDK 内核术语
- CLFS WDK 内核术语
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96c41d15b038d037c485dfa028a52736e57c66a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563971"
---
# <a name="clfs-terminology"></a>CLFS 术语


以下列表提供公用日志文件系统 (CLFS) 文档中使用的重要术语的定义。 这些定义在 CLFS 的讨论过程中应用，但可能不适用于否则。 许多这些条款的其他技术不同于此处提供的定义的上下文中都有常规含义或的含义。

<a href="" id="kernel-clfs-term-container"></a>**container**  
物理磁盘或其他稳定存储介质上连续范围。 例如，容器可能是连续的磁盘文件。

<a href="" id="kernel-clfs-term-sector"></a>**sector**  
物理存储介质上的原子 I/O 单位。 扇区的大小是特定存储设备的属性。 例如，硬盘可能具有 512 字节的扇区大小。

<a href="" id="kernel-clfs-term-log"></a>**log**  
基本文件和一组逻辑上有序的容器。 基本文件保留的日志的元数据和容器所包含日志记录。 所有容器都都具有相同大小。

<a href="" id="kernel-clfs-term-client"></a>**client**  
应用程序、 驱动程序、 线程或使用 CLFS 日志的软件的其他单元。

<a href="" id="kernel-clfs-term-record"></a>**record**  
客户端可以将追加到或从日志中读取的数据单位。

<a href="" id="kernel-clfs-term-stream"></a>**stream**  
在日志中记录的有序的子集。 日志可以有一个或多个流。 客户端会追加到的记录和特定的流中读取记录。 您可以比较给定的流，以确定它们编写的顺序中的记录。 无法比较不同的流中的记录。 给定的流可以包含多个客户端。 例如，多个线程可以将记录追加到单个流。 对于客户端，流将显示，就好像整个日志。

<a href="" id="kernel-clfs-term-dedicated-log"></a>**专用的日志**  
可以具有只有一个流日志。

<a href="" id="kernel-clfs-term-multiplexed-log"></a>**多路复用日志**  
可以有多个流日志。

<a href="" id="kernel-clfs-term-log-i-o-block"></a>**日志 I/O 块**  
CLFS 从中收集记录以原子方式写入到稳定存储一组缓冲区。

<a href="" id="kernel-clfs-term-marshalling-area"></a>**封送处理区域**  
一组日志 I/O 块，创建、 维护，并且由 CLFS 客户端计划用于收集日志记录和写入到稳定存储。 在特定的封送处理区域的易失性内存中分配的日志 I/O 块大小完全相同。

**请注意**  即使所有日志 I/O 块 （易失性内存中） 为特定的封送处理区域都是相同的大小，写入到稳定存储 （从该封送处理区域） 的日志 I/O 块的大小不同。 例如，如果日志 I/O 块强制到稳定存储之前已满，将写入的块中，仅使用的部分到稳定存储。

 

<a href="" id="kernel-clfs-term-log-sequence-number--lsn"></a>**日志序列号 (LSN)**  
不透明结构，它包含用于唯一地标识给定流中的日志记录的值。 当客户端将流写入一条记录时，该通道返回它可用于在将来识别该记录的 LSN。 Lsn，CLFS 将分配给以流形式记录递增序列。 即，分配给流中记录的 LSN 大于始终分配给在同一个读取以前写入记录的 LSN。

**请注意**  跨流记录不可比较。 也就是说，不能比较不同的流中的两个记录的 Lsn，以确定第一次写入的记录。

 

<a href="" id="kernel-clfs-term-base-lsn"></a>**基准 LSN**  
仍然需要的流的客户端的流中的最早记录的 LSN。 客户端负责更新基准 LSN。

<a href="" id="kernel-clfs-term-last-lsn"></a>**最后一个 LSN**  
仍然需要的流的客户端的流中的最年轻记录的 LSN。 这通常是最新写入到流，该记录，但客户端可以选择手动设置的最后一个 LSN，以指向流中的某些较早记录。 手动设置到更早的记录的最后一个 LSN 称为*截断*流。

<a href="" id="kernel-clfs-term-archive-tail"></a>**存档尾数据**  
最旧的存档的日志中记录的 LSN 尚未发生。 不是每个日志中的存档尾数据。 调用没有存档尾数据的日志*临时*，并调用已存档尾数据的日志*非临时*。 当客户端指定日志已存档尾数据时，客户端负责更新存档尾数据。

<a href="" id="kernel-clfs-term-active-portion-of-a-stream"></a>**流的活动部分**  
当前正在使用其客户端流的一部分。 活动部分开头指向的基准 LSN 或存档尾数据的记录，两者中较小。 活动部分以记录指向最后一个 LSN 的结尾。

 

 




