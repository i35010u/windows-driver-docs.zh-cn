---
title: 文件流、流上下文和按流上下文
description: 文件流、流上下文和按流上下文
ms.assetid: baea4967-f0d6-4096-aac4-fd38c117b4c6
keywords:
- 筛选器驱动程序 WDK 文件系统中，每个流的上下文跟踪
- 文件系统筛选器驱动程序 WDK，跟踪每个流上下文
- 每个流上下文跟踪 WDK 文件系统
- 跟踪每个流上下文 WDK 文件系统
- 文件流 WDK
- 流控制块 WDK 文件系统
- SCB WDK 文件系统
- 流上下文 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ac1bd55b1d13e4f263cdbf8cce0653c91f6ee76
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565080"
---
# <a name="file-streams-stream-contexts-and-per-stream-contexts"></a>文件流、流上下文和按流上下文


## <span id="ddk_file_streams_stream_contexts_and_per_stream_contexts_if"></span><span id="DDK_FILE_STREAMS_STREAM_CONTEXTS_AND_PER_STREAM_CONTEXTS_IF"></span>


一个*文件流*是用来保存文件数据的字节序列。 通常一个文件具有只有一个文件流，即该文件的默认数据流。 但是，在支持多个数据流的文件系统，每个文件可以包含多个文件流。 其中之一即是未命名的默认数据流。 其他是已命名备用数据流。 当打开文件时，实际上要打开给定文件的流。

当文件系统第一次打开一个文件流时，它将创建文件系统特定*流上下文*结构，如文件控制块 (FCB) 或流控制块 (SCB)，并将此结构的地址存储在**FsContext**所生成的文件对象的成员。

对于本地文件系统，如果打开已打开的文件流，则再次 （用于共享读访问，例如），I/O 子系统会创建另一个文件对象，但文件系统不会创建新的流上下文。 这两个文件对象收到相同的流上下文结构的地址。 因此，对于本地文件系统流上下文指针唯一标识文件流。

支持每个流的网络文件系统的上下文中，如果再次使用相同的网络打开已打开的文件流共享名称或 IP 地址，该行为与本地文件系统相同。 I/O 子系统创建新的文件对象，但文件系统不会创建新的流上下文。 相反，它将分配相同**FsContext**到这两个文件对象的指针值。 但是，如果使用不同的路径 （例如，其他的共享名或使用共享名称以前打开的文件的 IP 地址） 打开的文件流，则文件系统的确创建新的流上下文。 因此，对于支持每个流上下文的网络文件系统**FsContext**指针不唯一标识文件流。

一个*每个流上下文*是筛选器定义的结构，其中包含[ **FSRTL\_每\_流\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547357)结构作为其成员之一。 筛选器驱动程序使用此结构来跟踪每个打开的文件系统的文件流有关的信息。

### <a name="span-idfilesystemsupportforper-streamcontextsspanspan-idfilesystemsupportforper-streamcontextsspanspan-idfilesystemsupportforper-streamcontextsspanfile-system-support-for-per-stream-contexts"></a><span id="File_System_Support_for_Per-Stream_Contexts"></span><span id="file_system_support_for_per-stream_contexts"></span><span id="FILE_SYSTEM_SUPPORT_FOR_PER-STREAM_CONTEXTS"></span>文件系统支持的每个 Stream 上下文

Microsoft Windows XP 及更高版本，支持每个流上下文的文件系统必须使用包含的流上下文结构[ **FSRTL\_高级\_FCB\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff547334)结构。

文件系统为所有与特定文件流关联的每个流上下文的全局列表。 文件系统时创建新的流上下文 (FSRTL\_高级\_FCB\_标头对象) 的文件流，它会调用[ **FsRtlSetupAdvancedHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff547257)到初始化此列表。 当文件系统筛选器驱动程序调用[ **FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)，筛选器创建的每个流上下文添加到全局列表。

当文件系统中删除文件流及其流上下文时，它将调用[ **FsRtlTeardownPerStreamContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547295)来释放所有筛选器已将文件流关联的每个流上下文。 此例程调用[ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)例行为每个全局列表中的每个流上下文。 请注意， **FreeCallback**例程必须假定已释放的文件流的文件对象。

若要查询文件系统是否支持每个流上下文由给定的文件对象表示的文件流，请调用[ **FsRtlSupportsPerStreamContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547285)上的文件对象。 请注意对于某些类型的文件，但没有为其他文件系统，可能会支持每个流上下文。 例如，NTFS 和 FAT 当前不支持每个流上下文的分页文件。 因此如果**FsRtlSupportsPerStreamContexts**返回**TRUE**对于一个文件流，这并不意味着，它将返回**TRUE**流的所有文件。

 

 




