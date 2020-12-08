---
title: 创建按流上下文
description: 创建按流上下文
keywords:
- 筛选器驱动程序，WDK 文件系统，每流上下文跟踪
- 文件系统筛选器驱动程序 WDK，每流上下文跟踪
- 每流上下文跟踪 WDK 文件系统
- 跟踪每个流的上下文 WDK 文件系统
- 分配每流上下文
- 正在初始化每流上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5b47ff397e9af5b65f1f8ef23b1744d36a194bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815111"
---
# <a name="creating-a-per-stream-context"></a>创建按流上下文

使用包含 [**FSRTL_PER_STREAM_CONTEXT**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_per_stream_context) 结构的每个流的上下文结构的旧文件系统筛选器驱动程序可以利用 MICROSOFT Windows XP 和更高版本中的内置每流上下文支持。

文件系统筛选器驱动程序通常会在首次打开文件流时为文件流创建 [每个流的上下文结构](file-streams--stream-contexts--and-per-stream-contexts.md) 。 但是，可以在任何操作期间创建每个流的上下文结构并将其与文件流相关联。

## <a name="allocating-the-per-stream-context"></a>分配 Per-Stream 上下文

可以从分页或非分页池分配每个流的上下文结构。 若要分配每个流的上下文，请调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) ，如以下示例中所示：

```cpp
contextSize = sizeof(SPY_STREAM_CONTEXT) + fileName.Length;
ctx = ExAllocatePoolWithTag(NonPagedPool,
                            contextSize,
                            MYLEGACYFILTER_CONTEXT_TAG);
```

> [!NOTE]
> 如果筛选器从页面缓冲池分配每个流的上下文结构，则无法从其创建完成例程调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 。 这是因为，可以在 DISPATCH_LEVEL IRQL 时调用完成例程。

### <a name="initializing-the-per-stream-context"></a>初始化 Per-Stream 上下文

文件系统筛选器驱动程序调用 [**FsRtlInitPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext) 来初始化每个流的上下文结构。 此例程初始化上下文结构的 FSRTL_PER_STREAM_CONTEXT 部分。  (结构的其余部分是特定于筛选器的 ) 

> [!NOTE]
> 如果筛选器驱动程序只为每个文件流创建一个每流上下文结构，则它应将 *InstanceId* 参数的 **NULL** 传递到 [**FsRtlInitPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)。

筛选器驱动程序可以随时初始化每个流的上下文。 但是，必须在将上下文与文件流关联之前执行此操作。
