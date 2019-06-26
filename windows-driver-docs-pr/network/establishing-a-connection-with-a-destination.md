---
title: 与目标建立连接
description: 与目标建立连接
ms.assetid: 1258ee32-3914-4832-b98b-361dace0abaf
keywords:
- 网络、 Winsock 内核 WDK 远程传输地址
- WSK WDK 网络、 远程传输地址
- 远程传输地址绑定 WDK Winsock 内核
- 传输地址 WDK Winsock 内核
- 已建立套接字连接 WDK Winsock 内核
- 连接 WDK Winsock 内核
- 目标连接 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1312e98992ba3fd4b2e4c544eff51c06e0b7d553
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384558"
---
# <a name="establishing-a-connection-with-a-destination"></a>与目标建立连接


Winsock Kernel (WSK) 应用程序已绑定到本地传输地址的面向连接的套接字后，它可以连接套接字到远程传输地址来建立与远程系统的连接。 WSK 应用程序必须连接到远程传输地址的面向连接的套接字，然后它可以发送或通过套接字接收数据。

WSK 应用程序连接到远程传输地址通过调用的套接字[ **WskConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_connect)函数。 **WskConnect**函数所指向的**WskConnect**套接字的提供程序调度结构的成员。 一个套接字提供程序调度结构所指向的**调度**套接字对象结构的成员 ( [ **WSK\_套接字**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_socket)) 返回在创建套接字期间 WSK 子系统。

下面的代码示例显示了 WSK 应用程序如何可以面向连接的套接字连接到远程传输地址。

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

WSK 应用程序可以调用[ **WskSocketConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建、 绑定和连接中的单个函数调用的面向连接的套接字。

 

 





