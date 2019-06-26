---
title: 多路复用 CLFS 日志
description: 多路复用 CLFS 日志
ms.assetid: bbea9bdc-8bb8-4455-89c4-4735bad85ba0
keywords:
- 常见日志文件系统 WDK 内核，多路日志
- CLFS WDK 内核，多路日志
- 多路复用 WDK CLFS 日志
- 稳定的存储 WDK CLFS
- 存储 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dd53d61fbf3d9eabe2ef4d3f18ffdd377d1fa80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386004"
---
# <a name="multiplexed-clfs-logs"></a>多路复用 CLFS 日志





一个*多路复用日志*充当多个流的稳定存储。 一个*专用的日志*用作稳定存储为单个流。 本主题讨论多路的日志。 有关专用日志的信息，请参阅[专用 CLFS 日志](dedicated-clfs-logs.md)。

每个流的多路日志提供了其客户端提供的流是整个日志的视觉效果。 此上下文中的客户端是软件的一个驱动程序、 线程或某些其他单元的写入，并从公用日志文件系统 (CLFS) 日志中读取。 很可能有多个客户端的单个流。 每个客户端将具有其自己[**日志\_文件\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)结构，它代表打开的流的实例。

请考虑具有两个流，其中每个有一台客户端的多路日志的大小写。 以下过程可用于创建日志、 流和客户端区域的封送处理。

1.  代表客户端 1，调用[ **ClfsCreateLogFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfscreatelogfile)若要获取的指针**日志\_文件\_对象**结构。 设置*puszLogFileName*对窗体的字符串的参数"日志：&lt;日志名称&gt;::&lt;流名称&gt;"其中&lt;日志名称&gt;上是有效的路径基础文件系统和&lt;流名称&gt;是您能够向客户端 1 将使用的流的名称。 例如，可以设置*puszLogFileName*到"日志： c:\\ClfsLogs\\myLog::Stream1"。 在这种情况下，CLFS 将 c： 驱动器中创建为底的对数文件 myLog.blf\\ClfsLogs 目录和 Stream1 将由客户端 1 的流的名称。

    **请注意**它是传入的字符串的形式*puszLogFileName* ，它确定是否 CLFS 创建专用或多路日志。 如果字符串包含双冒号 （:）完成后的路径名称，然后 CLFS 创建多路的日志。



2.  代表客户端 2，调用[ **ClfsCreateLogFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfscreatelogfile)若要获取的指针**日志\_文件\_对象**结构。 设置*puszLogFileName*对窗体的字符串的参数"日志：&lt;日志名称&gt;::&lt;流名称&gt;"其中&lt;日志名称&gt;是相同的路径名称用于客户端 1，并&lt;流名称&gt;是您为将由客户端 2 的流的名称。 例如，可以设置*puszLogFileName*到"日志： c:\\ClfsLogs\\myLog::Stream2"。

3.  通过其中一**日志\_文件\_对象**指针从获取**ClfsCreateLogFile**到[ **ClfsAddLogContainer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsaddlogcontainer)上将保存日志记录的稳定存储中创建容器 （物理连续范围）。 通过设置指定的容器 （这将向上舍入为 1 兆字节的倍数） 的大小*pcbContainer*参数。 设置*puszContainerPath*参数来指定容器的路径名称。 路径名称可以是绝对或相对于包含基本的日志文件的目录。

    您可以为你的日志创建更多的容器，通过调用**ClfsAddLogContainer**试。 请注意，所有给定日志的容器必须大小相同。 作为调用的替代方法**ClfsAddLogContainer**几次，您可以调用[ **ClfsAddLogContainerSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsaddlogcontainerset)同时创建多个容器。 请注意在组的容器将用作日志记录由客户端 1 和客户端 2 编写稳定存储。

4.  传递**日志\_文件\_对象**代表客户端 1 到获得的指针[ **ClfsCreateMarshallingArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfscreatemarshallingarea)若要获取的指针封送处理区域 1 的客户端可用来读取和写入日志记录。 指定封送处理区域将使用通过设置日志 I/O 块的大小*cbMarshallingBuffer*参数。 有几个可用于设置各种属性封送处理区域的其他参数。

    如果客户端 1 需要其他封送处理几方面，传递同一**日志\_文件\_对象**指针，指向**ClfsCreateMarshallingArea**同样，一次针对每个其他封送处理该客户端 1 所需区域。

5.  传递**日志\_文件\_对象**代表客户端 2 到获得的指针**ClfsCreateMarshallingArea**来获取该客户端的封送处理区域 2 可用于读取和写入日志记录。 指定封送处理区域将使用通过设置日志 I/O 块的大小*cbMarshallingBuffer*参数。

    **请注意**有几个可用于设置各种属性封送处理区域的其他参数。




如果客户端 2 需要其他封送处理几方面，传递同一**日志\_文件\_对象**指针，指向**ClfsCreateMarshallingArea**同样，一次针对每个其他封送处理该客户端 2 所需区域。


现在，客户端 1 和 2 每个已**日志\_文件\_对象**和一个或多个封送处理区域，它们可以每个写入记录到其自己的流 （通过与这些流关联的封送处理区域）调用以下函数。

[**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreserveandappendlog)

[**ClfsReserveAndAppendLogAligned**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreserveandappendlogaligned)

[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)

所有日志记录写入客户端 1 和 2 转到该相同的日志。即，相同的物理容器上设置稳定存储。 CLFS 多路复用由两个客户端编写的日志记录和跟踪哪些记录属于每个流。

因为客户端 1 将记录写入到它的流，该通道返回识别这些记录的日志序列号 (Lsn) 的递增序列。 同样，客户端 2 获取其自己的 Lsn。 属于特定流 Lsn 可以进行比较来确定在其中编写相应的记录的顺序。 但是，不能与属于另一个流 LSN 比较属于一个流 LSN。

CLFS 维护基准 LSN 和每个流，其中包括流共享多路的日志的最后一个 LSN。 每个流具有包含该记录指向的基准 LSN 开始和结束指向最后一个 LSN 的记录的活动部分。 请注意，在稳定存储上的多路日志中的容器不能回收之前的所有日志的流具有超出了该容器中存储的任何记录的高级基的 Lsn。








