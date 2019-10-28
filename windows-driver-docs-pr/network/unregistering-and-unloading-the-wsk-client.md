---
title: 注销并卸载 WSK 客户端
description: 注销并卸载 WSK 客户端
ms.assetid: dd9030b1-271f-46e4-9139-b49903ca8313
keywords:
- 网络模块注册器 WDK Winsock 内核
- NMR WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5723f955787a0e2e73ddb701ee0c3a559aad12e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843002"
---
# <a name="unregistering-and-unloading-the-wsk-client"></a>注销并卸载 WSK 客户端


使用[网络模块注册器（NMR）](network-module-registrar2.md)附加到 WSK 子系统的任何 Winsock 内核（WSK）应用程序都必须在卸载之前取消注册 NMR。 当 WSK 应用程序通过调用[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)函数向 NMR 取消注册时，NMR 将调用应用程序的[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn)回调函数，以便应用程序可以在WSK 应用程序的注销过程。

此外，在可能的情况下，在 WSK 子系统通过 NMR 进行注销的情况下，NMR 还会调用 WSK 应用程序的*ClientDetachProvider*回调函数，以便应用程序能够作为WSK 子系统的注销过程。

NMR 只调用一次 WSK 应用程序的*ClientDetachProvider*回调函数。 如果 WSK 应用程序和 WSK 子系统都取消注册 NMR，则 NMR 仅在第一次注销开始后才调用 WSK 应用程序的*ClientDetachProvider*回调函数。

如果在 NMR 调用 WSK 应用程序的*ClientDetachProvider*回调函数时没有对 WSK\_提供\_程序中的任何 WSK 函数进行调用，则 WSK 应用程序应返回状态\_其*ClientDetachProvider*回调函数成功。 否则，WSK 应用程序必须从其*ClientDetachProvider*回调函数返回状态\_"挂起"，并且必须在对 WSK 函数进行的所有调用之后调用[**NmrClientDetachProviderComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)函数。已返回 WSK\_提供程序\_调度。 WSK 应用程序调用**NmrClientDetachProviderComplete**函数来通知 NMR 应用程序已与 WSK 子系统分离。 但是，在 WSK 应用程序关闭所有打开的套接字之前，WSK 子系统将不允许完全完成分离过程。 有关详细信息，请参阅[关闭套接字](closing-a-socket.md)。

当 WSK 应用程序通过从其*ClientDetachProvider*回调函数返回状态\_成功或通过调用**NMRCLIENTDETACHPROVIDERCOMPLETE**函数向 NMR 通知分离完成后，应用程序不能对 WSK\_提供程序中的任何 WSK 函数进行任何进一步调用\_调度。

如果 WSK 应用程序实现[*ClientCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn)回调函数，则 NMR 在 WSK 应用程序和 WSK 子系统完成后调用应用程序的*ClientCleanupBindingContext*回调函数分离。 WSK 应用程序的*ClientCleanupBindingContext*回调函数应对应用程序的绑定上下文结构中包含的数据执行任何必要的清理。 如果应用程序为结构动态分配内存，则它应释放绑定上下文结构的内存。

例如：

```C++
// ClientDetachProvider callback function
NTSTATUS
  ClientDetachProvider(
    IN PVOID ClientBindingContext
    )
{
  PWSK_APP_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext =
    (PWSK_APP_BINDING_CONTEXT)ClientBindingContext;

  // Check if there are no calls in progress to any WSK functions
  // in WSK_PROVIDER_DISPATCH and that there are no open sockets
  if (...)
  {
    // Return success status indicating that detachment is complete
    return STATUS_SUCCESS;
  }

  // There are calls in progress to one or more of the WSK functions
  // in WSK_PROVIDER_DISPATCH and/or one or more open sockets
  else
  {
    // Return pending status, indicating that detachment is pending
    // completion of the calls in progress to the WSK functions in
    // WSK_PROVIDER_DISPATCH and/or closing of the open sockets
    return STATUS_PENDING;

    // When all of the calls in progress to the WSK functions
    // in WSK_PROVIDER_DISPATCH are completed, the WSK application
    // must close all open sockets.
    //
    // After all sockets have been closed, the WSK application must
    // call the NmrClientDetachProviderComplete function with the
    // binding handle for the attachment to the WSK subsystem.
  }
}

// ClientCleanupBindingContext callback function
VOID
  ClientCleanupBindingContext(
    IN PVOID ClientBindingContext
    )
{
  PWSK_APP_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext =
    (PWSK_APP_BINDING_CONTEXT)ClientBindingContext;

  // Clean up the binding context structure
  ...

  // Free the memory for client's binding context structure
  ExFreePoolWithTag(
    BindingContext,
    BINDING_CONTEXT_POOL_TAG
    );
}
```

在从系统内存中卸载应用程序之前，WSK 应用程序的[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数必须确保从[NMR](network-module-registrar2.md)中注销该应用程序。 WSK 应用程序在从 NMR 完全注销之前，不能从其*Unload*函数返回。 如果对**NmrDeregisterClient**的调用返回状态\_"挂起"，则 WSK 应用程序必须调用**NmrWaitForClientDeregisterComplete**函数以等待注销完成，然后从其*卸载*返回才能.

例如：

```C++
// Variable containing the handle for registration with the NMR
HANDLE RegistrationHandle;

// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS Status;

  // Unregister the WSK application from the NMR
  Status =
    NmrDeregisterClient(
      RegistrationHandle
      );

  // Check if pending
  if (Status == STATUS_PENDING)
  {
    // Wait for the unregistration to be completed
    NmrWaitForClientDeregisterComplete(
      RegistrationHandle
      );
  }
}
```

不需要 WSK 应用程序从其*Unload*函数中调用**NmrDeregisterClient** 。 例如，如果 WSK 应用程序是复杂驱动程序的子组件，则在禁用 WSK 应用程序子组件时，可能会注销 WSK 应用程序。 但是，在这种情况下，驱动程序必须确保 WSK 应用程序在从其*Unload*函数返回之前已从 NMR 完全注销。

 

 





