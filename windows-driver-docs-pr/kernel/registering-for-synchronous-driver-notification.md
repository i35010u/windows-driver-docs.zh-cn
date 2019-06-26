---
title: 注册同步驱动程序通知
description: 注册同步驱动程序通知
ms.assetid: 852a2b69-c71f-4127-946e-8179954d504c
keywords:
- 驱动程序通知 WDK 动态硬件分区、 注册
- 同步通知--WDK 各种动态的硬件，分区、 注册
- 通知--WDK 各种动态的硬件，分区、 注册
- 同步的驱动程序通知 WDK 动态硬件分区、 注册
- 注册的驱动程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69f5b8865e4fbae5c422f79a101b140c7ef7ae9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373447"
---
# <a name="registering-for-synchronous-driver-notification"></a>注册同步驱动程序通知


若要使用同步的驱动程序通知，设备驱动程序实现动态硬件分区添加新的处理器时，操作系统将调用的回调函数。 下面的代码示例是此类回调函数的原型：

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

设备驱动程序通过调用注册同步驱动程序通知[ **KeRegisterProcessorChangeCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterprocessorchangecallback)函数。 设备驱动程序通常会调用**KeRegisterProcessorChangeCallback**中的函数及其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数。 如果设备驱动程序指定 KE\_处理器\_更改\_添加\_现有标志，为每个活动的处理器中当前存在在硬件分区中，立即调用回调函数对新处理器添加到硬件分区时要调用的补充。 下面的代码示例演示如何注册用于同步的驱动程序通知：

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

当设备驱动程序必须停止接收同步的驱动程序通知，例如当正在卸载它，它必须通过调用来注销回调函数[ **KeDeregisterProcessorChangeCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterprocessorchangecallback)函数。 设备驱动程序通常会调用**KeDeregisterProcessorChangeCallback**中的函数及其[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)函数。 下面的代码示例演示如何取消注册回调函数：

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

 

 




