---
title: 多路复用 CLFS 日志
description: 多路复用 CLFS 日志
ms.assetid: bbea9bdc-8bb8-4455-89c4-4735bad85ba0
keywords:
- 公用日志文件系统 WDK 内核，多路复用日志
- CLFS WDK 内核，多路复用日志
- 多路复用日志 CLFS
- 稳定存储 WDK CLFS
- 存储 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087a91aef6b98a04517bc33a1506d569c7798a86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827823"
---
# <a name="multiplexed-clfs-logs"></a>多路复用 CLFS 日志





多*路日志*为多个流提供稳定的存储。 *专用日志*充当单个流的稳定存储。 本主题讨论多路复用日志。 有关专用日志的信息，请参阅[专用 CLFS 日志](dedicated-clfs-logs.md)。

多路日志的每个流都为其客户端提供其流是整个日志的假象。 在此上下文中，客户端是驱动程序、线程或写入公用日志文件系统（CLFS）日志并从中读取数据的其他软件单元。 单个流可能有多个客户端。 每个客户端都有自己的[**日志\_文件\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)结构，该结构表示流的开放实例。

请考虑具有两个流（每个流都有一个客户端）的多路复用日志的情况。 您可以使用以下过程来创建日志、流和客户端封送处理区。

1.  在代表客户端1的情况下，调用[**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)以获取指向**日志\_文件\_对象**结构的指针。 将*puszLogFileName*参数设置为 "log：&lt;log name&gt;：：&lt;stream name&gt;" 形式的字符串，其中 &lt;日志名称&gt; 是基础文件系统上的有效路径，&lt;流名称&gt; 是你选择将其分配给客户端1将使用的流的名称。 例如，可以将*puszLogFileName*设置为 "log： c：\\ClfsLogs\\myLog：： Stream1"。 在这种情况下，CLFS 将在 c：\\ClfsLogs 目录中创建基本日志文件 myLog blf，Stream1 将是客户端1使用的流的名称。

    **注意** 它是在*puszLogFileName*中传递的字符串的形式，它确定 CLFS 是创建专用日志还是多路复用日志。 如果字符串具有双冒号（：:)在路径名称后，CLFS 创建一个多路复用日志。



2.  在代表客户端2的情况下，调用[**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)以获取指向**日志\_文件\_对象**结构的指针。 将*puszLogFileName*参数设置为以下格式的字符串： "log：&lt;log name&gt;：：&lt;stream name&gt;"，其中 &lt;日志名称&gt; 是用于客户端1的同一路径名称和 &lt;流名称&gt; 是你选择将其分配给客户端2使用的流的名称。 例如，可以将*puszLogFileName*设置为 "log： c：\\ClfsLogs\\myLog：： Stream2"。

3.  将从**ClfsCreateLogFile**获取的一个**日志\_文件\_对象**指针传递到[**ClfsAddLogContainer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainer) ，以便在将保存日志记录的稳定存储上创建一个容器（连续物理区）。 通过设置*pcbContainer*参数来指定容器的大小（将向上舍入为 1 mb 的倍数）。 设置*puszContainerPath*参数以指定容器的路径名称。 路径名称可以是包含基本日志文件的目录的绝对路径或相对路径。

    再次调用**ClfsAddLogContainer** ，可以为日志创建其他容器。 请注意，给定日志的所有容器的大小必须相同。 作为多次调用**ClfsAddLogContainer**的替代方法，可以调用[**ClfsAddLogContainerSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainerset)同时创建多个容器。 请注意，你的容器集将充当客户端1和客户端2编写的日志记录的稳定存储。

4.  将代表客户端1获取的**日志\_文件\_对象**指针传递到[**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea) ，以获取指向客户端1可用于读取和写入日志记录的封送处理区域的指针。 通过设置*cbMarshallingBuffer*参数来指定封送处理区将使用的日志 i/o 块的大小。 可以使用多个其他参数设置封送处理区域的各种属性。

    如果客户端1需要其他封送处理区，请再次将同一**日志\_文件\_对象**指针传递到**ClfsCreateMarshallingArea** ，并将其用于客户端1需要的每个其他封送处理区域。

5.  将代表客户端2获取的**日志\_文件\_对象**指针传递到**ClfsCreateMarshallingArea** ，以获取客户端2可用于读取和写入日志记录的封送处理区域。 通过设置*cbMarshallingBuffer*参数来指定封送处理区将使用的日志 i/o 块的大小。

    **注意** 可以使用多个其他参数设置封送处理区域的各种属性。




如果客户端2需要其他封送处理区，请再次将相同的**日志\_文件\_对象**指针传递到**ClfsCreateMarshallingArea** ，并针对客户端2需要的每个其他封送处理区域传递一次。


现在，每个客户端1和2都有一个**日志\_文件\_对象**和一个或多个封送处理区，它们都可以通过调用以下函数，将记录写入其自己的流（通过与这些流关联的封送处理区）。

[**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)

[**ClfsReserveAndAppendLogAligned**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlogaligned)

[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)

由客户端1和2编写的所有日志记录都将转为同一日志;也就是说，对于稳定存储上的同一组物理容器。 CLFS 多路复用两个客户端写入的日志记录，并跟踪哪些记录属于每个流。

当客户端1将记录写入其流时，它将返回一系列用于标识这些记录的日志序列号（Lsn）的递增序列。 同样，客户端2获取自己的 Lsn 序列。 可以比较属于特定流的 Lsn，以确定写入相应记录的顺序。 但是，属于一个流的 LSN 不能与属于另一个流的 LSN 进行比较。

CLFS 维护一个基本 LSN，并为每个流维护最后一个 LSN，其中包括共享一个多路复用日志的流。 每个流都有一个活动部分，该活动部分以基 LSN 指向的记录开头，并以最后一个 LSN 指向的记录结束。 请注意，不能回收稳定存储区中的多路复用日志中的容器，直到所有日志流的基本 Lsn 超出了存储在该容器中的任何记录。








