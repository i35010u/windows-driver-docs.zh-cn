---
title: 断开套接字与目标的连接
description: 断开套接字与目标的连接
ms.assetid: 83755eb4-a24e-4fef-858d-d58318227dc0
keywords:
- Winsock 内核 WDK 连接网络、 断开连接
- WSK WDK 连接网络、 断开连接
- 已建立套接字连接 WDK Winsock 内核
- 连接 WDK Winsock 内核
- WDK Winsock 内核的断开连接
- 目标连接 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a43c1dffa9b5222398253992ff99d32d173ed7cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379570"
---
# <a name="disconnecting-a-socket-from-a-destination"></a>断开套接字与目标的连接


Winsock Kernel (WSK) 应用程序完成后发送和接收数据，通过建立套接字连接，它可以断开面向连接的套接字与连接到的远程传输地址的连接。 WSK 应用程序断开与远程传输地址通过调用连接套接字[ **WskDisconnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571129)函数。 WSK 应用程序可以执行*硬性断开*或*正常断开连接*套接字。 放弃性断开连接并正常断开连接之间的差异的详细信息，请参阅**WskDisconnect**。

下面的代码示例演示如何 WSK 应用程序可以正常断开面向连接的套接字与远程传输地址。

```C++
// Prototype for the disconnect IoCompletion routine
NTSTATUS
  DisconnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to disconnect a socket from a remote transport address
NTSTATUS
  DisconnectSocket(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;
 
  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

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
    DisconnectComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the disconnect operation on the socket
  Status =
    Dispatch->WskDisconnect(
      Socket,
      NULL,  // No final data to be transmitted
      0,     // No flags (graceful disconnect)
      Irp
      );

  // Return the status of the call to WskDisconnect()
  return Status;
}

// Disconnect IoCompletion routine
NTSTATUS
  DisconnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the disconnect operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the socket object from the context
    Socket = (PWSK_SOCKET)Context;

    // Perform the next operation on the socket
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

如果 WSK 程序执行的套接字正常断开连接，应用程序可以发送数据的最终缓冲区指向远程传输地址之前通过传递一个指向断开连接的套接字[ **WSK\_BUF**](https://msdn.microsoft.com/library/windows/hardware/ff571153)结构[ **WskDisconnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571129)函数。

如果 WSK 应用程序关闭而第一个从断开连接的套接字连接到的远程传输地址不面向连接的套接字，WSK 子系统将自动执行之前关闭套接字的套接字硬性断开连接。 有关关闭套接字的详细信息，请参阅[关闭套接字](closing-a-socket.md)。

 

 





