---
title: 将客户端模块附加到提供程序模块
description: 将客户端模块附加到提供程序模块
ms.assetid: 351c07f6-186a-4f47-95f8-c94084ff68fb
keywords:
- 附加网络模块
- 注册网络模块
- 网络模块注册机构 WDK，附加网络模块
- NMR WDK，附加网络模块
- 客户端模块 WDK 网络模块注册机构，附加
- 网络模块 WDK 网络模块注册机构，附件
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abd60a45c908fc4b59ad854fb5ad530743e5396b
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349890"
---
# <a name="attaching-a-client-module-to-a-provider-module"></a>将客户端模块附加到提供程序模块


NMR 客户端模块已注册的网络模块注册机构 (NMR) 后，调用客户端模块[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)回调函数，一次为每个提供程序模块注册为相同的提供商[网络编程接口 (NPI)](network-programming-interface.md)的客户端模块已注册的客户端为。

NMR 还会调用的客户端模块[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)回调函数，每当新的提供程序模块将注册为同一 NPI 作为客户端为其客户端模块已注册的提供程序.

当 NMR 调用客户端模块[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)回调函数对于特定的提供程序模块，该测试通过，在*ProviderRegistrationInstance*参数，指向[ **NPI\_注册\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff568815)结构，它是与提供程序模块相关联。 客户端模块*ClientAttachProvider*回调函数可以使用提供程序模块中的数据**NPI\_注册\_实例**结构，以及中的数据[ **NPI\_MODULEID** ](https://msdn.microsoft.com/library/windows/hardware/ff568813)结构和 NPI 特定于提供程序特征结构指向**ModuleId**和**NpiSpecificCharacteristics**成员提供程序模块**NPI\_注册\_实例**结构，以确定它将附加到提供程序模块。

如果客户端模块确定它会将连接到提供程序模块，客户端模块的[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)回调函数分配并初始化的绑定上下文结构提供程序模块，然后调用附件[ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)函数将继续在附加过程。 在此情况下，客户端模块的*ClientAttachProvider*回调函数必须返回状态代码返回的**NmrClientAttachProvider**函数。

如果[ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)返回状态\_成功、 客户端模块和提供程序模块已成功附加到每个其他。 在此情况下，客户端模块的[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)回调函数必须保存 NMR 传入的绑定句柄*NmrBindingHandle*NMR 调用客户端模块的参数时参数*ClientAttachProvider*回调函数。 客户端模块*ClientAttachProvider*回调函数还必须将指针保存到提供程序绑定上下文，并在变量中的客户端模块传递给返回的提供程序调度表**NmrClientAttachProvider**函数，在*ProviderBindingContext*并*ProviderDispatch*参数。 客户端模块通常将此数据保存到提供程序模块附件其绑定上下文中。

如果[ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)不会返回状态\_成功，客户端模块[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)回调函数应清理并释放它分配了之前调用任何资源**NmrClientAttachProvider**。

如果客户端模块确定它不会附加到提供程序模块，则客户端模块[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)回调函数必须返回状态\_NOINTERFACE。

例如，假设"EXNPI"网络编程接口 (NPI) 标头文件 Exnpi.h 中定义了以下：

```C++
// EXNPI provider characteristics structure
typedef struct EXNPI_PROVIDER_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_PROVIDER_CHARACTERISTICS, *PEXNPI_PROVIDER_CHARACTERISTICS;

// EXNPI client dispatch table
typedef struct EXNPI_CLIENT_DISPATCH_ {
  .
  . // NPI-specific dispatch table of function pointers that
  . // point to a client module's NPI callback functions.
  .
} EXNPI_CLIENT_DISPATCH, *PEXNPI_CLIENT_DISPATCH;

// EXNPI provider dispatch table
typedef struct EXNPI_PROVIDER_DISPATCH_ {
  .
  . // NPI-specific dispatch table of function pointers that
  . // point to a provider module's NPI functions.
  .
} EXNPI_PROVIDER_DISPATCH, *PEXNPI_PROVIDER_DISPATCH;
```

下面的代码示例演示如何注册为 EXNPI NPI 的客户端的客户端模块可以将自身附加到已注册为 EXNPI NPI 的提供程序的提供程序模块：

```C++
// Context structure for the client
// module's binding to a provider module
typedef struct CLIENT_BINDING_CONTEXT_ {
  HANDLE NmrBindingHandle;
  PVOID ProviderBindingContext;
  PEXNPI_PROVIDER_DISPATCH ProviderDispatch;
  .
  . // Other client-specific members
  .
} CLIENT_BINDING_CONTEXT, *PCLIENT_BINDING_CONTEXT;

// Pool tag used for allocating the binding context
#define BINDING_CONTEXT_POOL_TAG 'tpcb'

// Structure for the client's dispatch table
const EXNPI_CLIENT_DISPATCH Dispatch = {
  .
  . // Function pointers to the client module's
  . // NPI callback functions
  .
};

// ClientAttachProvider callback function
NTSTATUS
  ClientAttachProvider(
    IN HANDLE NmrBindingHandle,
    IN PVOID ClientContext,
    IN PNPI_REGISTRATION_INSTANCE ProviderRegistrationInstance
    )
{
  PNPI_MODULEID ProviderModuleId;
  PEXNPI_PROVIDER_CHARACTERISTICS ProviderNpiSpecificCharacteristics;
  PCLIENT_BINDING_CONTEXT BindingContext;
  PVOID ProviderBindingContext;
  PEXNPI_PROVIDER_DISPATCH ProviderDispatch;
  NTSTATUS Status;

  // Get pointers to the provider module's identification structure
  // and the provider module's NPI-specific characteristics structure
  ProviderModuleId = ProviderRegistrationInstance->ModuleId;
  ProviderNpiSpecificCharacteristics =
    (PEXNPI_PROVIDER_CHARACTERISTICS)
      ProviderRegistrationInstance->NpiSpecificCharacteristics;

  //
  // Use the data in the structures pointed to by
  // ProviderRegistrationInstance, ProviderModuleId,
  // and ProviderNpiSpecificCharacteristics to determine
  // whether to attach to the provider module.
  //

  // If the client module determines that it will not attach
  // to the provider module
  if (...)
  {
    // Return status code indicating the modules did not
    // attach to each other
    return STATUS_NOINTERFACE;
  }

  // Allocate memory for the client module's
  // binding context structure
  BindingContext =
    (PCLIENT_BINDING_CONTEXT)
      ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(CLIENT_BINDING_CONTEXT),
        BINDING_CONTEXT_POOL_TAG
        );

  // Check result of allocation
  if (BindingContext == NULL)
  {
    // Return error status code
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Initialize the client binding context structure
  ...
 
  // Continue with the attachment to the provider module
  Status = NmrClientAttachProvider(
    NmrBindingHandle,
    BindingContext,
    &Dispatch,
    &ProviderBindingContext,
    &ProviderDispatch
    );

  // Check result of attachment
  if (Status == STATUS_SUCCESS)
  {
    // Save NmrBindingHandle, ProviderBindingContext,
    // and ProviderDispatch for future reference
    BindingContext->NmrBindingHandle =
      NmrBindingHandle;
    BindingContext->ProviderBindingContext =
      ProviderBindingContext;
    BindingContext->ProviderDispatch =
      ProviderDispatch;
  }

  // Attachment did not succeed
  else
  {
    // Free memory for client's binding context structure
    ExFreePoolWithTag(
      BindingContext,
      BINDING_CONTEXT_POOL_TAG
      );
  }

  // Return result of attachment
  return Status;
}
```

 

 





