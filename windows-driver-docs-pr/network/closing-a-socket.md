---
title: 关闭套接字
description: 关闭套接字
ms.assetid: 3fa2d5c3-7b52-4bbe-b99d-ef3be19c7c7e
keywords:
- Winsock 内核 WDK 网络套接字关闭
- WSK WDK 网络，套接字关闭
- 关闭套接字
- WskCloseSocket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fe8478b6c685c125bab4f7b11e67906cb268c42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356914"
---
# <a name="closing-a-socket"></a>关闭套接字


完成后使用套接字的 Winsock Kernel (WSK) 应用程序，它应关闭套接字并释放任何关联的资源。 应用程序可以从 WSK 子系统中分离本身之前，WSK 应用程序必须关闭所有打开的套接字。 分离 WSK 子系统提供 WSK 的应用程序的详细信息，请参阅[Winsock 内核应用程序中注销](unregistering-a-winsock-kernel-application.md)。

WSK 应用程序通过调用关闭套接字[ **WskCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571124)函数。 然后再调用**WskCloseSocket**函数，WSK 应用程序必须确保没有任何其他函数调用到套接字的函数，在任何应用程序中包括任何扩展函数的任何正在进行中的其它线程数。 但是，WSK 应用程序可以调用**WskCloseSocket**是否存在挂起的 Irp 从以前调用尚未完成的套接字的函数。

调用之前 WSK 应用程序使用以确保不不存在任何其他函数的方法调用中的任何套接字的函数的进度**WskCloseSocket**函数所依赖的应用程序的设计。 例如，如果 WSK 应用程序可能需要在向该套接字进行可能存在的调用中时关闭一个线程中的套接字中一个或多个其他线程，则该应用程序的其他函数通常将引用计数器用于跟踪的函数当前正在进行中的套接字上的调用。 在此情况下，WSK 应用程序以原子方式测试并递增套接字的引用计数器之前它将调用一个套接字的函数，然后以原子方式递减套接字的引用计数器时该函数将返回。 WSK 应用程序时的引用计数器为零，可以安全地调用**WskCloseSocket**函数来关闭套接字。

另一方面，如果 WSK 应用程序的设计可保证，不会的任何调用在其他线程中的特定套接字的函数的正在进行中时在应用程序调用**WskCloseSocket**函数以关闭套接字，则 WSK 应用程序不需要使用引用计数器来跟踪当前正在对套接字的函数调用的数目。 例如，如果 WSK 应用程序在单个线程中执行其特定的套接字的套接字操作的所有操作，然后应用程序可以安全地调用**WskCloseSocket**而无需该线程中从函数引用计数器。

调用**WskCloseSocket**函数会导致要取消和完成从以前对套接字的函数调用的所有挂起 Irp 的 WSK 子系统。 WSK 子系统还可确保在进行任何事件回调函数，具有回 WSK 子系统中返回控件之前完成关闭操作。

下面的代码示例演示如何 WSK 应用程序可以关闭套接字。

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

应用程序已调用后 WSK [ **WskCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571124)，它不应造成会对任何套接字的函数的任何进一步调用。

如果 WSK 应用程序关闭已不之前断开连接两个方向的面向连接的套接字，WSK 子系统将自动关闭套接字之前执行套接字硬性断开的连接。 正在断开连接的套接字的详细信息，请参阅[断开与目标的连接套接字](disconnecting-a-socket-from-a-destination.md)。

 

 





