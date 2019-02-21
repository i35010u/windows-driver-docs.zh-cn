---
title: 分离的提供程序模块提供的客户端模块
description: 分离的提供程序模块提供的客户端模块
ms.assetid: 148c1a90-0fef-4b22-bf7e-f35285f1bc55
keywords:
- 客户端模块 WDK 网络模块注册机构，分离
- NmrDeregisterClient
- 网络模块 WDK 网络模块注册机构，分离
- 取消注册网络模块
- 网络模块注册机构 WDK，分离网络模块
- NMR WDK，分离网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ca2986211eac16cc57b6d94459d87131a5a7bbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521684"
---
# <a name="detaching-a-client-module-from-a-provider-module"></a>分离的提供程序模块提供的客户端模块


当客户端模块注销与网络模块注册机构 (NMR) 通过调用[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)函数，NMR 调用客户端模块[ *ClientDetachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544908)回调函数，一次它附加到，以便客户端模块可以从所有提供程序模块本身分离，如客户端模块的一部分的取消注册过程的每个提供程序模块.

此外，只要提供程序模块到附加的客户端模块会向 NMR 通过调用[ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)函数，NMR 还调用客户端模块[*ClientDetachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544908)回调函数，以便客户端模块可以分离的提供程序模块如提供程序模块的一部分的取消注册过程。

后其[ *ClientDetachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544908)调用回调函数中，客户端模块必须不执行任何提供程序模块的任何进一步调用[网络编程接口 (NPI)](network-programming-interface.md)函数。 如果对任何提供程序模块 NPI 函数没有正在进行中的调用时客户端模块*ClientDetachProvider*调用回调函数，则*ClientDetachProvider*回调函数应返回状态\_成功。

如果没有正在进行中的一个或多个提供程序调用模块的 NPI 函数时客户端模块[ *ClientDetachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544908)调用回调函数，则*ClientDetachProvider*回调函数应返回状态\_PENDING。 在这种情况下，必须调用客户端模块[ **NmrClientDetachProviderComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568772)函数后对提供程序模块 NPI 函数的所有正在进行中调用已完成。 在调用**NmrClientDetachProviderComplete**通知 NMR 分离的提供程序模块中的客户端模块的已完成。

有关如何跟踪提供程序模块的 NPI 函数的正在进行中调用的数量的详细信息，请参阅[编程注意事项](programming-considerations.md)。

如果客户端模块实现[ *ClientCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff544904)回调函数 NMR 调用客户端模块*ClientCleanupBindingContext*回调客户端模块和提供程序模块均已完成从彼此分离后的函数。 客户端模块*ClientCleanupBindingContext*回调函数应执行任何必要的客户端模块的绑定上下文结构中包含的数据的清理。 如果客户端模块动态分配内存结构，它随后应释放绑定上下文结构的内存。

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
  // the provider module&#39;s NPI functions.
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

    // When the last in-progress call to the provider module&#39;s
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

  // Free the memory for client&#39;s binding context structure
  ExFreePoolWithTag(
    BindingContext,
    BINDING_CONTEXT_POOL_TAG
    );
}
```

 

 





