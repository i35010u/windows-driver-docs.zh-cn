---
title: 取消注册和卸载 WSK 客户端
description: 取消注册和卸载 WSK 客户端
ms.assetid: dd9030b1-271f-46e4-9139-b49903ca8313
keywords:
- 网络模块注册机构 WDK Winsock 内核
- NMR WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6800f8db8b2e5f05e01837e7675f8a065709cf7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380799"
---
# <a name="unregistering-and-unloading-the-wsk-client"></a>取消注册和卸载 WSK 客户端


使用任何 Winsock Kernel (WSK) 应用程序[网络模块注册机构 (NMR)](network-module-registrar2.md)将附加到 WSK 子系统必须注销 NMR 卸载前倒带。 当 WSK 应用程序中注销使用 NMR 通过调用[ **NmrDeregisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterclient)函数，NMR 调用应用程序的[ *ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_detach_provider_fn)回调函数，以便应用程序可以从 WSK 应用程序的注销过程的一部分的 WSK 子系统中分离本身。

此外，在向 NMR 取消注册 WSK 子系统的可能性不大，但也有可能情况下，NMR 还会调用 WSK 应用程序的*ClientDetachProvider*回调函数，以便应用程序可以分离自身WSK 子系统 WSK 子系统的注销过程的一部分。

NMR 调用 WSK 应用程序的*ClientDetachProvider*仅一次回调函数。 如果 WSK 应用程序和 WSK 子系统中注销 NMR，NMR 调用 WSK 应用程序的*ClientDetachProvider*仅后启动的第一个注销回调函数。

在向任一中 WSK WSK 函数进行任何调用是否\_提供程序\_NMR 调用 WSK 应用程序的次调度*ClientDetachProvider*回调函数、 WSK 应用程序应返回状态\_成功从其*ClientDetachProvider*回调函数。 否则，WSK 应用程序必须返回状态\_PENDING 从其*ClientDetachProvider*回调函数，并且它必须调用[ **NmrClientDetachProviderComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)函数毕竟 WSK 正在进行中，调用的函数中 WSK\_提供程序\_调度已返回。 WSK 应用程序调用**NmrClientDetachProviderComplete**函数，以通知应用程序已从 WSK 子系统分离 NMR。 但是，WSK 子系统将允许所有打开的套接字关闭 WSK 应用程序之前完全完成分离过程。 有关详细信息，请参阅[关闭套接字](closing-a-socket.md)。

WSK 应用程序已通知 NMR 无法进行分离，完成后通过返回状态\_成功从其*ClientDetachProvider*回调函数或通过调用**NmrClientDetachProviderComplete**函数，应用程序必须不调用任何进一步的任何 WSK 函数中 WSK\_提供程序\_调度。

如果 WSK 应用程序实现[ *ClientCleanupBindingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn)回调函数 NMR 调用应用程序的*ClientCleanupBindingContext*回调WSK 应用程序和 WSK 子系统完成彼此分离后的函数。 WSK 应用程序的*ClientCleanupBindingContext*回调函数应执行任何必要的应用程序的绑定上下文结构中包含的数据的清理。 如果应用程序动态分配内存结构，它随后应释放绑定上下文结构的内存。

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

WSK 应用程序的[ **Unload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)函数必须确保将从中注销该应用程序[NMR](network-module-registrar2.md)的应用程序是从系统内存中卸载之前。 WSK 应用程序不能返回从其*Unload*函数之前，从 NMR 完全注销之后。 如果在调用**NmrDeregisterClient**将返回状态\_WSK 应用程序必须调用挂起、 **NmrWaitForClientDeregisterComplete**函数等待的注销完成之前它将返回其*Unload*函数。

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

WSK 应用程序不需要调用**NmrDeregisterClient**从其*卸载*函数。 例如，如果 WSK 程序是一个复杂的驱动程序的子组件，WSK 应用程序子组件停用时，可能会出现 WSK 应用程序的注销。 但是，在这种情况下，驱动程序必须仍确保 WSK 应用程序已得到从 NMR 完全注销之前从返回其*Unload*函数。

 

 





