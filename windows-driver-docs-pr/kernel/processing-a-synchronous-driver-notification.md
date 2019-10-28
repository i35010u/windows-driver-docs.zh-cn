---
title: 处理同步驱动程序通知
description: 处理同步驱动程序通知
ms.assetid: 84e4e05f-1383-4f5f-8fc0-20cd508afa3c
keywords:
- 驱动程序通知 WDK 动态硬件分区，处理
- 同步驱动程序通知 WDK 动态硬件分区，处理
- 注册驱动程序通知 WDK 动态硬件分区，同步
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df7358ac0a555f22d87c67e2db8baad27a66e088
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838490"
---
# <a name="processing-a-synchronous-driver-notification"></a>处理同步驱动程序通知


当操作系统调用注册的回调函数时，它会将一个指针传递到[**KE\_处理器\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_ke_processor_change_notify_context)在*ChangeContext*参数中\_通知\_上下文结构，并将指针传递到在*OperationStatus*参数中包含一个 NTSTATUS 代码。 **KE\_处理器\_更改\_通知\_上下文**结构包含处理器添加操作的状态、要添加的新处理器的处理器编号以及与相关联的 NTSTATUS 代码指示的状态。

将新处理器添加到硬件分区时，操作系统将调用注册的回调函数两次。 操作系统首先调用具有**KeProcessorAddStartNotify**状态的回调函数，然后再启动新的处理器。 如果操作系统成功添加了新的处理器，它将第二次调用回调函数并具有**KeProcessorAddCompleteNotify**状态。 否则，它会第二次调用回调函数并返回**KeProcessorAddFailureNotify**状态。

如果在设备驱动程序注册回调函数时指定了 KE\_处理器\_更改\_添加\_现有标志，则还会为当前存在于中的每个活动处理器立即调用回调函数。硬件分区。 通常情况下，回调函数将不需要区分对现有处理器调用它的时间和为新处理器调用该函数的时间。 有关操作系统何时调用注册的回调函数的详细信息，请参阅[**KeRegisterProcessorChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterprocessorchangecallback)函数的说明。

下面的代码示例演示了用于处理同步驱动程序通知的回调函数的实现：

```cpp
// Synchronous notification callback function
VOID
  SyncProcessorCallback(
    IN PVOID CallbackContext,
    IN PKE_PROCESSOR_CHANGE_NOTIFICATION_CONTEXT ChangeContext,
    IN PNTSTATUS OperationStatus
    )
{
  PNTSTATUS CallbackStatus;
  ULONG ProcessorNumber;
  ULONG ProcessorCount;
  KAFFINITY ActiveProcessors;

  // The CallbackContext contains a pointer to a
  // variable that contains an NTSTATUS code. This
  // is used to pass back any error status to the
  // caller of KeRegisterProcessorChangeCallback.
  CallbackStatus =
    (PNTSTATUS)
      CallbackContext;

  // Get the processor number of the new processor
  ProcessorNumber =
    ChangeContext->NtNumber;

  // Switch on the state of the add operation
  switch (ChangeContext->State)
  {
    // Before the operating system has added the new processor
    case KeProcessorAddStartNotify:

      // Allocate any per-processor data
      // structures for the new processor.
      ...

      // Assign any other per-processor resources
      // to the new processor.
      ...

      // Perform any other necessary preparation
      // for execution of the driver code
      // on the new processor.
      ...

      // If an error occurs such that continuing
      // to add the processor would be fatal
      // (for example, an allocation failure of a
      // per-processor data structure), set the
      // status to an appropriate NTSTATUS code.
      if (...)
      {
        // This returns the status to the operating system.
        *OperationStatus = STATUS_INSUFFICIENT_RESOURCES;

        // This returns the status to the caller of the
        // KeRegisterProcessorChangeCallback function.
        *CallbackStatus = STATUS_INSUFFICIENT_RESOURCES;
      }

      break;

    // The operating system has successfully added the new processor
    case KeProcessorAddCompleteNotify:

      //
      // The following can be performed either here or
      // in an asynchronous notification callback function.
      //

      // Get the current processor count and affinity
      ProcessorCount =
        KeQueryActiveProcessorCount(
          &ActiveProcessors
          );

      // Adjust any resource allocations that are based
      // on the number of processors.
      ...

      // Adjust the assignment of resources that are
      // assigned to specific processors.
      ...

      // Begin scheduling any per-processor threads
      // on the new processor.
      ...

      // Adjust the scheduling of DPCs and other threads
      ...

      // Adjust any load balancing algorithms
      ...

      break;

    // The operating system has failed to add the new processor
    case KeProcessorAddFailureNotify:

      // Clean up and free any per-processor
      // resources that were allocated for the
      // specified processor during the
      // KeProcessorAddStartNotify state.
      ...

      break;
  }
}
```

 

 




