---
title: 从提供程序模块分离客户端模块
description: 从提供程序模块分离客户端模块
ms.assetid: 148c1a90-0fef-4b22-bf7e-f35285f1bc55
keywords:
- 客户端模块 WDK 网络模块注册器，分离
- NmrDeregisterClient
- 网络模块 WDK 网络模块注册器，分离
- 注销网络模块
- 网络模块注册 WDK，分离网络模块
- NMR WDK，分离网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4c26fdda7a295f851c9dd23edb8e9cfea8dbc8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838156"
---
# <a name="detaching-a-client-module-from-a-provider-module"></a>从提供程序模块分离客户端模块


当客户端模块通过调用[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)函数与网络模块注册器（NMR）注销时，NMR 将调用客户端模块的[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn)回调函数，一次针对每个提供程序模块。附加了，以便客户端模块可以在客户端模块的注销过程中将其自身与所有提供程序模块分离。

此外，每当通过调用[**NmrDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)函数将客户端模块附加到的提供程序模块与 NMR 注销时，NMR 还会调用客户端模块的[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn)回调函数，以便在提供程序模块的注销过程中，客户端模块可以将自身从提供程序模块中分离出来。

调用[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn)回调函数之后，客户端模块不能对任何提供程序模块的[网络编程接口（NPI）](network-programming-interface.md)函数进行进一步调用。 如果在调用客户端模块的*ClientDetachProvider*回调函数时，未对任何提供程序模块的 NPI 函数进行正在进行的调用，则*ClientDetachProvider*回调函数应返回状态\_辉煌.

如果在调用客户端模块的[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn)回调函数时，正在对一个或多个提供程序模块的 NPI 函数进行正在进行的调用，则*ClientDetachProvider*回调函数应返回状态\_未. 在这种情况下，当对提供程序模块的 NPI 函数的所有正在进行的调用都完成之后，客户端模块必须调用[**NmrClientDetachProviderComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)函数。 对**NmrClientDetachProviderComplete**的调用通知 NMR 提供程序模块的客户端模块的分离已完成。

有关如何跟踪对提供程序模块的 NPI 函数的正在进行的调用数的详细信息，请参阅[编程注意事项](programming-considerations.md)。

如果客户端模块实现[*ClientCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn)回调函数，则在客户端模块和提供程序模块完成后，NMR 将调用客户端模块的*ClientCleanupBindingContext*回调函数分离。 客户端模块的*ClientCleanupBindingContext*回调函数应对客户端模块的绑定上下文结构中包含的数据执行任何必要的清理。 如果客户端模块为结构动态分配内存，则它应释放绑定上下文结构的内存。

例如：

```C++
// ClientDetachProvider callback function
NTSTATUS
  ClientDetachProvider(
    IN PVOID ClientBindingContext
    )
{
  PCLIENT_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PCLIENT_BINDING_CONTEXT)ClientBindingContext;

  // Set a flag indicating that the client module is detaching
  // from the provider module so that no more calls are made to
  // the provider module's NPI functions.
  ...

  // Check if there are no in-progress NPI function calls to the
  // provider module
  if (...)
  {
    // Return success status indicating detachment is complete
    return STATUS_SUCCESS;
  }

  // There are one or more in-progress NPI function calls
  // to the provider module
  else
  {
    // Return pending status indicating detachment is pending
    // completion of the in-progress NPI function calls
    return STATUS_PENDING;

    // When the last in-progress call to the provider module's
    // NPI functions completes, the client module must call
    // NmrClientDetachProviderComplete() with the binding handle
    // for the attachment to the provider module.
  }
}

// ClientCleanupBindingContext callback function
VOID
  ClientCleanupBindingContext(
    IN PVOID ClientBindingContext
    )
{
  PCLIENT_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PCLIENT_BINDING_CONTEXT)ClientBindingContext;

  // Clean up the client binding context structure
  ...

  // Free the memory for client's binding context structure
  ExFreePoolWithTag(
    BindingContext,
    BINDING_CONTEXT_POOL_TAG
    );
}
```

 

 





