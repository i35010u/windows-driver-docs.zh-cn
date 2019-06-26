---
title: 创建按流上下文
description: 创建按流上下文
ms.assetid: e33dba3b-50f7-43d8-b7e8-b7c2c9034d51
keywords:
- 筛选器驱动程序 WDK 文件系统中，每个流的上下文跟踪
- 文件系统筛选器驱动程序 WDK，跟踪每个流上下文
- 每个流上下文跟踪 WDK 文件系统
- 跟踪每个流上下文 WDK 文件系统
- 分配每个流上下文
- 初始化每个流上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a56d96061f2eef94ebe54ba4116adc6f1a767bfd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363543"
---
# <a name="creating-a-per-stream-context"></a>创建按流上下文


## <span id="ddk_creating_a_per_stream_context_if"></span><span id="DDK_CREATING_A_PER_STREAM_CONTEXT_IF"></span>


文件系统筛选器驱动程序通常会创建[每个流的上下文结构](file-streams--stream-contexts--and-per-stream-contexts.md)文件打开时的文件流是第一个流。 但是，可以创建每个流上下文结构并将其与文件流关联的任何操作期间。

### <a name="span-idallocatingtheper-streamcontextspanspan-idallocatingtheper-streamcontextspanspan-idallocatingtheper-streamcontextspanallocating-the-per-stream-context"></a><span id="Allocating_the_Per-Stream_Context"></span><span id="allocating_the_per-stream_context"></span><span id="ALLOCATING_THE_PER-STREAM_CONTEXT"></span>分配 Stream 每个上下文

每个流可以从分页或非分页缓冲池分配结构的上下文。 若要分配的每个流上下文，调用[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)如下面的示例中所示：

```cpp
contextSize = sizeof(SPY_STREAM_CONTEXT) + fileName.Length;
ctx = ExAllocatePoolWithTag(NonPagedPool, 
                            contextSize,
                            MYLEGACYFILTER_CONTEXT_TAG);
```

**请注意**  如果你的筛选器从页面缓冲池分配的每个流上下文结构，它不能调用[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)从其创建完成例程。 这是因为可以在 IRQL 调度调用完成例程\_级别。

 

### <a name="span-idinitializingtheper-streamcontextspanspan-idinitializingtheper-streamcontextspanspan-idinitializingtheper-streamcontextspaninitializing-the-per-stream-context"></a><span id="Initializing_the_Per-Stream_Context"></span><span id="initializing_the_per-stream_context"></span><span id="INITIALIZING_THE_PER-STREAM_CONTEXT"></span>初始化每个 Stream 上下文

文件系统筛选器驱动程序调用[ **FsRtlInitPerStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlinitperstreamcontext)初始化每个流上下文结构。 此例程初始化 FSRTL\_出差\_流\_上下文一部分的上下文结构。 （该结构的其余部分是特定于驱动程序筛选器。）

**请注意**  如果筛选器驱动程序创建只有一个每个文件流的每个流上下文结构，它应传递**NULL**有关*InstanceId*参数[**FsRtlInitPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlinitperstreamcontext)。

 

筛选器驱动程序可以在任何时间初始化每个流上下文。 但是，它必须实现与文件流关联上下文之前。

 

 




