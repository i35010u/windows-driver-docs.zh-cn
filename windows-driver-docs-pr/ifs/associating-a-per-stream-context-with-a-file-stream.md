---
title: 将按流上下文与文件流相关联
description: 将按流上下文与文件流相关联
ms.assetid: 99c93574-2ba6-417a-89a4-a5b9a350a8da
keywords:
- 筛选器驱动程序，WDK 文件系统，每流上下文跟踪
- 文件系统筛选器驱动程序 WDK，每流上下文跟踪
- 每流上下文跟踪 WDK 文件系统
- 跟踪每个流的上下文 WDK 文件系统
- 关联每个流的上下文 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e47dc00ff501cae73a611c3aa9e3129d65ac23
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065406"
---
# <a name="associating-a-per-stream-context-with-a-file-stream"></a>将按流上下文与文件流相关联


## <span id="ddk_associating_a_per_stream_context_with_a_file_stream_if"></span><span id="DDK_ASSOCIATING_A_PER_STREAM_CONTEXT_WITH_A_FILE_STREAM_IF"></span>


仅当文件系统已成功处理 [**IRP \_ MJ \_ CREATE**](./irp-mj-create.md) 请求以打开流后，每个流的上下文结构才能与文件流相关联。 这是因为，只有在文件系统处理了 create 请求后，文件系统筛选器驱动程序才能将文件对象的 FsContext 指针视为有效。 由于 FsContext 指针唯一标识一个文件流，因此需要确定该文件对象是否表示该筛选器已经查看的文件流，以及该筛选器已为其创建了每个流的上下文。 出于此原因，筛选器在创建调度 (或 "预创建" ) 路径中创建每个流上下文的情况并不常见，只是为了在 "创建完成" (或 "后期创建" ) 路径中删除该上下文，因为它是重复的。

文件系统筛选器驱动程序调用 [**FsRtlLookupPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext)，以检查它是否已与其他每个流上下文关联。

如果 [**FsRtlLookupPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext) 找到同一文件流的现有每流上下文，则筛选器应删除新创建的每个流的上下文。

如果 [**FsRtlLookupPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext) 找不到已为文件流预先创建的每个流上下文，筛选器可以调用 [**FsRtlInsertPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinsertperstreamcontext) 将新创建的流上下文与文件流相关联。

为每个流的上下文调用 [**FsRtlInsertPerStreamContext**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinsertperstreamcontext) 后，文件系统将承担删除和释放它的责任。 如果筛选器驱动程序分配了每个流的上下文，但没有为其调用 **FsRtlInsertPerStreamContext** ，则筛选器驱动程序仍负责通过调用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)来释放它。

 

