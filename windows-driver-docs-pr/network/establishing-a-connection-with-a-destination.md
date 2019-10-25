---
title: 与目标建立连接
description: 与目标建立连接
ms.assetid: 1258ee32-3914-4832-b98b-361dace0abaf
keywords:
- Winsock 内核 WDK 网络，远程传输地址
- WSK WDK 网络，远程传输地址
- 远程传输地址绑定 WDK Winsock 内核
- 传输地址 WDK Winsock 内核
- 建立的套接字连接 WDK Winsock 内核
- 连接 WDK Winsock 内核
- 目标连接 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89ec07b3abebc92bdf45914a42de50605c39fa39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834772"
---
# <a name="establishing-a-connection-with-a-destination"></a>与目标建立连接


Winsock 内核（WSK）应用程序已将面向连接的套接字绑定到本地传输地址后，它可以将套接字连接到远程传输地址，以便与远程系统建立连接。 WSK 应用程序必须先将面向连接的套接字连接到远程传输地址，然后才能在套接字上发送或接收数据。

WSK 应用程序通过调用[**WskConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_connect)函数将套接字连接到远程传输地址。 **WskConnect**函数由套接字提供程序调度结构的**WskConnect**成员指向。 套接字的提供程序调度结构由 WSK 子系统在创建套接字期间返回的套接字对象结构（ [**WSK\_套接字**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket)）的**调度**成员指向。

下面的代码示例演示 WSK 应用程序如何将面向连接的套接字连接到远程传输地址。

```C++
// Prototype for the connect IoCompletion routine
NTSTATUS
  ConnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to connect a socket to a remote transport address
NTSTATUS
  ConnectSocket(
    PWSK_SOCKET Socket,
    PSOCKADDR RemoteAddress
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
    ConnectComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the connect operation on the socket
  Status =
    Dispatch->WskConnect(
      Socket,
      RemoteAddress,
      0,  // No flags
      Irp
      );

  // Return the status of the call to WskConnect()
  return Status;
}

// Connect IoCompletion routine
NTSTATUS
  ConnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the connect operation
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

WSK 应用程序可以在单个函数调用中调用[**WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建、绑定和连接面向连接的套接字。

 

 





