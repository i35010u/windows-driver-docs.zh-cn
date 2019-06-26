---
title: 注册扩展接口
description: 注册扩展接口
ms.assetid: 33dc32da-9bc1-40b4-8737-ec132ec36708
keywords:
- 网络、 Winsock 内核 WDK 扩展插件接口
- WSK WDK 网络、 扩展插件接口
- 扩展接口 WDK Winsock 内核
- 注册 Winsock 内核扩展插件接口
- SIO_WSK_REGISTER_EXTENSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1adad4b82d8a0525014309b2db135c07856d005
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374797"
---
# <a name="registering-an-extension-interface"></a>注册扩展接口


Winsock Kernel (WSK) 应用程序已成功创建套接字后，它可以为一个或多个注册的套接字[扩展插件接口](winsock-kernel-extension-interfaces.md)受 WSK 子系统。 WSK 应用程序确定 WSK 子系统支持的扩展插件接口的一组，应检查**版本**的成员[ **WSK\_提供程序\_调度** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch) WSK 子系统返回到应用程序在附件的结构。

由独立于 WSK NPI NPI 定义每个扩展接口。 但是，请注意，扩展插件接口 NPIs 不支持特定于 NPI 的特征。

WSK 应用程序注册的扩展接口通过执行[ **SIO\_WSK\_注册\_扩展**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-register-extension)套接字 IOCTL 套接字上的操作。 有关正在执行的套接字 IOCTL 操作的详细信息，请参阅[套接字上执行管理操作](performing-control-operations-on-a-socket.md)。

如果 WSK 应用程序将尝试注册 WSK 子系统，SIO 不支持的扩展接口的套接字\_WSK\_注册\_扩展套接字 IOCTL 操作将返回状态\_不\_受支持。

例如，假设，如以下代码示例所示定义扩展插件接口。

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

下面显示了如何为面向连接的套接字此扩展插件接口注册 WSK 应用程序。

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

WSK 应用程序注册为基于套接字的套接字的扩展插件接口。

 

 





