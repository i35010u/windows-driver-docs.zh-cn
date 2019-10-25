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
ms.openlocfilehash: fffc480c3ae74313ccc05395f9543e9feb1515cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836952"
---
# <a name="dedicated-clfs-logs"></a>专用 CLFS 日志





公用日志文件系统（CLFS）日志可以是专用或多路复用。 *专用日志*充当单个流的稳定存储。 多*路日志*为多个流提供稳定的存储。 本主题讨论专用日志。 有关多路复用日志的信息，请参阅多[路复用 CLFS logs](multiplexed-clfs-logs.md)。

若要创建专用日志，请执行以下步骤。

1.  调用[**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)以获取指向[**日志\_文件\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)结构的指针。 将*puszLogFileName*参数设置为 "log： *&lt;log name&gt;* " 格式的字符串，其中 *&lt;日志名称&gt;* 是基础文件系统上的有效路径。 例如，如果将*puszLogFileName*设置为 "log： c：\\ClfsLogs\\myLog"，则将在 c：\\blf 目录中创建基本日志文件 myLog。 C：\\ClfsLogs 目录还将充当稍后添加到日志中的容器的默认位置。

    **注意** 它是在*puszLogFileName*中传递的字符串的形式，它确定 CLFS 是创建专用日志还是多路复用日志。 如果字符串具有双冒号（：:)在日志名称后，CLFS 创建一个多路复用日志。 在此处给出的示例中，"log： c\\ClfsLogs\\myLog" 没有双冒号，因此 CLFS 创建专用日志。




**ClfsCreateLogFile**返回的**日志\_文件\_对象**指针表示专用日志的一个打开实例，只是一个流。


2.  将从**ClfsCreateLogFile**获取的**日志\_文件\_对象**指针传递到[**ClfsAddLogContainer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainer) ，以在保存日志记录的稳定存储上创建容器（连续物理区）。 通过设置*pcbContainer*参数来指定容器的大小（将向上舍入为 512 kb 的倍数）。 设置*puszContainerPath*参数以指定容器的路径名称。 路径名称可以是包含基本日志文件的目录的绝对路径或相对路径。

    再次调用**ClfsAddLogContainer** ，可以为日志创建其他容器。 请注意，给定日志的所有容器的大小必须相同。 作为多次调用**ClfsAddLogContainer**的替代方法，可以调用[**ClfsAddLogContainerSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsaddlogcontainerset)同时创建多个容器。

3.  将从**ClfsCreateLogFile**获取的**日志\_文件\_对象**指针传递到[**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea) ，以获取指向可用于在流中读取和写入日志记录的封送处理区域的指针。 通过设置*cbMarshallingBuffer*参数来指定封送处理区将使用的日志 i/o 块的大小。 可以使用多个其他参数设置封送处理区域的各种属性。

    如果需要其他封送处理区，请将相同的**日志\_文件\_对象**指针再次传递给**ClfsCreateMarshallingArea** ，一次是针对所需的每个其他的封送处理区。

现在，你已有一个或多个与流关联的封送处理区，可以通过调用以下函数将记录写入这些封送处理区。

[**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)

[**ClfsReserveAndAppendLogAligned**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlogaligned)

[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)

每次写入一条记录时，都将返回标识该记录的日志序列号（LSN）。 分配给记录的 LSN 总是大于分配给先前写入记录的 LSN，而不考虑用于写入记录的封送处理区域。








