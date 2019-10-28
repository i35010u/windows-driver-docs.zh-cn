---
title: 注册同步驱动程序通知
description: 注册同步驱动程序通知
ms.assetid: 852a2b69-c71f-4127-946e-8179954d504c
keywords:
- 驱动程序通知 WDK 动态硬件分区，注册
- 同步通知 WDK 动态硬件分区，注册
- 通知 WDK 动态硬件分区，注册
- 同步驱动程序通知 WDK 动态硬件分区，注册
- 注册驱动程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78a186b86d56a0f1d1d03336f0dde6821a0eb15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838462"
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

设备驱动程序通过调用[**KeRegisterProcessorChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterprocessorchangecallback)函数，注册同步驱动程序通知。 设备驱动程序通常从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数内调用**KeRegisterProcessorChangeCallback**函数。 如果设备驱动程序指定了 KE\_处理器\_CHANGE\_添加\_现有标志，则除了调用，还会立即为当前存在于硬件分区中的每个活动处理器调用回调函数。将新处理器添加到硬件分区时。 下面的代码示例演示如何注册同步驱动程序通知：

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

如果设备驱动程序必须停止收到同步驱动程序通知（例如，在卸载该通知时），则它必须通过调用[**KeDeregisterProcessorChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterprocessorchangecallback)函数来注销回调函数。 设备驱动程序通常从其[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数内调用**KeDeregisterProcessorChangeCallback**函数。 下面的代码示例演示如何注销回调函数：

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

 

 




