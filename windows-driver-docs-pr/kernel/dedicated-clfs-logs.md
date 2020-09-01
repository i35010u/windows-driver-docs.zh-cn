---
title: 专用 CLFS 日志
description: 专用 CLFS 日志
ms.assetid: c6ca580c-b7f4-493a-8bd6-35d0aa932b1a
keywords:
- 公用日志文件系统 WDK 内核，专用日志
- CLFS WDK 内核，专用日志
- 专用日志 WDK CLFS
- 稳定存储 WDK CLFS
- 存储 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3aac2b3cad335fb494d182e1db64b8b65d726c9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188587"
---
# <a name="dedicated-clfs-logs"></a>专用 CLFS 日志





 (CLFS) 日志公用日志文件系统可以是专用或多路复用。 *专用日志*充当单个流的稳定存储。 多 *路日志* 为多个流提供稳定的存储。 本主题讨论专用日志。 有关多路复用日志的信息，请参阅多 [路复用 CLFS logs](multiplexed-clfs-logs.md)。

若要创建专用日志，请执行以下步骤。

1.  调用 [**ClfsCreateLogFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile) 以获取指向 [**日志 \_ 文件 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object) 结构的指针。 将*puszLogFileName*参数设置为 "log：* &lt; log &gt; name*" 形式的字符串，其中* &lt; 日志名称 &gt; *是基础文件系统上的有效路径。 例如，如果将 *puszLogFileName* 设置为 "log： c： \\ ClfsLogs \\ myLog"，则将在 c： \\ blf 目录中创建基本日志文件 myLog。 C： \\ ClfsLogs 目录还将充当稍后添加到日志中的容器的默认位置。

    **注意**  它是在 *puszLogFileName* 中传递的字符串的形式，它确定 CLFS 是创建专用日志还是多路复用日志。 如果字符串在日志名称后有一个双冒号 (：： ) ，则 CLFS 将创建一个多路复用日志。 在此处提供的示例中，"log： c \\ ClfsLogs \\ myLog" 没有双冒号，因此 CLFS 创建了一个专用日志。




**ClfsCreateLogFile**返回的**日志 \_ 文件 \_ 对象**指针表示专用日志的一个打开实例，只是一个流。


2.  将从**ClfsCreateLogFile**获取的**日志 \_ 文件 \_ 对象**指针传递到[**ClfsAddLogContainer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainer) ，以便在将保存日志记录的稳定存储上创建一个容器 (连续物理区) 。 通过设置 *pcbContainer* 参数来指定容器 (的大小，该大小将向上舍入为 512) kb 的倍数。 设置 *puszContainerPath* 参数以指定容器的路径名称。 路径名称可以是包含基本日志文件的目录的绝对路径或相对路径。

    再次调用 **ClfsAddLogContainer** ，可以为日志创建其他容器。 请注意，给定日志的所有容器的大小必须相同。 作为多次调用 **ClfsAddLogContainer** 的替代方法，可以调用 [**ClfsAddLogContainerSet**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainerset) 同时创建多个容器。

3.  将从**ClfsCreateLogFile**获取的**日志 \_ 文件 \_ 对象**指针传递到[**ClfsCreateMarshallingArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea) ，以获取指向可用于在流中读取和写入日志记录的封送处理区域的指针。 通过设置 *cbMarshallingBuffer* 参数来指定封送处理区将使用的日志 i/o 块的大小。 可以使用多个其他参数设置封送处理区域的各种属性。

    如果需要其他封送处理区，请再次将相同的 **日志 \_ 文件 \_ 对象** 指针传递到 **ClfsCreateMarshallingArea** ，一次是针对所需的每个其他的封送处理区。

现在，你已有一个或多个与流关联的封送处理区，可以通过调用以下函数将记录写入这些封送处理区。

[**ClfsReserveAndAppendLog**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)

[**ClfsReserveAndAppendLogAligned**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlogaligned)

[**ClfsWriteRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)

每次写入一条记录时，都将返回一个日志序列号 (LSN) 用于标识该记录。 分配给记录的 LSN 总是大于分配给先前写入记录的 LSN，而不考虑用于写入记录的封送处理区域。