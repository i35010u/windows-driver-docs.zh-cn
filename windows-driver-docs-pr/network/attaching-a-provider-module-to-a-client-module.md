---
title: 将提供程序模块附加到客户端模块
description: 将提供程序模块附加到客户端模块
keywords:
- 附加网络模块
- 正在注册网络模块
- 网络模块注册 WDK，附加网络模块
- NMR WDK，附加网络模块
- 提供商模块 WDK 网络模块注册器，附加
- 网络模块 WDK 网络模块注册机构，附件
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f83afe9fcd0e454bdf55e1712d1b4987f1a3dc28
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832635"
---
# <a name="attaching-a-provider-module-to-a-client-module"></a>将提供程序模块附加到客户端模块


客户端模块调用 [**NmrClientAttachProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider) 函数以将自身附加到提供程序模块。 有关客户端模块如何附加到提供程序模块的详细信息，请参阅将 [客户端模块附加到提供程序模块](attaching-a-client-module-to-a-provider-module.md)。

当客户端模块调用 [**NmrClientAttachProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)时，NMR 将调用提供程序模块的 [*ProviderAttachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn) 回调函数。 当 NMR 调用提供程序模块的 *ProviderAttachClient* 回调函数时，它将在 *ClientRegistrationInstance* 参数中传递一个指针，该指针指向与调用 **NmrClientAttachProvider** 的客户端模块关联的 [**NPI \_ 注册 \_ 实例**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)结构。 提供程序模块的 *ProviderAttachClient* 回调函数可以使用客户端模块的 **NPI \_ 注册 \_ 实例** 结构中的数据、 [**NPI \_ MODULEID**](/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))结构中的数据和 [网络编程接口 () NPI](network-programming-interface.md)客户端模块的 **MODULEID \_ 注册 \_ 实例** 结构的 **NpiSpecificCharacteristics** 和 **NPI** 成员指向的特定客户端特征结构，以确定它是否会附加到客户端模块。

如果提供程序模块确定它将附加到客户端模块，则提供程序模块的 [*ProviderAttachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn) 回调函数必须执行以下操作：

-   为客户端模块的附件分配和初始化绑定上下文结构。

-   保存传入 *NmrBindingHandle* 参数的绑定句柄。

-   保存传递给 *ClientBindingContext* 和 *ClientDispatch* 参数的指针，以便提供程序模块可以调用客户端模块的 NPI 回调函数。

-   设置 *ProviderBindingContext* 参数指向的变量，以指向提供程序模块的绑定上下文结构。

-   设置 *ProviderDispatch* 参数指向的变量，以指向包含 NPI 函数的提供程序模块的调度表的结构。

-   返回状态 \_ 成功。

提供程序模块通常会保存绑定句柄、指向客户端绑定上下文的指针，以及指向客户端模块的附件在其绑定上下文中的指针。

如果提供程序模块的 [*ProviderAttachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn) 回调函数返回状态 \_ "成功"，则客户端模块和提供程序模块已成功相互连接。

如果提供程序模块确定它不会附加到客户端模块，则提供程序模块的 [*ProviderAttachClient*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn) 回调函数必须返回 STATUS \_ NOINTERFACE。

例如，假设 "EXNPI" 网络编程接口 (NPI) 在头文件 Exnpi 中定义以下内容：

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

下面的代码示例演示如何将作为 EXNPI NPI 的提供程序注册的提供程序模块附加到注册为 EXNPI NPI 的客户端的客户端模块：

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

 

