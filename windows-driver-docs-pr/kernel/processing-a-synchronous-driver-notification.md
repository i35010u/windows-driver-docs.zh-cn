---
title: 处理同步驱动程序通知
description: 处理同步驱动程序通知
keywords:
- 驱动程序通知 WDK 动态硬件分区，处理
- 同步驱动程序通知 WDK 动态硬件分区，处理
- 注册驱动程序通知 WDK 动态硬件分区，同步
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5673375f267404ce9d88babd8efb55f358878a83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805419"
---
# <a name="processing-a-synchronous-driver-notification"></a>处理同步驱动程序通知


当操作系统调用注册的回调函数时，它会将指针传递到 *ChangeContext* 参数中的 [**KE \_ PROCESSOR \_ CHANGE \_ 通知 \_ 上下文**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_ke_processor_change_notify_context)结构，并将指针传递到 *OperationStatus* 参数中包含 NTSTATUS 代码的变量。 **KE \_ processor \_ CHANGE \_ 通知 \_ 上下文** 结构包含处理器添加操作的状态、要添加的新处理器的处理器编号，以及与指示的状态关联的 NTSTATUS 代码。

将新处理器添加到硬件分区时，操作系统将调用注册的回调函数两次。 操作系统首先调用具有 **KeProcessorAddStartNotify** 状态的回调函数，然后再启动新的处理器。 如果操作系统成功添加了新的处理器，它将第二次调用回调函数并具有 **KeProcessorAddCompleteNotify** 状态。 否则，它会第二次调用回调函数并返回 **KeProcessorAddFailureNotify** 状态。

如果在 \_ \_ \_ \_ 设备驱动程序注册回调函数时指定了 KE PROCESSOR CHANGE ADD 现有标志，则对于当前存在于硬件分区中的每个活动处理器，还会立即调用回调函数。 通常情况下，回调函数将不需要区分对现有处理器调用它的时间和为新处理器调用该函数的时间。 有关操作系统何时调用注册的回调函数的详细信息，请参阅 [**KeRegisterProcessorChangeCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterprocessorchangecallback) 函数的说明。

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

 

