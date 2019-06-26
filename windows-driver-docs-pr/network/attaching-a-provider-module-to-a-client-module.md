---
title: 将提供程序模块附加到客户端模块
description: 将提供程序模块附加到客户端模块
ms.assetid: 5c68273e-d343-4d83-8703-957960934136
keywords:
- 附加网络模块
- 注册网络模块
- 网络模块注册机构 WDK，附加网络模块
- NMR WDK，附加网络模块
- 提供程序模块 WDK 网络模块注册机构，附加
- 网络模块 WDK 网络模块注册机构，附件
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b86d68fbdd57f01a859393c07d96efad1aa1f798
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384422"
---
# <a name="attaching-a-provider-module-to-a-client-module"></a>将提供程序模块附加到客户端模块


客户端模块会调用[ **NmrClientAttachProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientattachprovider)函数以将自身附加到提供程序模块。 有关如何将客户端模块附加到提供程序模块的详细信息，请参阅[将客户端模块附加到提供程序模块](attaching-a-client-module-to-a-provider-module.md)。

当客户端模块调用[ **NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientattachprovider)，NMR 调用提供程序模块[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数。 当 NMR 调用提供程序模块*ProviderAttachClient*回调函数，它将传递，在*ClientRegistrationInstance*参数，指向[ **NPI\_注册\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_registration_instance)结构，它是与名为的客户端模块关联**NmrClientAttachProvider**。 提供程序模块*ProviderAttachClient*回调函数可以使用客户端模块中的数据**NPI\_注册\_实例**结构中的数据[**NPI\_MODULEID** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))结构并[网络编程接口 (NPI)](network-programming-interface.md)-特定客户端特性结构指向**ModuleId**并**NpiSpecificCharacteristics**的客户端模块成员**NPI\_注册\_实例**结构，为确定是否将附加到客户端模块。

如果提供程序模块确定它会将连接到客户端模块，然后提供程序模块[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数必须执行以下操作：

-   分配并初始化绑定上下文结构到客户端模块的附件。

-   保存传入的绑定句柄*NmrBindingHandle*参数。

-   保存中传递的指针*ClientBindingContext*并*ClientDispatch*参数，以便提供程序模块能够进行对客户端模块 NPI 回调函数的调用。

-   设置指向的变量*ProviderBindingContext*参数指向的提供程序模块的绑定上下文结构。

-   设置指向的变量*ProviderDispatch*参数指向包含 NPI 函数提供程序模块调度表的结构。

-   返回状态\_成功。

提供程序模块通常将保存到客户端调度结构在客户端模块到附件其绑定上下文中的绑定句柄，指向客户端绑定上下文的指针和指针。

如果提供程序模块[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数将返回状态\_成功、 客户端模块和提供程序模块已成功附加到每个其他。

如果提供程序模块确定它不会附加到客户端模块，然后提供程序模块[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)回调函数必须返回状态\_NOINTERFACE。

例如，假设"EXNPI"网络编程接口 (NPI) 标头文件 Exnpi.h 中定义了以下：

```C++
// EXNPI client characteristics structure
typedef struct EXNPI_CLIENT_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_CLIENT_CHARACTERISTICS, *PEXNPI_CLIENT_CHARACTERISTICS;

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

下面的代码示例演示如何注册为 EXNPI NPI 的提供程序的提供程序模块可以将自身附加到已注册为 EXNPI NPI 的客户端的客户端模块：

```C++
// Context structure for the provider
// module's binding to a client module
typedef struct PROVIDER_BINDING_CONTEXT_ {
  HANDLE NmrBindingHandle;
  PVOID ClientBindingContext;
  PEXNPI_CLIENT_DISPATCH ClientDispatch;
  .
  . // Other provider-specific members
  .
} PROVIDER_BINDING_CONTEXT, *PPROVIDER_BINDING_CONTEXT;

// Pool tag used for allocating the binding context
#define BINDING_CONTEXT_POOL_TAG 'tpcb'

// Structure for the provider's dispatch table
const EXNPI_PROVIDER_DISPATCH Dispatch = {
  .
  . // Function pointers to the provider
  . // module's NPI functions
  .
};

// ProviderAttachClient callback function
NTSTATUS
  ProviderAttachClient(
    IN HANDLE NmrBindingHandle,
    IN PVOID ProviderContext,
    IN PNPI_REGISTRATION_INSTANCE ClientRegistrationInstance,
    IN PVOID ClientBindingContext,
    IN CONST VOID *ClientDispatch,
    OUT PVOID *ProviderBindingContext,
    OUT PVOID *ProviderDispatch
    )
{
  PNPI_MODULEID ClientModuleId;
  PEXNPI_CLIENT_CHARACTERISTICS ClientNpiSpecificCharacteristics;
  PPROVIDER_BINDING_CONTEXT BindingContext;
  PVOID ClientBindingContext;
  PEXNPI_CLIENT_DISPATCH ClientDispatch;

  // Check parameters
  if ((ProviderBindingContext == NULL) ||
      (ProviderDispatch == NULL))
  {
    // Return error status code
    return STATUS_INVALID_PARAMETER;
  }

  // Get pointers to the client module's identification structure
  // and the client module's NPI-specific characteristics structure
  ClientModuleId = ClientRegistrationInstance->ModuleId;
  ClientNpiSpecificCharacteristics =
    (PEXNPI_CLIENT_CHARACTERISTICS)
      ProviderRegistrationInstance->NpiSpecificCharacteristics;

  //
  // Use the data in the structures pointed to by
  // ClientRegistrationInstance, ClientModuleId,
  // and ClientNpiSpecificCharacteristics to determine
  // whether to attach to the client module.
  //

  // If the provider module determines that it will not attach
  // to the client module
  if (...)
  {
    // Return status code indicating the modules did not
    // attach to each other
    return STATUS_NOINTERFACE;
  }

  // Allocate memory for the provider module's
  // binding context structure
  BindingContext =
    (PPROVIDER_BINDING_CONTEXT)
      ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(PROVIDER_BINDING_CONTEXT),
        BINDING_CONTEXT_POOL_TAG
        );

  // Check result of allocation
  if (BindingContext == NULL)
  {
    // Return error status code
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Initialize the provider binding context structure
  ...

  // Save NmrBindingHandle, ClientBindingContext,
  // and ClientDispatch for future reference
  BindingContext->NmrBindingHandle =
    NmrBindingHandle;
  BindingContext->ClientBindingContext =
    ClientBindingContext;
  BindingContext->ClientDispatch =
    ClientDispatch;

  // Return a pointer to the provider binding context structure
  // in the ProviderBindingContext parameter
  *ProviderBindingContext = BindingContext;

  // Return a pointer to the provider dispatch structure
  // in the ProviderDispatch parameter
  *ProviderDispatch = &Dispatch;

  // Return success status
  return STATUS_SUCCESS;
}
```

 

 





