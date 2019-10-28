---
title: 确保在安全的 IRQL 上执行完成处理
description: 确保在安全的 IRQL 上执行完成处理
ms.assetid: 54487fba-2ced-4bcd-afa6-d56b351aa7d6
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，完成处理
- 完成 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a83d64463151bb74641ad4c0a4fb6d6df832e92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841427"
---
# <a name="ensuring-that-completion-processing-is-performed-at-safe-irql"></a>确保在安全的 IRQL 上执行完成处理


## <span id="ddk_ensuring_that_completion_processing_is_performed_at_safe_irql_if"></span><span id="DDK_ENSURING_THAT_COMPLETION_PROCESSING_IS_PERFORMED_AT_SAFE_IRQL_IF"></span>


如[编写 Postoperation 回调例程](writing-postoperation-callback-routines.md)中所述，基于 IRP 的 i/o 操作的[**Postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)可以在 IRQL = 调度\_级别调用，除非微筛选器驱动程序的 preoperation 回调例程同步操作的方法是：返回 FLT\_PREOP\_SYNCHRONIZE，或操作为创建操作，该操作本质上是同步的。 （有关此返回值的详细信息，请参阅[返回 FLT\_PREOP\_SYNCHRONIZE](returning-flt-preop-synchronize.md)。）

但是，对于尚未同步的基于 IRP 的 i/o 操作，微筛选器驱动程序可使用两种方法来确保完成处理的执行速度为 IRQL &lt;= APC\_级别。

第一种方法是，postoperation 回调例程挂起 i/o 操作，直到完成处理才能以 IRQL &lt;= APC\_级别执行。 此方法在[Postoperation 回调例程中挂起 I/o 操作](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)中进行了介绍。

第二种方法是让微微筛选器驱动程序的 postoperation 回调例程来调用[**FltDoCompletionProcessingWhenSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)。 仅当当前 IRQL 为 &gt;= 调度\_级别时， **FltDoCompletionProcessingWhenSafe** pends i/o 操作。 否则，此例程会立即执行微筛选器驱动程序的**SafePostCallback**例程。 此方法在**FltDoCompletionProcessingWhenSafe**中进行了介绍。

 

 




