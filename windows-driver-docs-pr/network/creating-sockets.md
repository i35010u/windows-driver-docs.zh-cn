---
title: 创建套接字
description: 创建套接字
ms.assetid: 84cd0503-15bd-401f-836c-1fdc8425d073
keywords:
- Winsock 内核 WDK 网络，套接字创建
- WSK WDK 网络，套接字创建
- 侦听套接字 WDK Winsock 内核
- WskSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbd031054b16f257a1946d932fdee5716234f72b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210201"
---
# <a name="creating-sockets"></a>创建套接字


Winsock 内核 (WSK) 应用程序已成功连接到 WSK 子系统后，它可以创建可用于网络 i/o 操作的套接字。 WSK 应用程序通过调用 [**WskSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket) 函数来创建套接字。 **WskSocket**函数由 WSK 子系统在附件期间返回的[**WSK \_ 提供程序 \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)结构的**WskSocket**成员指向。

WSK 应用程序必须指定在创建新套接字时创建的 WSK 套接字的类别。 有关 WSK 套接字类别的详细信息，请参阅 [Winsock 内核套接字类别](winsock-kernel-socket-categories.md)。

WSK 应用程序还必须指定地址族、套接字类型和协议，无论何时创建新的套接字。 有关 WSK 支持的地址系列的详细信息，请参阅 [WSK 地址系列](/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))。

创建新的套接字时，如果应用程序将在套接字上启用任何事件回调函数，则 WSK 应用程序必须提供套接字上下文值和指向客户端调度表结构的指针。 有关在套接字上启用事件回调函数的详细信息，请参阅 [启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

如果套接字创建成功，则 IRP 的 **IoStatus** 字段包含一个指向套接字对象结构的指针，该结构 ( [**WSK \_ 套**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket) 接字的套) 接字。 有关将 Irp 用于 WSK 函数的详细信息，请参阅将 [irp 与 Winsock 内核函数结合使用](using-irps-with-winsock-kernel-functions.md)。

下面的代码示例演示 WSK 应用程序如何创建侦听套接字。

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

对于面向连接的套接字，WSK 应用程序可以调用 [**WskSocketConnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect) 函数在单个函数调用中创建、绑定和连接套接字。

 

