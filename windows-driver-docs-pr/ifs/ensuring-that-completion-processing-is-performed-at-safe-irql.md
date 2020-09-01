---
title: 确保在安全的 IRQL 上执行完成处理
description: 确保在安全的 IRQL 上执行完成处理
ms.assetid: 54487fba-2ced-4bcd-afa6-d56b351aa7d6
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，完成处理
- 完成 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02727b7837f1ada0766263fadfe2fbc110e0f66d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065250"
---
# <a name="ensuring-that-completion-processing-is-performed-at-safe-irql"></a>确保在安全的 IRQL 上执行完成处理


## <span id="ddk_ensuring_that_completion_processing_is_performed_at_safe_irql_if"></span><span id="DDK_ENSURING_THAT_COMPLETION_PROCESSING_IS_PERFORMED_AT_SAFE_IRQL_IF"></span>


如 [编写 Postoperation 回调例程](writing-postoperation-callback-routines.md)中所述，基于 IRP 的 i/o 操作的 [**Postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 可以在 IRQL = 调度 \_ 级别调用，除非微筛选器驱动程序的 PREOPERATION 回调例程通过返回 FLT PREOP SYNCHRONIZE 同步操作， \_ \_ 或者该操作是一种本质上同步的创建操作。  (有关此返回值的详细信息，请参阅 [返回 FLT \_ PREOP \_ SYNCHRONIZE](returning-flt-preop-synchronize.md)。 ) 

但是，对于尚未同步的基于 IRP 的 i/o 操作，微筛选器驱动程序可以使用两种方法来确保完成处理的执行速度为 IRQL &lt; = APC \_ 级别。

第一种方法是，postoperation 回调例程挂起 i/o 操作，直到完成处理才能以 IRQL &lt; = APC \_ 级别执行。 此方法在 [Postoperation 回调例程中挂起 I/o 操作](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)中进行了介绍。

第二种方法是让微微筛选器驱动程序的 postoperation 回调例程来调用 [**FltDoCompletionProcessingWhenSafe**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)。 仅当当前 IRQL 为 = 调度级别时， **FltDoCompletionProcessingWhenSafe** pends i/o 操作 &gt; \_ 。 否则，此例程会立即执行微筛选器驱动程序的 **SafePostCallback** 例程。 此方法在 **FltDoCompletionProcessingWhenSafe**中进行了介绍。

 

