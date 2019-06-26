---
title: 确保在安全的 IRQL 上执行完成处理
description: 确保在安全的 IRQL 上执行完成处理
ms.assetid: 54487fba-2ced-4bcd-afa6-d56b351aa7d6
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，完成处理
- 完成 I/O 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd8a46d0a4c5a143c66a6fc10ef42c7581598fdb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386100"
---
# <a name="ensuring-that-completion-processing-is-performed-at-safe-irql"></a>确保在安全的 IRQL 上执行完成处理


## <span id="ddk_ensuring_that_completion_processing_is_performed_at_safe_irql_if"></span><span id="DDK_ENSURING_THAT_COMPLETION_PROCESSING_IS_PERFORMED_AT_SAFE_IRQL_IF"></span>


如中所述[写入 Postoperation 回调例程](writing-postoperation-callback-routines.md)，则[ **postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)基于 IRP 的 I/O 操作可以调用在 IRQL = 调度\_级别，除非微筛选器驱动程序的 preoperation 回调例程同步操作通过返回 FLT\_PREOP\_同步或操作是一个 create 操作，这是本质上的同步。 (有关此返回值的详细信息，请参阅[返回 FLT\_PREOP\_同步](returning-flt-preop-synchronize.md)。)

但是，对于已不同步的基于 IRP 的 I/O 操作，微筛选器驱动程序可以使用到两种方法来确保完成处理执行在 IRQL &lt;= APC\_级别。

第一项技术是 postoperation 回调例程挂起 I/O 操作直到完成处理可以执行在 IRQL &lt;= APC\_级别。 此方法中所述[Postoperation 回调例程中的挂起 I/O 操作](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)。

第二种方法是为微筛选器驱动程序的 postoperation 回调例程来调用[ **FltDoCompletionProcessingWhenSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)。 **FltDoCompletionProcessingWhenSafe**等待 I/O 操作仅当为当前 IRQL &gt;= 调度\_级别。 否则，此例程执行微筛选器驱动程序**SafePostCallback**立即例程。 此方法中所述**FltDoCompletionProcessingWhenSafe**。

 

 




