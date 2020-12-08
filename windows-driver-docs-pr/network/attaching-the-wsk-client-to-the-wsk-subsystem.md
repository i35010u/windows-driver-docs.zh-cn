---
title: 将 WSK 客户端附加到 WSK 子系统
description: 将 WSK 客户端附加到 WSK 子系统
keywords:
- 网络模块注册器 WDK Winsock 内核
- NMR WDK Winsock 内核
- 卸载 WSK 客户端
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29fc504ce5e2f2e6f1b208fc7f56b3af719f592d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813033"
---
# <a name="attaching-the-wsk-client-to-the-wsk-subsystem"></a>将 WSK 客户端附加到 WSK 子系统


Winsock 内核 (WSK) 应用程序已注册到 [网络模块注册器 (NMR)](network-module-registrar2.md) 作为 WSK NPI 的客户端时，如果已加载 NMR 子系统并已将其自身注册到 ClientAttachProvider，则 WSK 会立即调用应用程序的 [*NMR*](/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn) 回调函数。 如果未向 NMR 注册 WSK 子系统，则 NMR 将在 WSK 子系统注册到 NMR 之前，不会调用应用程序的 *ClientAttachProvider* 回调函数。

WSK 应用程序应执行以下一系列调用来完成附件过程。

1.  当 NMR 调用 WSK 应用程序的 *ClientAttachProvider* 回调函数时，它将传递指向与 WSK 子系统关联的 [**NPI \_ 注册 \_ 实例**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance) 结构的指针。 WSK 应用程序的 *ClientAttachProvider* 回调函数可以通过 NMR 使用传递给它的数据来确定它是否可以附加到 WSK 子系统。 通常，WSK 应用程序仅需要 [**WSK \_ 提供程序 \_ 特征**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_characteristics) 结构中包含的版本信息，该结构由 WSK 子系统的 NPI 注册实例结构的 **NpiSpecificCharacteristics** 成员 \_ 指向 \_ 。

2.  如果 WSK 应用程序确定它可以附加到 WSK 子系统，则 WSK 应用程序的 *ClientAttachProvider* 回调函数将该附件的绑定上下文结构分配给 WSK 子系统并对其进行初始化。 然后，应用程序会调用 [**NmrClientAttachProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider) 函数来继续执行附件操作。

    如果 **NmrClientAttachProvider** 返回状态 \_ SUCCESS，则 WSK 应用程序已成功连接到 WSK 子系统。 在这种情况下，当 NMR 调用应用程序的 *ClientAttachProvider* 回调函数时，WSK 应用程序的 *ClientAttachProvider* 回调函数必须保存 NMR 传入 *NmrBindingHandle* 参数的绑定句柄。 WSK 应用程序的 *ClientAttachProvider* 回调函数还必须将指向客户端对象 ( 的指针保存在 [**WSK \_ 客户端**](./wsk-client.md)) 和提供程序调度表中， ( [**WSK 提供程序) \_ \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)表在应用程序 *传递到 NmrClientAttachProvider 和* *ProviderBindingContext* 参数的 **ProviderDispatch** 函数的变量中返回。 WSK 应用程序通常会在其绑定上下文中将此数据保存到 WSK 子系统的附件。 WSK 应用程序成功附加到 WSK 子系统后，WSK 应用程序的 *ClientAttachProvider* 回调函数必须返回状态 " \_ 成功"。

3.  如果 **NmrClientAttachProvider** 返回 STATUS \_ NOINTERFACE，则 WSK 应用程序可以通过再次调用 **NmrClientAttachProvider** 函数再次尝试附加到 WSK 子系统，并将 *ClientDispatch* 指针传递到不同的 [**WSK \_ 客户端 \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch) 结构，后者指定了应用程序支持的另一版 WSK NPI。

