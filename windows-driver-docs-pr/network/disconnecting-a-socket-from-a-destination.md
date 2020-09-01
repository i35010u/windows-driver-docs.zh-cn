---
title: 断开套接字与目标的连接
description: 断开套接字与目标的连接
ms.assetid: 83755eb4-a24e-4fef-858d-d58318227dc0
keywords:
- Winsock 内核 WDK 网络，断开连接
- WSK WDK 网络，断开连接
- 建立的套接字连接 WDK Winsock 内核
- 连接 WDK Winsock 内核
- 断开 WDK Winsock 内核
- 目标连接 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5080da6f440fb26803bfd0e74459972aa1a7b2d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212517"
---
# <a name="disconnecting-a-socket-from-a-destination"></a>断开套接字与目标的连接


当 Winsock 内核 (WSK) 应用程序完成通过建立的套接字连接发送和接收数据时，它可以断开面向连接的套接字与连接到的远程传输地址的连接。 WSK 应用程序通过调用 [**WskDisconnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect) 函数将套接字与远程传输地址断开连接。 WSK 应用程序可以执行 *异常断开连接* 或插座的 *正常断开连接* 。 有关异常断开连接与正常断开连接之间的差异的详细信息，请参阅 **WskDisconnect**。

下面的代码示例演示 WSK 应用程序如何将面向连接的套接字与远程传输地址正确断开连接。

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

如果 WSK 应用程序执行套接字的正常断开连接，则在通过将指向 [**WSK \_ BUF**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_buf) 结构的指针传递到 [**WskDisconnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect) 函数之前，应用程序可以将数据的最终缓冲区发送到远程传输地址。

如果 WSK 应用程序关闭面向连接的套接字，而不先将套接字从其连接到的远程传输地址断开连接，则在关闭套接字之前，WSK 子系统会自动执行套接字的异常断开连接。 有关关闭套接字的详细信息，请参阅 [关闭套接字](closing-a-socket.md)。

 

