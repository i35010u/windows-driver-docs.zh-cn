---
title: 将按流上下文与文件流相关联
description: 将按流上下文与文件流相关联
ms.assetid: 99c93574-2ba6-417a-89a4-a5b9a350a8da
keywords:
- 筛选器驱动程序 WDK 文件系统中，每个流的上下文跟踪
- 文件系统筛选器驱动程序 WDK，跟踪每个流上下文
- 每个流上下文跟踪 WDK 文件系统
- 跟踪每个流上下文 WDK 文件系统
- 将每个流上下文 WDK 文件系统相关联
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2bd8e2f78a5f4ad35a1ef36d72696e700b70b1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322311"
---
# <a name="associating-a-per-stream-context-with-a-file-stream"></a>将按流上下文与文件流相关联


## <span id="ddk_associating_a_per_stream_context_with_a_file_stream_if"></span><span id="DDK_ASSOCIATING_A_PER_STREAM_CONTEXT_WITH_A_FILE_STREAM_IF"></span>


仅在文件系统已成功处理后，每个流上下文结构可以是与文件流相关联[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)请求打开流。 这是因为它是仅后的文件系统已处理的文件对象的 FsContext 指针可以被视为有效的文件系统筛选器驱动程序创建请求。 FsContext 指针唯一标识文件流，因为它确定所需文件的对象是否表示文件流已看到筛选器-并为其筛选器已创建的每个流上下文。 出于此原因，它不是异常筛选器的每个流上下文创建调度 （或"预先创建"） 在路径中创建，只是为了创建完成 （或"后创建"） 路径中删除它，因为证明重复。

若要检查是否它已经关联另一个的每个流上下文与相同的文件流，文件系统筛选器驱动程序调用[ **FsRtlLookupPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546945)。

如果[ **FsRtlLookupPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546945)查找现有的每个流上下文的同一个文件流，该筛选器应删除新创建的每个流上下文。

如果[ **FsRtlLookupPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546945)不会不查找每个流上下文筛选器创建的以前的文件流，该筛选器可以调用[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)将新创建的流上下文与文件流相关联。

之后[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)调用为每个流的上下文中，文件系统假定删除和释放它的职责。 如果筛选器驱动程序分配的每个流上下文，并不会调用**FsRtlInsertPerStreamContext**筛选器驱动程序，是仍要负责释放通过调用[ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590).

 

 




