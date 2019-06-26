---
title: 将套接字绑定到传输地址
description: 将套接字绑定到传输地址
ms.assetid: b76bb601-536f-43de-b91c-932f4f08c274
keywords:
- 网络、 Winsock 内核 WDK 本地传输地址
- WSK WDK 网络、 本地传输地址
- 绑定套接字 WDK Winsock 内核
- 本地传输地址绑定 WDK Winsock 内核
- 传输地址 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d8426226782a66bb545bac440823549745e952e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354636"
---
# <a name="binding-a-socket-to-a-transport-address"></a>将套接字绑定到传输地址


Winsock Kernel (WSK) 应用程序已成功创建套接字后，它可以将该套接字绑定到本地传输地址。 它可以接受传入连接之前，侦听套接字必须绑定到本地传输地址。 数据报套接字必须绑定到本地传输地址，它才能发送或接收数据报。 面向连接的套接字必须绑定到本地传输地址，才能连接到远程传输地址。

**请注意**  基本套接字不支持发送或接收网络数据。 因此，WSK 应用程序不能将一个基本的套接字绑定到本地传输地址。

 

WSK 应用程序的调用将套接字绑定到本地传输地址[ **WskBind** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_bind)函数。 **WskBind**函数所指向的**WskBind**套接字的提供程序调度结构的成员。 一个套接字提供程序调度结构所指向的**调度**套接字对象结构的成员 ( [ **WSK\_套接字**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_socket)) 返回在创建套接字期间 WSK 子系统。

一个套接字可绑定到本地的通配符地址。 已绑定到本地的通配符地址的套接字的行为的详细信息，请参阅**WskBind**。

下面的代码示例演示如何 WSK 应用程序可以将侦听套接字绑定到本地传输地址。

```C++
// Prototype for the bind IoCompletion routine
NTSTATUS
  BindComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to bind a listening socket to a local transport address
NTSTATUS
  BindListeningSocket(
    PWSK_SOCKET Socket,
    PSOCKADDR LocalAddress
    )
{
  PWSK_PROVIDER_LISTEN_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_LISTEN_DISPATCH)(Socket->Dispatch);

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
    BindComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the bind operation on the socket
  Status =
    Dispatch->WskBind(
      Socket,
      LocalAddress,
      0,  // No flags
      Irp
      );

  // Return the status of the call to WskBind()
  return Status;
}

// Bind IoCompletion routine
NTSTATUS
  BindComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the bind operation
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

对于面向连接的套接字，WSK 应用程序可以调用[ **WskSocketConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建、 绑定和连接中的单个函数调用的套接字。

 

 





