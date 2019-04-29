---
title: 从客户端模块分离提供程序模块
description: 从客户端模块分离提供程序模块
ms.assetid: 011d0770-6942-480e-95ee-88a2903822b2
keywords:
- 提供程序模块 WDK 网络模块注册机构，分离
- 网络模块 WDK 网络模块注册机构，分离
- 取消注册网络模块
- 网络模块注册机构 WDK，分离网络模块
- NMR WDK，分离网络模块
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6852d48f426a1c09c124eb1d510dc694e9ef3a51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364232"
---
# <a name="detaching-a-provider-module-from-a-client-module"></a>从客户端模块分离提供程序模块


当提供程序模块注销与网络模块注册机构 (NMR) 通过调用[ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)函数，NMR 调用提供程序模块[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)回调函数，一次它附加到，以便提供程序模块可以从所有客户端模块本身分离，如提供程序模块的一部分的取消注册过程的每个客户端模块.

此外，每当对客户端模块附加提供程序模块会向 NMR 通过调用[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)函数，NMR 还调用提供程序模块[*ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)回调函数，以便提供程序模块可以分离客户端模块根据客户端模块的一部分的取消注册过程。

后其[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)调用回调函数、 提供程序模块必须不执行任何客户端模块的任何进一步调用[网络编程接口 (NPI)](network-programming-interface.md)回调函数。 如果不有任何正在进行中调用任何客户端模块 NPI 回调函数时提供程序模块*ProviderDetachClient*调用回调函数，则*ProviderDetachClient*回调函数应返回状态\_成功。

如果没有正在进行中的一个或多个客户端调用模块的 NPI 回调函数时提供程序模块[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)调用回调函数，则*ProviderDetachClient*回调函数应返回状态\_PENDING。 在这种情况下，必须调用提供程序模块[ **NmrProviderDetachClientComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568781)函数后对客户端模块 NPI 回调函数的所有正在进行中调用已完成。 在调用**NmrProviderDetachClientComplete**通知 NMR 的客户端模块中的提供程序模块中分离已完成。

有关如何跟踪正在进行中对客户端模块的 NPI 回调函数的调用数的详细信息，请参阅[编程注意事项](programming-considerations.md)。

如果实现了提供程序模块[ *ProviderCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff570396)回调函数 NMR 调用提供程序模块*ProviderCleanupBindingContext*提供程序模块和客户端模块均已完成从彼此分离后的回调函数。 提供程序模块*ProviderCleanupBindingContext*回调函数应执行任何必要的提供程序模块的绑定上下文结构中包含的数据的清理。 如果提供程序模块动态分配内存结构，它随后应释放绑定上下文结构的内存。

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

 

 





