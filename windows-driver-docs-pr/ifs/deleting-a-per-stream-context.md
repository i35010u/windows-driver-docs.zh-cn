---
title: 删除按流上下文
description: 删除按流上下文
keywords:
- 筛选器驱动程序，WDK 文件系统，每流上下文跟踪
- 文件系统筛选器驱动程序 WDK，每流上下文跟踪
- 每流上下文跟踪 WDK 文件系统
- 跟踪每个流的上下文 WDK 文件系统
- 正在删除每个流的上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b521fc5225330552cb5ca4ad34dfededdd27b9f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840103"
---
# <a name="deleting-a-per-stream-context"></a>删除按流上下文


## <span id="ddk_deleting_a_per_stream_context_if"></span><span id="DDK_DELETING_A_PER_STREAM_CONTEXT_IF"></span>


当不再需要与文件流关联的每个流上下文时，应将其删除。 可以通过以下两种方式之一删除流上下文：

-   当筛选器驱动程序调用 [**FsRtlRemovePerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlremoveperstreamcontext)时，手动。

-   当文件系统调用 [**FsRtlTeardownPerStreamContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperstreamcontexts)时，它会自动调用流上下文的 [**FreeCallback**](/previous-versions/ff547357(v=vs.85)) 例程。

### <a name="span-idwhen_the_filter_deletes_the_per-stream_contextspanspan-idwhen_the_filter_deletes_the_per-stream_contextspanspan-idwhen_the_filter_deletes_the_per-stream_contextspanwhen-the-filter-deletes-the-per-stream-context"></a><span id="When_the_Filter_Deletes_the_Per-Stream_Context"></span><span id="when_the_filter_deletes_the_per-stream_context"></span><span id="WHEN_THE_FILTER_DELETES_THE_PER-STREAM_CONTEXT"></span>当筛选器删除 Per-Stream 上下文时

当文件流仍处于打开状态时，当筛选器驱动程序需要删除文件流的每个流的上下文时，它将首先调用 [**FsRtlRemovePerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlremoveperstreamcontext) 以从与给定文件相关联的上下文的全局列表中删除该上下文。 在调用 **FsRtlRemovePerStreamContext** 之后，筛选器通常会释放上下文结构。

**注意**   在筛选器驱动程序调用 [**FsRtlInsertPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinsertperstreamcontext) 以将每个流的上下文结构与文件流相关联后，在释放它之前，它必须为上下文调用 [**FsRtlRemovePerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlremoveperstreamcontext) 。 否则，在关闭文件流时系统将会崩溃。

 

### <a name="span-idwhen_the_per-stream_context_s_freecallback_is_calledspanspan-idwhen_the_per-stream_context_s_freecallback_is_calledspanspan-idwhen_the_per-stream_context_s_freecallback_is_calledspanwhen-the-per-stream-contexts-freecallback-is-called"></a><span id="When_the_Per-Stream_Context_s_FreeCallback_Is_Called"></span><span id="when_the_per-stream_context_s_freecallback_is_called"></span><span id="WHEN_THE_PER-STREAM_CONTEXT_S_FREECALLBACK_IS_CALLED"></span>当调用 Per-Stream 上下文的 FreeCallback 时

当文件流被关闭或删除时，文件系统会为文件流释放自己的流上下文。 此时，文件系统还将调用 [**FsRtlTeardownPerStreamContexts**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperstreamcontexts)，后者又会调用为该文件流的上下文的全局列表中包含的所有每个流的上下文注册的 [**FreeCallback**](/previous-versions/ff547357(v=vs.85)) 例程。  (当筛选器驱动程序调用 [**FsRtlInitPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)来初始化每个流的上下文结构时，将注册 **FreeCallback** 例程。 有关详细信息，请参阅 **FSRTL \_ PER \_ STREAM \_ CONTEXT**。 ) 

**注意**   在筛选器驱动程序调用 [**FsRtlInsertPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinsertperstreamcontext) 以将每个流的上下文结构与文件流相关联后，文件系统负责确保在不再存在对流的任何打开的引用时，将调用筛选器的每个流上下文的 [**FreeCallback**](/previous-versions/ff547357(v=vs.85)) 例程。

 

 

