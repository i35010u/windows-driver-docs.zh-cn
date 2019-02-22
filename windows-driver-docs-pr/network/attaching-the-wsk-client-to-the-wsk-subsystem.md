---
title: 附加到 WSK 子系统 WSK 客户端
description: 附加到 WSK 子系统 WSK 客户端
ms.assetid: 752d204f-3022-48b0-9237-707b753a7ad3
keywords:
- 网络模块注册机构 WDK Winsock 内核
- NMR WDK Winsock 内核
- 正在卸载 WSK 客户端
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 725cb7d9e23d846f9567a2fa8bef45ed3939c713
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556127"
---
# <a name="attaching-the-wsk-client-to-the-wsk-subsystem"></a>附加到 WSK 子系统 WSK 客户端


应用程序已注册后 Winsock Kernel (WSK)[网络模块注册机构 (NMR)](network-module-registrar2.md) WSK NPI 的客户端，作为 NMR 立即调用应用程序的[ *ClientAttachProvider*](https://msdn.microsoft.com/library/windows/hardware/ff544903)如果 WSK 子系统加载和注册其自身的 NMR 回调函数。 如果未向 NMR 注册 WSK 子系统，NMR 不会调用应用程序的*ClientAttachProvider*直到 WSK 子系统向 NMR 注册回调函数。

WSK 应用程序应做出以下一系列调用完成的附件过程。

1.  当 NMR 调用 WSK 应用程序的*ClientAttachProvider*回调函数，它将传递一个指向[ **NPI\_注册\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff568815) WSK 子系统与关联的结构。 WSK 应用程序的*ClientAttachProvider*回调函数可以使用通过 NMR 传递给它的数据来确定它可以附加到 WSK 子系统。 通常情况下，WSK 应用程序只需中包含的版本信息[ **WSK\_提供程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff571172) 所指向的结构**NpiSpecificCharacteristics** WSK 子系统 NPI 成员\_注册\_实例结构。

2.  如果 WSK 应用程序确定它可以将附加到 WSK 子系统，WSK 应用程序的*ClientAttachProvider*回调函数分配并初始化到 WSK 子系统附件的绑定上下文结构. 然后，应用程序调用[ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)函数将继续在附加过程。

    如果**NmrClientAttachProvider**将返回状态\_成功后，WSK 应用程序已成功附加到 WSK 子系统。 在此情况下，WSK 应用程序的*ClientAttachProvider*回调函数必须保存 NMR 传入的绑定句柄*NmrBindingHandle* NMR 调用参数时参数应用程序的*ClientAttachProvider*回调函数。 WSK 应用程序的*ClientAttachProvider*回调函数还必须将指针保存到客户端对象 ( [ **WSK\_客户端**](https://msdn.microsoft.com/library/windows/hardware/ff571155)) 和提供程序调度表 ( [ **WSK\_提供程序\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff571175)) 的应用程序传递给的变量中返回**NmrClientAttachProvider**函数，在*ProviderBindingContext*并*ProviderDispatch*参数。 WSK 应用程序通常将此数据保存到 WSK 子系统附件其绑定上下文中。 WSK 子系统，WSK 应用程序的应用程序已成功附加后 WSK *ClientAttachProvider*回调函数必须返回状态\_成功。

3.  如果**NmrClientAttachProvider**将返回状态\_NOINTERFACE，WSK 应用程序可以使另一个尝试通过调用附加到 WSK 子系统**NmrClientAttachProvider**同样，函数并传递*ClientDispatch*到不同的指针[ **WSK\_客户端\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff571159)结构指定的应用程序支持 WSK NPI 的替代版本。

4.  如果调用**NmrClientAttachProvider**函数不返回状态\_成功和 WSK 应用程序不会进行任何进一步的尝试将附加到 WSK 子系统，WSK 应用程序的*ClientAttachProvider*回调函数应清理并释放它分配了名为之前的任何资源**NmrClientAttachProvider**。 在此情况下，WSK 应用程序的*ClientAttachProvider*回调函数必须返回到的最后一个调用返回的状态代码**NmrClientAttachProvider**函数。

5.  如果 WSK 应用程序确定它不能将附加到提供程序模块，该应用程序的*ClientAttachProvider*回调函数必须返回状态\_NOINTERFACE。

下面的代码示例演示如何 WSK 应用程序可以将自身附加到 WSK 子系统。

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

 

 





