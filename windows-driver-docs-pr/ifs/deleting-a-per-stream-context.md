---
title: 删除按流上下文
description: 删除按流上下文
ms.assetid: 293a2ba2-af8a-4c1b-bc35-5e37e6e84d57
keywords:
- 筛选器驱动程序，WDK 文件系统，每流上下文跟踪
- 文件系统筛选器驱动程序 WDK，每流上下文跟踪
- 每流上下文跟踪 WDK 文件系统
- 跟踪每个流的上下文 WDK 文件系统
- 正在删除每个流的上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d208588b510e872e6b4e4e867b5f00622a369d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841443"
---
# <a name="deleting-a-per-stream-context"></a>删除按流上下文


## <span id="ddk_deleting_a_per_stream_context_if"></span><span id="DDK_DELETING_A_PER_STREAM_CONTEXT_IF"></span>


当不再需要与文件流关联的每个流上下文时，应将其删除。 可以通过以下两种方式之一删除流上下文：

-   当筛选器驱动程序调用[**FsRtlRemovePerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff547238)时，手动。

-   当文件系统调用[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)时，它会自动调用流上下文的[**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357)例程。

### <a name="span-idwhen_the_filter_deletes_the_per-stream_contextspanspan-idwhen_the_filter_deletes_the_per-stream_contextspanspan-idwhen_the_filter_deletes_the_per-stream_contextspanwhen-the-filter-deletes-the-per-stream-context"></a><span id="When_the_Filter_Deletes_the_Per-Stream_Context"></span><span id="when_the_filter_deletes_the_per-stream_context"></span><span id="WHEN_THE_FILTER_DELETES_THE_PER-STREAM_CONTEXT"></span>当筛选器删除每个流的上下文时

当文件流仍处于打开状态时，当筛选器驱动程序需要删除文件流的每个流的上下文时，它将首先调用[**FsRtlRemovePerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff547238)以从与给定文件相关联的上下文的全局列表中删除该上下文。 在调用**FsRtlRemovePerStreamContext**之后，筛选器通常会释放上下文结构。

**请注意**   筛选器驱动程序调用[**FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)后，若要将每个流的上下文结构与文件流相关联，则在释放之前，它必须调用上下文的[**FsRtlRemovePerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff547238) 。 否则，在关闭文件流时系统将会崩溃。

 

### <a name="span-idwhen_the_per-stream_context_s_freecallback_is_calledspanspan-idwhen_the_per-stream_context_s_freecallback_is_calledspanspan-idwhen_the_per-stream_context_s_freecallback_is_calledspanwhen-the-per-stream-contexts-freecallback-is-called"></a><span id="When_the_Per-Stream_Context_s_FreeCallback_Is_Called"></span><span id="when_the_per-stream_context_s_freecallback_is_called"></span><span id="WHEN_THE_PER-STREAM_CONTEXT_S_FREECALLBACK_IS_CALLED"></span>调用每个流上下文的 FreeCallback 时

当文件流被关闭或删除时，文件系统会为文件流释放自己的流上下文。 此时，文件系统还将调用[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)，后者又会调用为该文件流的上下文的全局列表中包含的所有每个流的上下文注册的[**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357)例程。 （当筛选器驱动程序调用[**FsRtlInitPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)来初始化每个流的上下文结构时，将注册**FreeCallback**例程。 有关详细信息，请参阅**FSRTL\_PER\_STREAM\_CONTEXT**。）

**请注意**   筛选器驱动程序调用[**FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194) ，以便将每个流的上下文结构与文件流相关联[ **，则文件**](https://msdn.microsoft.com/library/windows/hardware/ff547357)系统负责确保当不再存在对流的任何打开的引用时，将调用筛选器的每流上下文。

 

 

 




