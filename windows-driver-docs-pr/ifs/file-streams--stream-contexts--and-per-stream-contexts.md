---
title: 文件流、流上下文和按流上下文
description: 文件流、流上下文和按流上下文
ms.assetid: baea4967-f0d6-4096-aac4-fd38c117b4c6
keywords:
- 筛选器驱动程序，WDK 文件系统，每流上下文跟踪
- 文件系统筛选器驱动程序 WDK，每流上下文跟踪
- 每流上下文跟踪 WDK 文件系统
- 跟踪每个流的上下文 WDK 文件系统
- 文件流 WDK
- 流控制块 WDK 文件系统
- SCB WDK 文件系统
- 流上下文 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0d256eea30827f95b7777ff6a18149c5f6d44ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841412"
---
# <a name="file-streams-stream-contexts-and-per-stream-contexts"></a>文件流、流上下文和按流上下文


## <span id="ddk_file_streams_stream_contexts_and_per_stream_contexts_if"></span><span id="DDK_FILE_STREAMS_STREAM_CONTEXTS_AND_PER_STREAM_CONTEXTS_IF"></span>


*文件流*是用于保存文件数据的字节序列。 通常，文件只有一个文件流，即文件的默认数据流。 但是，在支持多个数据流的文件系统上，每个文件可以有多个文件流。 其中一种是未命名的默认数据流。 其他命名为备用数据流。 打开文件时，实际上是打开了给定文件的流。

当文件系统首次打开文件流时，它将创建文件系统特定的*流上下文*结构，如文件控制块（FCB）或流控制块（SCB），并将此结构的地址存储在**FsContext**中。生成的文件对象的成员。

对于本地文件系统，如果再次打开已打开的文件流（例如，为共享读取访问），则 i/o 子系统将创建另一个文件对象，但文件系统不会创建新的流上下文。 这两个文件对象均接收相同流上下文结构的地址。 因此，对于本地文件系统，流上下文指针唯一标识文件流。

对于支持每个流的上下文的网络文件系统，如果使用相同的网络共享名或 IP 地址再次打开已打开的文件流，则行为与本地文件系统相同。 I/o 子系统会创建一个新的文件对象，但文件系统不会创建新的流上下文。 相反，它会将相同的**FsContext**指针值分配给这两个文件对象。 但是，如果使用不同的路径（例如，不同的共享名，或以前使用共享名打开的文件的 IP 地址）打开文件流，则文件系统将创建一个新的流上下文。 因此，对于支持每个流的上下文的网络文件系统， **FsContext**指针不会唯一标识文件流。

*每个流上下文*是一个筛选器定义的结构，其中包含[**每个\_流的 FSRTL\_，\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547357)结构作为其成员之一。 筛选器驱动程序使用此结构跟踪文件系统打开的每个文件流的相关信息。

### <a name="span-idfile_system_support_for_per-stream_contextsspanspan-idfile_system_support_for_per-stream_contextsspanspan-idfile_system_support_for_per-stream_contextsspanfile-system-support-for-per-stream-contexts"></a><span id="File_System_Support_for_Per-Stream_Contexts"></span><span id="file_system_support_for_per-stream_contexts"></span><span id="FILE_SYSTEM_SUPPORT_FOR_PER-STREAM_CONTEXTS"></span>针对每个流的上下文的文件系统支持

在 Microsoft Windows XP 和更高版本上，支持每个流的上下文的文件系统必须使用包含[**FSRTL\_ADVANCED\_FCB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)结构的流上下文结构。

与特定文件流关联的每个流上下文的全局列表由文件系统拥有。 当文件系统为文件流创建新的流上下文（FSRTL\_ADVANCED\_FCB\_标头对象）时，它将调用[**FsRtlSetupAdvancedHeader**](https://msdn.microsoft.com/library/windows/hardware/ff547257)来初始化此列表。 当文件系统筛选器驱动程序调用[**FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)时，会将筛选器创建的每个流的上下文添加到全局列表。

当文件系统删除文件流的流上下文时，它会调用[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)来释放筛选器与文件流关联的所有每个流的上下文。 此例程为全局列表中的每个流上下文调用[**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357)例程。 请注意， **FreeCallback**例程必须假定文件流的文件对象已被释放。

若要查询文件系统是否支持给定文件对象表示的文件流的每个流上下文，请对文件对象调用[**FsRtlSupportsPerStreamContexts**](https://docs.microsoft.com/previous-versions/ff547285(v=vs.85)) 。 请注意，对于某些类型的文件，文件系统可能支持每流上下文，但不适用于其他文件。 例如，NTFS 和 FAT 目前不支持页面文件的每个流的上下文。 因此，如果**FsRtlSupportsPerStreamContexts**对一个文件流返回**true** ，这并不意味着它将为所有文件流返回**true** 。

 

 




