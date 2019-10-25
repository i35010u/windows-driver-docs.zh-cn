---
title: 创建按流上下文
description: 创建按流上下文
ms.assetid: e33dba3b-50f7-43d8-b7e8-b7c2c9034d51
keywords:
- 筛选器驱动程序，WDK 文件系统，每流上下文跟踪
- 文件系统筛选器驱动程序 WDK，每流上下文跟踪
- 每流上下文跟踪 WDK 文件系统
- 跟踪每个流的上下文 WDK 文件系统
- 分配每流上下文
- 正在初始化每流上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2a5435647c97777c7443356eb952e0783b09d06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841450"
---
# <a name="creating-a-per-stream-context"></a>创建按流上下文


## <span id="ddk_creating_a_per_stream_context_if"></span><span id="DDK_CREATING_A_PER_STREAM_CONTEXT_IF"></span>


文件系统筛选器驱动程序通常会在首次打开文件流时为文件流创建[每个流的上下文结构](file-streams--stream-contexts--and-per-stream-contexts.md)。 但是，可以在任何操作期间创建每个流的上下文结构并将其与文件流相关联。

### <a name="span-idallocating_the_per-stream_contextspanspan-idallocating_the_per-stream_contextspanspan-idallocating_the_per-stream_contextspanallocating-the-per-stream-context"></a><span id="Allocating_the_Per-Stream_Context"></span><span id="allocating_the_per-stream_context"></span><span id="ALLOCATING_THE_PER-STREAM_CONTEXT"></span>分配每个流的上下文

可以从分页或非分页池分配每个流的上下文结构。 若要分配每个流的上下文，请调用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) ，如以下示例中所示：

```cpp
contextSize = sizeof(SPY_STREAM_CONTEXT) + fileName.Length;
ctx = ExAllocatePoolWithTag(NonPagedPool, 
                            contextSize,
                            MYLEGACYFILTER_CONTEXT_TAG);
```

**请注意**  如果筛选器从页面缓冲池分配每个流的上下文结构，则无法从其创建完成例程调用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 。 这是因为，可以在 IRQL 调度\_级别调用完成例程。

 

### <a name="span-idinitializing_the_per-stream_contextspanspan-idinitializing_the_per-stream_contextspanspan-idinitializing_the_per-stream_contextspaninitializing-the-per-stream-context"></a><span id="Initializing_the_Per-Stream_Context"></span><span id="initializing_the_per-stream_context"></span><span id="INITIALIZING_THE_PER-STREAM_CONTEXT"></span>正在初始化每个流的上下文

文件系统筛选器驱动程序调用[**FsRtlInitPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)来初始化每个流的上下文结构。 此例程初始化上下文结构\_上下文部分的每\_流的 FSRTL\_。 （结构的其余部分是特定于筛选器的。）

**请注意**  如果筛选器驱动程序只为每个文件流创建一个每流上下文结构，则它应将*InstanceId*参数的**NULL**传递到[**FsRtlInitPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)。

 

筛选器驱动程序可以随时初始化每个流的上下文。 但是，必须在将上下文与文件流关联之前执行此操作。

 

 




