---
title: 删除按流上下文
description: 删除按流上下文
ms.assetid: 293a2ba2-af8a-4c1b-bc35-5e37e6e84d57
keywords:
- 筛选器驱动程序 WDK 文件系统中，每个流的上下文跟踪
- 文件系统筛选器驱动程序 WDK，跟踪每个流上下文
- 每个流上下文跟踪 WDK 文件系统
- 跟踪每个流上下文 WDK 文件系统
- 删除每个流上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87cc07573c7c3d28011af77bf28a0ae66f39d7d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381009"
---
# <a name="deleting-a-per-stream-context"></a>删除按流上下文


## <span id="ddk_deleting_a_per_stream_context_if"></span><span id="DDK_DELETING_A_PER_STREAM_CONTEXT_IF"></span>


如果不再需要与文件流关联的每个流上下文，则应删除。 Stream 上下文会删除在两种方式之一：

-   手动，当筛选器驱动程序调用[ **FsRtlRemovePerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff547238)。

-   自动，当文件系统调用[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)，从而又会调用的流上下文[ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)例程。

### <a name="span-idwhenthefilterdeletestheper-streamcontextspanspan-idwhenthefilterdeletestheper-streamcontextspanspan-idwhenthefilterdeletestheper-streamcontextspanwhen-the-filter-deletes-the-per-stream-context"></a><span id="When_the_Filter_Deletes_the_Per-Stream_Context"></span><span id="when_the_filter_deletes_the_per-stream_context"></span><span id="WHEN_THE_FILTER_DELETES_THE_PER-STREAM_CONTEXT"></span>筛选器时删除的每个 Stream 上下文

当需要删除文件流文件流时其每个流上下文筛选器驱动程序仍处于打开状态，它首先调用[ **FsRtlRemovePerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547238)若要从全局列表中删除上下文与给定文件相关联的上下文。 在调用**FsRtlRemovePerStreamContext**，筛选器通常释放上下文结构。

**请注意**  后筛选器驱动程序已调用[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)若要将与文件流关联的每个流上下文结构，它必须调用[ **FsRtlRemovePerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547238)之前将其释放上下文。 否则，系统将崩溃时文件流已关闭。

 

### <a name="span-idwhentheper-streamcontextsfreecallbackiscalledspanspan-idwhentheper-streamcontextsfreecallbackiscalledspanspan-idwhentheper-streamcontextsfreecallbackiscalledspanwhen-the-per-stream-contexts-freecallback-is-called"></a><span id="When_the_Per-Stream_Context_s_FreeCallback_Is_Called"></span><span id="when_the_per-stream_context_s_freecallback_is_called"></span><span id="WHEN_THE_PER-STREAM_CONTEXT_S_FREECALLBACK_IS_CALLED"></span>当调用每个 Stream 上下文 FreeCallback

当正在文件流文件系统关闭或删除，释放其自己的文件流的流上下文。 在此期间，文件系统还会调用[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)，从而又会调用[ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)例程注册的所有全局列表的文件流的上下文中包含的每个流上下文。 (A **FreeCallback**例程在筛选器驱动程序调用时才注册[ **FsRtlInitPerStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlinitperstreamcontext)初始化每个流上下文结构。 有关详细信息，请参阅**FSRTL\_每\_流\_上下文**。)

**请注意**  后筛选器驱动程序已调用[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)要与文件流关联的每个流上下文结构，文件系统是负责确保[ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)例程的筛选器的每个流上下文调用时不再有任何打开的流的引用。

 

 

 




