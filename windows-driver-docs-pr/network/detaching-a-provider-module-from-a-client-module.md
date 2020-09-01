---
title: 从客户端模块分离提供程序模块
description: 从客户端模块分离提供程序模块
ms.assetid: 011d0770-6942-480e-95ee-88a2903822b2
keywords:
- 提供商模块 WDK 网络模块注册程序，分离
- 网络模块 WDK 网络模块注册器，分离
- 注销网络模块
- 网络模块注册 WDK，分离网络模块
- NMR WDK，分离网络模块
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c8ce3d9993979669ffb79fac6c9a0759060b4fc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209789"
---
# <a name="detaching-a-provider-module-from-a-client-module"></a>从客户端模块分离提供程序模块


当通过调用 [**NmrDeregisterProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider) 函数与网络模块注册器注销的提供程序模块 (NMR) 时，NMR 将调用提供程序模块的 [*ProviderDetachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) 回调函数，对它所附加到的每个客户端模块一次，以便提供程序模块可以在提供程序模块的注销过程中将其自身与所有客户端模块分离。

此外，每当提供程序模块通过调用 [**NmrDeregisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient) 函数与 NMR 连接到的客户端模块时，NMR 还将调用提供程序模块的 [*ProviderDetachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) 回调函数，以便提供程序模块可在客户端模块的注销过程中将其自身与客户端模块分离。

调用 [*ProviderDetachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) 回调函数后，提供程序模块不能对任何客户端模块的网络编程接口进行进一步调用， [ (NPI) ](network-programming-interface.md) 回调函数。 如果调用提供程序模块的 *ProviderDetachClient* 回调函数时，未对任何客户端模块的 NPI 回调函数进行正在进行的调用，则 *ProviderDetachClient* 回调函数应返回状态 "成功" \_ 。

如果调用提供程序模块的 [*ProviderDetachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) 回调函数时，正在对一个或多个客户端模块的 NPI 回调函数进行正在进行的调用，则 *ProviderDetachClient* 回调函数应返回状态 " \_ 挂起"。 在这种情况下，在对客户端模块的 NPI 回调函数进行的所有正在进行的调用完成后，提供程序模块必须调用 [**NmrProviderDetachClientComplete**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrproviderdetachclientcomplete) 函数。 对 **NmrProviderDetachClientComplete** 的调用通知 NMR，客户端模块中的提供程序模块的分离已完成。

有关如何跟踪对客户端模块的 NPI 回调函数正在进行的调用数的详细信息，请参阅 [编程注意事项](programming-considerations.md)。

如果提供程序模块实现 [*ProviderCleanupBindingContext*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_cleanup_binding_context_fn) 回调函数，则在提供程序模块和客户端模块都完成分离后，NMR 将调用提供程序模块的 *ProviderCleanupBindingContext* 回调函数。 提供程序模块的 *ProviderCleanupBindingContext* 回调函数应对提供程序模块的绑定上下文结构中包含的数据执行任何必要的清理。 如果提供程序模块动态分配了结构的内存，则它应释放绑定上下文结构的内存。

例如：

```C++
// ProviderDetachClient callback function
NTSTATUS
  ProviderDetachClient(
    IN PVOID ProviderBindingContext
    )
{
  PPROVIDER_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PPROVIDER_BINDING_CONTEXT)ProviderBindingContext;

  // Set a flag indicating that the provider module is detaching
  // from the client module so that no more calls are made to
  // the client module's NPI callback functions.
  ...

  // Check if there are no in-progress NPI callback function calls
  // to the client module
  if (...)
  {
    // Return success status indicating detachment is complete
    return STATUS_SUCCESS;
  }

  // There are one or more in-progress NPI callback function
  // calls to the client module
  else
  {
    // Return pending status indicating detachment is pending
    // completion of the in-progress NPI callback function calls
    return STATUS_PENDING;

    // When the last in-progress call to the client module's
    // NPI callback functions completes, the provider module
    // must call NmrProviderDetachClientComplete() with the
    // binding handle for the attachment to the client module.
  }
}

// ProviderCleanupBindingContext callback function
VOID
  ProviderCleanupBindingContext(
    IN PVOID ProviderBindingContext
    )
{
  PPROVIDER_BINDING_CONTEXT BindingContext;

  // Get a pointer to the binding context
  BindingContext = (PPROVIDER_BINDING_CONTEXT)ProviderBindingContext;

  // Clean up the provider binding context structure
  ...

  // Free the memory for provider's binding context structure
  ExFreePoolWithTag(
    BindingContext,
    BINDING_CONTEXT_POOL_TAG
    );
}
```

 

