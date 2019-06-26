---
title: 创建套接字
description: 创建套接字
ms.assetid: 84cd0503-15bd-401f-836c-1fdc8425d073
keywords:
- 网络、 Winsock 内核 WDK 创建套接字
- WSK WDK 网络、 创建套接字
- 侦听套接字 WDK Winsock 内核
- WskSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d204cc87cd897a1158aeb2b458f79319e53221b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374886"
---
# <a name="creating-sockets"></a>创建套接字


Winsock Kernel (WSK) 应用程序已成功附加到 WSK 子系统之后，它可以创建可用于网络 I/O 操作的套接字。 WSK 应用程序通过调用创建套接字[ **WskSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)函数。 **WskSocket**函数所指向的**WskSocket**的成员[ **WSK\_提供程序\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch)WSK 子系统在附件过程返回的结构。

WSK 应用程序必须指定 WSK 套接字的类别创建时它会创建一个新的套接字。 有关 WSK 套接字类别的详细信息，请参阅[Winsock 内核套接字类别](winsock-kernel-socket-categories.md)。

WSK 应用程序还必须指定地址族、 套接字类型和协议，每当创建新的套接字时。 有关支持的 WSK 的地址系列的详细信息，请参阅[WSK 地址系列](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))。

在创建新的套接字，WSK 应用程序必须提供的套接字上下文值和指向客户端调度表结构的指针，如果应用程序将会启用套接字上的任何事件回调函数。 有关启用套接字上的事件回调函数的详细信息，请参阅[启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

如果成功，创建套接字**IoStatus.Information** IRP 的字段包含指向套接字对象结构的指针 ( [ **WSK\_套接字**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_socket))新的套接字。 有关 Irp 用于 WSK 函数的详细信息，请参阅[Winsock 内核函数使用 Irp](using-irps-with-winsock-kernel-functions.md)。

下面的代码示例演示如何 WSK 应用程序可以创建侦听套接字。

```C++
// Context structure for each socket
typedef struct _WSK_APP_SOCKET_CONTEXT {
  PWSK_SOCKET Socket;
  .
  .  // Other application-specific members
  .
} WSK_APP_SOCKET_CONTEXT, *PWSK_APP_SOCKET_CONTEXT;

// Prototype for the socket creation IoCompletion routine
NTSTATUS
  CreateListeningSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to create a new listening socket
NTSTATUS
  CreateListeningSocket(
    PWSK_PROVIDER_NPI WskProviderNpi,
    PWSK_APP_SOCKET_CONTEXT SocketContext,
    PWSK_CLIENT_LISTEN_DISPATCH Dispatch,
    )
{
  PIRP Irp;
  NTSTATUS Status;

  // Allocate an IRP
  Irp =
    IoAllocateIrp(
      1,
      FALSE
      );

  // Check result
  if (!Irp)
  {
    // Return error
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Set the completion routine for the IRP
  IoSetCompletionRoutine(
    Irp,
    CreateListeningSocketComplete,
    SocketContext,
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the creation of the socket
  Status =
    WskProviderNpi->Dispatch->
        WskSocket(
          WskProviderNpi->Client,
          AF_INET,
          SOCK_STREAM,
          IPPROTO_TCP,
          WSK_FLAG_LISTEN_SOCKET,
          SocketContext,
          Dispatch,
          NULL,
          NULL,
          NULL,
          Irp
          );

  // Return the status of the call to WskSocket()
  return Status;
}

// Socket creation IoCompletion routine
NTSTATUS
  CreateListeningSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_APP_SOCKET_CONTEXT SocketContext;

  // Check the result of the socket creation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the socket context
    SocketContext =
      (PWSK_APP_SOCKET_CONTEXT)Context;

    // Save the socket object for the new socket
    SocketContext->Socket =
      (PWSK_SOCKET)(Irp->IoStatus.Information);

    // Set any socket options for the new socket
    ...

    // Enable any event callback functions on the new socket
    ...

    // Perform any other initializations
    ...
  }

  // Error status
  else
  {
    // Handle error
    ...
  }

  // Free the IRP
  IoFreeIrp(Irp);

  // Always return STATUS_MORE_PROCESSING_REQUIRED to
  // terminate the completion processing of the IRP.
  return STATUS_MORE_PROCESSING_REQUIRED;
}
```

对于面向连接的套接字，WSK 应用程序可以调用[ **WskSocketConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建、 绑定和连接中的单个函数调用的套接字。

 

 





