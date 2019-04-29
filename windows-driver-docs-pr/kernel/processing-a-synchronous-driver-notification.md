---
title: 处理同步驱动程序通知
description: 处理同步驱动程序通知
ms.assetid: 84e4e05f-1383-4f5f-8fc0-20cd508afa3c
keywords:
- 驱动程序通知 WDK 动态硬件分区、 处理
- 同步的驱动程序通知 WDK 动态硬件分区、 处理
- 注册驱动程序通知 WDK 动态硬件分区，同步
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c51bf91d66e5eee3bfebee22a8c976ae22e7620
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369099"
---
# <a name="processing-a-synchronous-driver-notification"></a>处理同步驱动程序通知


当操作系统将调用注册的回调函数时，会传递一个指向[ **KE\_处理器\_更改\_通知\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff554229)结构中*ChangeContext*参数和一个指向包含 NTSTATUS 的变量中的代码*OperationStatus*参数。 **KE\_处理器\_更改\_通知\_上下文**结构包含处理器状态添加操作，正在添加的新处理器的处理器数和 NTSTATUS 代码与指示的状态相关联。

当新处理器添加到硬件分区时，操作系统将调用注册的回调函数两次。 操作系统将首先调用回调函数**KeProcessorAddStartNotify**状态，然后将它启动新的处理器。 如果操作系统已成功添加了新的处理器，它调用的回调函数与第二次**KeProcessorAddCompleteNotify**状态。 否则，它调用的回调函数与第二次**KeProcessorAddFailureNotify**状态。

如果 KE\_处理器\_更改\_添加\_现有标志指定当设备驱动程序已注册的回调函数时，还为每个活动处理器立即调用回调函数，硬件分区中当前不存在。 通常情况下，回调函数不会区分针对现有处理器和适用于新处理器调用时调用它。 当操作系统将调用注册的回调函数的详细信息，请参阅的说明[ **KeRegisterProcessorChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff553120)函数。

下面的代码示例显示了处理同步驱动程序通知的回调函数的实现：

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

 

 




