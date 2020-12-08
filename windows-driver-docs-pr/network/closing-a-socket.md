---
title: 关闭套接字
description: 关闭套接字
keywords:
- Winsock 内核 WDK 网络，插座关闭
- WSK WDK 网络，插座关闭
- 关闭套接字
- WskCloseSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3e5a2e5ae3afcee802fbf6f1519a76ad971bd28
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817643"
---
# <a name="closing-a-socket"></a>关闭套接字


如果 Winsock 内核 (WSK) 应用程序已使用套接字完成，则它应关闭套接字并释放所有关联的资源。 WSK 应用程序必须关闭所有打开的套接字，然后应用程序才能从 WSK 子系统分离其自身。 有关从 WSK 子系统分离 WSK 应用程序的详细信息，请参阅取消 [注册 Winsock 内核应用程序](unregistering-a-winsock-kernel-application.md)。

WSK 应用程序通过调用 [**WskCloseSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket) 函数关闭套接字。 在调用 **WskCloseSocket** 函数之前，WSK 应用程序必须确保任何套接字函数正在进行其他函数调用，包括任何应用程序的任何其他线程中的扩展函数。 但是，如果之前调用了尚未完成的套接字函数，WSK 应用程序可以调用 **WskCloseSocket** 。

WSK 应用程序使用的方法，以确保在调用 **WskCloseSocket** 函数之前，不会对任何套接字函数进行任何其他函数调用，这取决于应用程序的设计。 例如，如果 WSK 应用程序可能需要在一个线程中关闭套接字，而在一个或多个其他线程中有对该插槽的其他函数的调用，则应用程序通常会使用引用计数器来跟踪套接字上当前正在进行的函数调用的数量。 在这种情况下，WSK 应用程序会在调用某个套接字的函数之前，以原子方式测试并递增套接字的引用计数器，然后在函数返回时以原子方式递减套接字的引用计数器。 当引用计数器为零时，WSK 应用程序可以安全地调用 **WskCloseSocket** 函数来关闭套接字。

另一方面，如果 WSK 应用程序的设计保证在应用程序调用 **WskCloseSocket** 函数关闭套接字时，不会对任何其他线程中的特定套接字函数进行任何调用，则 WSK 应用程序不需要使用引用计数器来跟踪套接字上当前正在进行的函数调用的数量。 例如，如果 WSK 应用程序从单个线程为特定套接字执行其所有套接字操作，则应用程序可以安全地从该线程中调用 **WskCloseSocket** 函数，而无需引用计数器。

调用 **WskCloseSocket** 函数会导致 WSK 子系统取消并完成先前调用套接字的函数的所有挂起的 irp。 WSK 子系统还可确保正在进行的任何事件回调函数都在关闭操作完成之前返回到 WSK 子系统。

下面的代码示例演示 WSK 应用程序如何关闭套接字。

```C++
// Prototype for the socket close IoCompletion routine
NTSTATUS
  CloseSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to close a socket
NTSTATUS
  CloseSocket(
    PWSK_SOCKET Socket,
    PWSK_APP_SOCKET_CONTEXT SocketContext
    )
{
  PWSK_PROVIDER_BASIC_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_BASIC_DISPATCH)(Socket->Dispatch);

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
    CloseSocketComplete,
    SocketContext,
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the close operation on the socket
  Status =
    Dispatch->WskCloseSocket(
      Socket,
      Irp
      );

  // Return the status of the call to WskCloseSocket()
  return Status;
}

// Socket close IoCompletion routine
NTSTATUS
  CloseSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_APP_SOCKET_CONTEXT SocketContext;

  // Check the result of the socket close operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the socket context
    SocketContext =
      (PWSK_APP_SOCKET_CONTEXT)Context;

    // Perform any cleanup and/or deallocation of the socket context
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

在 WSK 应用程序调用 [**WskCloseSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)后，它不应对任何套接字函数进行进一步调用。

如果 WSK 应用程序关闭了一个面向连接的套接字，该套接字在两个方向上都未断开连接，则在关闭套接字之前，WSK 子系统会自动执行套接字的异常断开连接。 有关断开套接字连接的详细信息，请参阅 [断开套接字与目标的连接](disconnecting-a-socket-from-a-destination.md)。

 

