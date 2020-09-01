---
title: 取消注册和卸载 WSK 客户端
description: 取消注册和卸载 WSK 客户端
ms.assetid: dd9030b1-271f-46e4-9139-b49903ca8313
keywords:
- 网络模块注册器 WDK Winsock 内核
- NMR WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e568202f252f02df59aa41ab20592f269f44b1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215779"
---
# <a name="unregistering-and-unloading-the-wsk-client"></a>取消注册和卸载 WSK 客户端


使用 [网络模块注册器 (NMR) ](network-module-registrar2.md) 以附加到 WSK 子系统的任何 Winsock 内核 (WSK) 应用程序都必须在卸载之前取消注册 NMR。 当 WSK 应用程序通过调用 [**NmrDeregisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient) 函数向 NMR 取消注册时，NMR 将调用应用程序的 [*ClientDetachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn) 回调函数，以便应用程序可以在 WSK 应用程序的注销过程中将其自身从 WSK 子系统分离。

此外，在可能的情况下，在 WSK 子系统通过 NMR 进行注销的情况下，NMR 还会调用 WSK 应用程序的 *ClientDetachProvider* 回调函数，以便应用程序可以在 WSK 子系统的注销过程中将其自身从 WSK 子系统中分离出来。

NMR 只调用一次 WSK 应用程序的 *ClientDetachProvider* 回调函数。 如果 WSK 应用程序和 WSK 子系统都取消注册 NMR，则 NMR 仅在第一次注销开始后才调用 WSK 应用程序的 *ClientDetachProvider* 回调函数。

如果 \_ NMR 调用 WSK 应用程序的 ClientDetachProvider 回调函数时，未对 WSK 提供程序调度中的任何 WSK 函数进行调用 \_ ，则 WSK *ClientDetachProvider*应用程序应 \_ 从其*ClientDetachProvider*回调函数返回状态 SUCCESS。 否则，WSK 应用程序必须 \_ 从其 *ClientDetachProvider* 回调函数返回 "挂起" 状态，并且在对 WSK 提供程序调度中的 WSK 函数进行的所有调用都返回后，必须调用 [**NmrClientDetachProviderComplete**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientdetachprovidercomplete) 函数 \_ \_ 。 WSK 应用程序调用 **NmrClientDetachProviderComplete** 函数来通知 NMR 应用程序已与 WSK 子系统分离。 但是，在 WSK 应用程序关闭所有打开的套接字之前，WSK 子系统将不允许完全完成分离过程。 有关详细信息，请参阅 [关闭套接字](closing-a-socket.md)。

当 WSK 应用程序通过 \_ 从其 *ClientDetachProvider* 回调函数返回状态 "成功" 或通过调用 **NmrClientDetachProviderComplete** 函数向 NMR 通知分离完成后，应用程序不能对 WSK \_ 提供程序调度中的任何 WSK 函数进行进一步调用 \_ 。

如果 WSK 应用程序实现 [*ClientCleanupBindingContext*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn) 回调函数，则 NMR 将在 WSK 应用程序和 WSK 子系统都完成分离后，调用应用程序的 *ClientCleanupBindingContext* 回调函数。 WSK 应用程序的 *ClientCleanupBindingContext* 回调函数应对应用程序的绑定上下文结构中包含的数据执行任何必要的清理。 如果应用程序为结构动态分配内存，则它应释放绑定上下文结构的内存。

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

在从系统内存中卸载应用程序之前，WSK 应用程序的 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数必须确保从 [NMR](network-module-registrar2.md) 中注销该应用程序。 WSK 应用程序在从 NMR 完全注销之前，不能从其 *Unload* 函数返回。 如果对 **NmrDeregisterClient** 的调用返回状态 " \_ 挂起"，则 WSK 应用程序必须调用 **NmrWaitForClientDeregisterComplete** 函数以等待注销完成，然后再从其 *Unload* 函数返回。

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

不需要 WSK 应用程序从其*Unload*函数中调用**NmrDeregisterClient** 。 例如，如果 WSK 应用程序是复杂驱动程序的子组件，则在禁用 WSK 应用程序子组件时，可能会注销 WSK 应用程序。 但是，在这种情况下，驱动程序必须确保 WSK 应用程序在从其 *Unload* 函数返回之前已从 NMR 完全注销。

 