4.  如果对 **NmrClientAttachProvider** 函数的调用未返回状态 \_ SUCCESS，并且 WSK 应用程序没有进一步尝试附加到 WSK 子系统，则 WSK 应用程序的 *ClientAttachProvider* 回调函数应清除并释放它在调用 **NmrClientAttachProvider** 之前分配的所有资源。 在这种情况下，WSK 应用程序的 *ClientAttachProvider* 回调函数必须返回对 **NmrClientAttachProvider** 函数的最后一次调用返回的状态代码。

5.  如果 WSK 应用程序确定它无法附加到提供程序模块，则该应用程序的 *ClientAttachProvider* 回调函数必须返回 STATUS \_ NOINTERFACE。

下面的代码示例演示 WSK 应用程序如何将自身附加到 WSK 子系统。

```C++
// Context structure type for the WSK application's
// binding to the WSK subsystem
typedef struct WSK_APP_BINDING_CONTEXT_ {
  HANDLE NmrBindingHandle;
  PWSK_CLIENT WskClient;
  PWSK_PROVIDER_DISPATCH WskProviderDispatch;
  .
  . // Other application-specific members
  .
} WSK_APP_BINDING_CONTEXT, *PWSK_APP_BINDING_CONTEXT;

// Pool tag used for allocating the binding context
#define BINDING_CONTEXT_POOL_TAG 'tpcb'

// The WSK application uses version 1.0 of WSK
#define WSK_APP_WSK_VERSION MAKE_WSK_VERSION(1,0)

// Structure for the WSK application's dispatch table
const WSK_CLIENT_DISPATCH WskAppDispatch = {
  WSK_APP_WSK_VERSION,
  0,
  NULL  // No WskClientEvent callback
};

// ClientAttachProvider NMR API callback function
NTSTATUS
  ClientAttachProvider(
    IN HANDLE NmrBindingHandle,
    IN PVOID ClientContext,
    IN PNPI_REGISTRATION_INSTANCE ProviderRegistrationInstance
    )
{
  PNPI_MODULEID WskProviderModuleId;
  PWSK_PROVIDER_CHARACTERISTICS WskProviderCharacteristics;
  PWSK_APP_BINDING_CONTEXT BindingContext;
  PWSK_CLIENT WskClient;
  PWSK_PROVIDER_DISPATCH WskProviderDispatch;
  NTSTATUS Status;

  // Get pointers to the WSK subsystem's identification and
  // characteristics structures
  WskProviderModuleId = ProviderRegistrationInstance->ModuleId;
  WskProviderCharacteristics =
    (PWSK_PROVIDER_CHARACTERISTICS)
      ProviderRegistrationInstance->NpiSpecificCharacteristics;

  //
  // The WSK application can use the data in the structures pointed
  // to by ProviderRegistrationInstance, WskProviderModuleId, and
  // WskProviderCharacteristics to determine if the WSK application
  // can attach to the WSK subsystem.
  //
  // In this example, the WSK application does not perform any
  // checks to determine if it can attach to the WSK subsystem.
  //

  // Allocate memory for the WSK application's binding
  // context structure
  BindingContext =
    (PWSK_APP_BINDING_CONTEXT)
      ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(WSK_APP_BINDING_CONTEXT),
        BINDING_CONTEXT_POOL_TAG
        );

  // Check result of allocation
  if (BindingContext == NULL)
  {
    // Return error status code
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Initialize the binding context structure
  ...
 
  // Continue with the attachment to the WSK subsystem
  Status = NmrClientAttachProvider(
    NmrBindingHandle,
    BindingContext,
    &WskAppDispatch,
    &WskClient,
    &WskProviderDispatch
    );

  // Check result of attachment
  if (Status == STATUS_SUCCESS)
  {
    // Save NmrBindingHandle, WskClient, and
    // WskProviderDispatch for future reference
    BindingContext->NmrBindingHandle = NmrBindingHandle;
    BindingContext->WskClient = WskClient;
    BindingContext->WskProviderDispatch = WskProviderDispatch;
  }

  // Attachment did not succeed
  else
  {
    // Free memory for application's binding context structure
    ExFreePoolWithTag(
      BindingContext,
      BINDING_CONTEXT_POOL_TAG
      );
  }

  // Return result of attachment
  return Status;
}
```

 

