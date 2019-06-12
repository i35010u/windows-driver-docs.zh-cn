---
title: 专用 CLFS 日志
description: 专用 CLFS 日志
ms.assetid: c6ca580c-b7f4-493a-8bd6-35d0aa932b1a
keywords:
- 常见日志文件系统 WDK 内核，专用日志
- CLFS WDK 内核，专用日志
- 专用的日志 WDK CLFS
- 稳定的存储 WDK CLFS
- 存储 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 860735d2ae97d08a090a888b324079754b771257
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388226"
---
# <a name="dedicated-clfs-logs"></a>专用 CLFS 日志





公用日志文件系统 (CLFS) 日志可以专用或多路复用。 一个*专用的日志*用作稳定存储为单个流。 一个*多路复用日志*充当多个流的稳定存储。 本主题讨论专用的日志。 有关多路日志的信息，请参阅[多路复用 CLFS 日志](multiplexed-clfs-logs.md)。

若要创建专用的日志，请执行以下步骤。

1.  调用[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)若要获取的指针[**日志\_文件\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff554316)结构。 设置*puszLogFileName*对窗体的字符串的参数"日志： *&lt;日志名称&gt;* "其中 *&lt;日志名称&gt;* 是基础文件系统上的有效路径。 例如，如果您设置*puszLogFileName*到"日志： c:\\ClfsLogs\\myLog"，将在 c： 驱动器中创建为底的对数文件 myLog.blf\\ClfsLogs 目录。 在 c:\\ClfsLogs 目录也将用作更高版本添加到日志的容器的默认位置。

    **请注意**它是传入的字符串的形式*puszLogFileName* ，它确定是否 CLFS 创建专用或多路日志。 如果字符串包含双冒号 （:）完成后的日志名称，然后 CLFS 创建多路的日志。 此处，提供的示例在"日志： c\\ClfsLogs\\myLog"有没有双冒号，因此 CLFS 创建专用的日志。




**日志\_文件\_对象**返回指针**ClfsCreateLogFile**表示专用的日志的一个，仅流的公开实例。


2.  传递**日志\_文件\_对象**指针从获取**ClfsCreateLogFile**到[ **ClfsAddLogContainer** ](https://msdn.microsoft.com/library/windows/hardware/ff540768)若要在将保存日志记录的稳定存储中创建容器 （物理连续范围）。 通过设置指定的容器 （这将向上舍入为 512 千字节的倍数） 的大小*pcbContainer*参数。 设置*puszContainerPath*参数来指定容器的路径名称。 路径名称可以是绝对或相对于包含基本的日志文件的目录。

    您可以为你的日志创建更多的容器，通过调用**ClfsAddLogContainer**试。 请注意，所有给定日志的容器必须大小相同。 作为调用的替代方法**ClfsAddLogContainer**几次，您可以调用[ **ClfsAddLogContainerSet** ](https://msdn.microsoft.com/library/windows/hardware/ff540770)同时创建多个容器。

3.  传递**日志\_文件\_对象**指针从获取**ClfsCreateLogFile**到[ **ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)以获取可用于读取和写入你的流日志记录的封送处理区域的指针。 指定封送处理区域将使用通过设置日志 I/O 块的大小*cbMarshallingBuffer*参数。 有几个可用于设置各种属性封送处理区域的其他参数。

    如果需要其他封送处理几方面，传递同一**日志\_文件\_对象**指针，指向**ClfsCreateMarshallingArea**同样，一次针对每个其他的封送处理区域您需要。

现在，已与你的流相关联的一个或多个封送处理区域，您可以写入记录那些通过调用以下函数的封送处理区域。

[**ClfsReserveAndAppendLog**](https://msdn.microsoft.com/library/windows/hardware/ff541723)

[**ClfsReserveAndAppendLogAligned**](https://msdn.microsoft.com/library/windows/hardware/ff541726)

[**ClfsWriteRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541770)

每次写入一条记录，你获得标识记录的日志序列号 (LSN)。 分配给记录的 LSN 始终是大于分配给之前编写的记录，而不考虑其封送处理区域用于写入记录的 LSN。








