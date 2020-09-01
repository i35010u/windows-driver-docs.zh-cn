---
title: 将客户端模块附加到提供程序模块
description: 将客户端模块附加到提供程序模块
ms.assetid: 351c07f6-186a-4f47-95f8-c94084ff68fb
keywords:
- 附加网络模块
- 正在注册网络模块
- 网络模块注册 WDK，附加网络模块
- NMR WDK，附加网络模块
- 客户端模块 WDK 网络模块注册器，附加
- 网络模块 WDK 网络模块注册机构，附件
- NmrClientAttachProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9bc220f1b3a84a5caeee598bd41cc2612c12029
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215996"
---
# <a name="attaching-a-client-module-to-a-provider-module"></a>将客户端模块附加到提供程序模块


向网络模块注册机构注册 (NMR) 后，NMR 将调用客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数，一次针对注册为同一网络编程接口的提供者的每个提供程序模块， [ (NPI) ](network-programming-interface.md) 客户端模块已将其注册为客户端模块。

每当新的提供程序模块注册为客户端模块已注册为客户端的同一 NPI 的提供程序时，NMR 还会调用客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数。

当 NMR 调用特定提供程序模块的客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数时，它将在 *ProviderRegistrationInstance* 参数中传递一个指针，该指针指向与提供程序模块关联的 [**NPI \_ 注册 \_ 实例**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance) 结构。 客户端模块的*ClientAttachProvider*回调函数可以使用提供程序模块的**NPI \_ 注册 \_ 实例**结构中的数据，以及[**NPI \_ MODULEID**](/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))结构中的数据，以及由提供程序模块的**NPI \_ 注册 \_ 实例****结构的 MODULEID 和** **NpiSpecificCharacteristics**成员所指向的 NPI 特定提供程序特征结构，以确定它是否会附加到提供程序模块。

如果客户端模块确定它将附加到提供程序模块，则客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数将向提供程序模块分配附件的绑定上下文结构，然后调用 [**NmrClientAttachProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider) 函数以继续执行附件过程。 在这种情况下，客户端模块的 *ClientAttachProvider* 回调函数必须返回 **NmrClientAttachProvider** 函数返回的状态代码。

如果 [**NmrClientAttachProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider) 返回状态 " \_ 成功"，则客户端模块和提供程序模块已成功彼此连接。 在这种情况下，当 NMR 调用客户端模块的*ClientAttachProvider*回调函数时，客户端模块的[*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)回调函数必须保存 NMR 传入*NmrBindingHandle*参数的绑定句柄。 客户端模块的*ClientAttachProvider*回调函数还必须将指向提供程序绑定上下文和提供程序调度表的指针保存在客户端模块传递到*ProviderBindingContext*和*ProviderDispatch*参数中的**NmrClientAttachProvider**函数的变量中。 通常，客户端模块会将此数据保存到提供程序模块的附件的绑定上下文中。

如果 [**NmrClientAttachProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider) 未返回状态 \_ "成功"，则客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数应清除并释放它在调用 **NmrClientAttachProvider**之前分配的所有资源。

如果客户端模块确定它不会附加到提供程序模块，则客户端模块的 [*ClientAttachProvider*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数必须返回 STATUS \_ NOINTERFACE。

例如，假设 "EXNPI" 网络编程接口 (NPI) 在头文件 Exnpi 中定义以下内容：

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

下面的代码示例演示如何将注册为 EXNPI NPI 的客户端的客户端模块附加到注册为 EXNPI NPI 的提供程序的提供程序模块：

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

 

