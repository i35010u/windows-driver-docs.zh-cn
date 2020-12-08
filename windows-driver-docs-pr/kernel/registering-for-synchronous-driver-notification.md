---
title: 注册同步驱动程序通知
description: 注册同步驱动程序通知
keywords:
- 驱动程序通知 WDK 动态硬件分区，注册
- 同步通知 WDK 动态硬件分区，注册
- 通知 WDK 动态硬件分区，注册
- 同步驱动程序通知 WDK 动态硬件分区，注册
- 注册驱动程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea547c2956066bfd01a4f0ecd46d4e26452d5c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837703"
---
# <a name="registering-for-synchronous-driver-notification"></a>注册同步驱动程序通知


若要使用同步驱动程序通知，设备驱动程序可实现一个回调函数，当你将新处理器动态添加到硬件分区时，操作系统将调用此函数。 下面的代码示例是此类回调函数的原型：

```cpp
// Prototype for the synchronous
// notification callback function
VOID
  SyncProcessorCallback(
    IN PVOID CallbackContext,
    IN PKE_PROCESSOR_CHANGE_NOTIFY_CONTEXT ChangeContext,
    IN PNTSTATUS OperationStatus
    );
```

设备驱动程序通过调用 [**KeRegisterProcessorChangeCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterprocessorchangecallback) 函数，注册同步驱动程序通知。 设备驱动程序通常从其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数内调用 **KeRegisterProcessorChangeCallback** 函数。 如果设备驱动程序指定了 KE \_ processor \_ CHANGE \_ ADD \_ 现有标志，则除了在将新处理器添加到硬件分区时，还会调用当前存在于硬件分区中的每个活动处理器的回调函数。 下面的代码示例演示如何注册同步驱动程序通知：

```cpp
PVOID CallbackRegistrationHandle;
NTSTATUS CallbackStatus = STATUS_SUCCESS;

// The driver's DriverEntry routine
NTSTATUS  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  ...

  // Register the callback function
  CallbackRegistrationHandle =
    KeRegisterProcessorChangeCallback(
      SyncProcessorCallback,
      &CallbackStatus,
      KE_PROCESSOR_CHANGE_ADD_EXISTING
      );

  // Check the result
  if (CallbackRegistrationHandle == NULL)
  {
    // Perform any necessary cleanup
    ...

    // Check the callback status
    if (CallbackStatus != STATUS_SUCCESS)
    {
      // Return the error status from the callback function
      return CallbackStatus;
    }
    else
    {
      // Return a generic error status
      return STATUS_UNSUCCESSFUL;
    }
  }

  ...

  return STATUS_SUCCESS;
}
```

如果设备驱动程序必须停止收到同步驱动程序通知（例如，在卸载该通知时），则它必须通过调用 [**KeDeregisterProcessorChangeCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterprocessorchangecallback) 函数来注销回调函数。 设备驱动程序通常从其 [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数内调用 **KeDeregisterProcessorChangeCallback** 函数。 下面的代码示例演示如何注销回调函数：

```cpp
// The driver's Unload routine
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    );
{
  ...

  // Unregister the callback function
  KeDeregisterProcessorChangeCallback(
    CallbackRegistrationHandle
    );

  ...
}
```

 

