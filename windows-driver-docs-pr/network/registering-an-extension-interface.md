---
title: 注册扩展接口
description: 注册扩展接口
ms.assetid: 33dc32da-9bc1-40b4-8737-ec132ec36708
keywords:
- Winsock 内核 WDK 网络，扩展接口
- WSK WDK 网络，扩展接口
- 扩展接口 WDK Winsock 内核
- 注册 Winsock 内核扩展接口
- SIO_WSK_REGISTER_EXTENSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 239551ec06e469d25ae0d3dcea43f1931ea35159
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842095"
---
# <a name="registering-an-extension-interface"></a>注册扩展接口


Winsock 内核（WSK）应用程序成功创建套接字后，它可以为 WSK 子系统支持的一个或多个[扩展接口](winsock-kernel-extension-interfaces.md)注册该套接字。 WSK 应用程序通过检查 WSK 子系统返回给应用程序的[**WSK\_提供程序\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)结构的**版本**成员，确定 WSK 子系统支持的扩展接口集。在附件时。

每个扩展接口都由与 WSK NPI 无关的 NPI 定义。 但请注意，扩展接口的 NPIs 不支持 NPI 特定的特征。

WSK 应用程序通过执行[**SIO\_WSK\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-register-extension)在套接字上注册\_扩展套接字 IOCTL 操作来注册扩展接口。 有关执行套接字 IOCTL 操作的详细信息，请参阅[在套接字上执行控制操作](performing-control-operations-on-a-socket.md)。

如果 WSK 应用程序尝试为 WSK 子系统不支持的扩展接口注册套接字，则 SIO\_WSK\_REGISTER\_扩展套接字 IOCTL 操作将返回\_\_不受支持的状态。

例如，假设扩展接口定义为，如下面的代码示例中所示。

```C++
const NPIID EXAMPLE_EXTIF_NPIID = {...};

typedef struct _EXAMPLE_EXTIF_PROVIDER_DISPATCH {
  .
  . // Function pointers for the functions that are
  . // defined by the extension interface.
  .
} EXAMPLE_EXTIF_PROVIDER_DISPATCH, *PEXAMPLE_EXTIF_PROVIDER_DISPATCH;

typedef struct _EXAMPLE_EXTIF_CLIENT_DISPATCH {
  .
  . // Function pointers for the callback functions
  . // that are defined by the extension interface.
  .
} EXAMPLE_EXTIF_CLIENT_DISPATCH, *PEXAMPLE_EXTIF_CLIENT_DISPATCH;
```

下面演示了 WSK 应用程序如何为面向连接的套接字注册此扩展接口。

```C++
// Client dispatch structure for the extension interface
const EXAMPLE_EXTIF_CLIENT_DISPATCH ExtIfClientDispatch = {
  .
  . // The WSK application's callback functions
  . // for the extension interface
  .
};

// Context structure type for the example extension interface
typedef struct _EXAMPLE_EXTIF_CLIENT_CONTEXT
{
  const EXAMPLE_EXTIF_PROVIDER_DISPATCH *ExtIfProviderDispatch;
  PVOID ExtIfProviderContext;
    .
    .  // Other application-specific members
    .
} EXAMPLE_EXTIF_CLIENT_CONTEXT, *PEXAMPLE_EXTIF_CLIENT_CONTEXT;

// Function to register the example extension interface
NTSTATUS
  RegisterExampleExtIf(
    PWSK_SOCKET Socket,
    PEXAMPLE_EXTIF_CLIENT_CONTEXT ExtIfClientContext
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  WSK_EXTENSION_CONTROL_IN ExtensionControlIn;
  WSK_EXTENSION_CONTROL_OUT ExtensionControlOut;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

  // Fill in the WSK_EXTENSION_CONTROL_IN structure
  ExtensionControlIn.NpiId = &EXAMPLE_EXTIF_NPIID;
  ExtensionControlIn.ClientContext = ExtIfClientContext;
  ExtensionControlIn.ClientDispatch = &ExtIfClientDispatch;

  // Initiate the IOCTL operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskIoctl,
      SIO_WSK_REGISTER_EXTENSION,
      0,
      sizeof(WSK_EXTENSION_CONTROL_IN),
      &ExtensionControlIn,
      sizeof(WSK_EXTENSION_CONTROL_OUT),
      &ExtensionControlOut,
      NULL,
      NULL  // No IRP used for this IOCTL operation
      );

  // Check result
  if (Status == STATUS_SUCCESS)
  {
    // Save provider dispatch table and provider context
    ExtIfClientContext->ExtIfProviderDispatch =
      (const EXAMPLE_EXTIF_PROVIDER_DISPATCH *)
        ExtensionControlOut.ProviderDispatch;
    ExtIfClientContext->ExtIfProviderContext =
      ExtensionControlOut.ProviderContext;
  }

  // Return the status of the call to WskControlSocket()
  return Status;
}
```

WSK 应用程序在套接字基础上注册扩展接口。

 

 





