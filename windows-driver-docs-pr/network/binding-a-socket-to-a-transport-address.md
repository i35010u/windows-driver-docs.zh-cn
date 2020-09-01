---
title: 将套接字绑定到传输地址
description: 将套接字绑定到传输地址
ms.assetid: b76bb601-536f-43de-b91c-932f4f08c274
keywords:
- Winsock 内核 WDK 网络，本地传输地址
- WSK WDK 网络，本地传输地址
- 绑定套接字 WDK Winsock 内核
- 本地传输地址绑定 WDK Winsock 内核
- 传输地址 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bd3f66c4046b5aa94cc28fccfb127869ac3295a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206487"
---
# <a name="binding-a-socket-to-a-transport-address"></a>将套接字绑定到传输地址


Winsock 内核 (WSK) 应用程序成功创建套接字后，它可以将该套接字绑定到本地传输地址。 侦听套接字必须绑定到本地传输地址，然后才能接受传入连接。 数据报套接字必须绑定到本地传输地址，然后才能发送或接收数据报。 面向连接的套接字必须绑定到本地传输地址，然后才能连接到远程传输地址。

**注意**   基本套接字不支持发送或接收网络数据。 因此，WSK 应用程序无法将基本套接字绑定到本地传输地址。

 

WSK 应用程序通过调用 [**WskBind**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_bind) 函数将套接字绑定到本地传输地址。 **WskBind**函数由套接字提供程序调度结构的**WskBind**成员指向。 套接字的提供程序调度结构由套接字对象结构的 **调度** 成员指向， ( [**WSK \_ 套**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket) 接字) 在创建套接字期间由 WSK 子系统返回。

套接字可绑定到本地通配符地址。 有关已绑定到本地通配符地址的套接字行为的详细信息，请参阅 **WskBind**。

下面的代码示例演示 WSK 应用程序如何可以将侦听套接字绑定到本地传输地址。

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

对于面向连接的套接字，WSK 应用程序可以调用 [**WskSocketConnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect) 函数在单个函数调用中创建、绑定和连接套接字。

 

