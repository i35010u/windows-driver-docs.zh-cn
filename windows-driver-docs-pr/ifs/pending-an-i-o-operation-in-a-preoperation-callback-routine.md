---
title: 在预操作回调例程中挂起 I/O 操作
description: 在预操作回调例程中挂起 I/O 操作
ms.assetid: 39b04911-c0d9-42ec-b93e-b440b12f9e41
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器中的挂起的操作
- 挂起的回调例程 WDK 中的 I/O 操作文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c28659e301e7e85bc0db0319cec681159173430
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564757"
---
# <a name="pending-an-io-operation-in-a-preoperation-callback-routine"></a>在预操作回调例程中挂起 I/O 操作


## <span id="ddk_pending_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)挂起 I/O 操作可以通过将发布到系统工作队列的操作并返回 FLT\_PREOP\_PENDING。 返回此状态的值，则表示它调用之前，保持微筛选器驱动程序的 I/O 操作的控件[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913)恢复的 I/O 操作的处理。

微筛选器驱动程序的 preoperation 回调例程等待 I/O 操作，请执行以下步骤：

1.  通过调用一个例程，如发布到系统工作队列的 I/O 操作[ **FltQueueDeferredIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff543449)。

2.  返回 FLT\_PREOP\_PENDING。

与微筛选器驱动程序，必须挂起所有 （或大多数） 传入的 I/O 操作不应使用如例程**FltQueueDeferredIoWorkItem**挂起操作，因为调用此例程会导致系统工作队列为来路。 相反，这样的微筛选器驱动程序应使用取消安全队列。 有关使用取消安全队列的详细信息，请参阅[ *FltCbdqInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff541802)。

请注意，在调用**FltQueueDeferredIoWorkItem**如果任意下列条件为 true，则将失败：

-   该操作不是一个基于 IRP 的 I/O 操作。

-   操作已在分页 I/O 操作。

-   **TopLevelIrp**当前线程的字段不是**NULL**。 (有关如何查找此字段的值的详细信息，请参阅[ **IoGetTopLevelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548405)。)

-   正在销毁 I/O 操作的目标实例。

如果微筛选器驱动程序的 preoperation 回调例程将返回 FLT\_PREOP\_挂起，它必须返回**NULL**中*CompletionContext*输出参数。

微筛选器驱动程序可以返回 FLT\_PREOP\_PENDING 仅为基于 IRP 的 I/O 操作。 若要确定操作是否是基于 IRP 的 I/O 操作，请使用[ **FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)宏。

取消排队和正在处理 I/O 操作的工作例程必须调用**FltCompletePendedPreOperation**恢复操作的处理。

 

 




