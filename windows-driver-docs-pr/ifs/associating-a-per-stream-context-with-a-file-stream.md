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
ms.openlocfilehash: 8d4f928ad63f8075ad9ba4768f6ec64ae289d4ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841493"
---
# <a name="associating-a-per-stream-context-with-a-file-stream"></a>将按流上下文与文件流相关联


## <span id="ddk_associating_a_per_stream_context_with_a_file_stream_if"></span><span id="DDK_ASSOCIATING_A_PER_STREAM_CONTEXT_WITH_A_FILE_STREAM_IF"></span>


仅当文件系统已成功处理[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)请求打开流时，每个流的上下文结构才能与文件流相关联。 这是因为，只有在文件系统处理了 create 请求后，文件系统筛选器驱动程序才能将文件对象的 FsContext 指针视为有效。 由于 FsContext 指针唯一标识一个文件流，因此需要确定该文件对象是否表示该筛选器已经查看的文件流，以及该筛选器已为其创建了每个流的上下文。 出于此原因，在创建调度（或 "预创建"）路径中，筛选器创建每个流上下文的情况并不常见，只是为了在 "创建完成" （或 "创建后"）路径中删除该路径，因为它是重复的。

文件系统筛选器驱动程序调用[**FsRtlLookupPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext)，以检查它是否已与其他每个流上下文关联。

如果[**FsRtlLookupPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext)找到同一文件流的现有每流上下文，则筛选器应删除新创建的每个流的上下文。

如果[**FsRtlLookupPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext)找不到已为文件流预先创建的每个流上下文，筛选器可以调用[**FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)将新创建的流上下文与文件流。

为每个流的上下文调用[**FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)后，文件系统将承担删除和释放它的责任。 如果筛选器驱动程序分配了每个流的上下文，但没有为其调用**FsRtlInsertPerStreamContext** ，则筛选器驱动程序仍负责通过调用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)来释放它。

 

 




