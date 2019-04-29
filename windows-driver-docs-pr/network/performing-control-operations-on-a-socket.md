---
title: 针对套接字执行控制操作
description: 针对套接字执行控制操作
ms.assetid: 5d6ff02a-dc50-4818-9d0d-ba741fe7dfd8
keywords:
- 网络、 Winsock 内核 WDK 控制操作
- WSK WDK 网络、 控制操作
- 控制操作 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58433daf71a339c3bca4176d65a3c3a5d67371ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358822"
---
# <a name="performing-control-operations-on-a-socket"></a>针对套接字执行控制操作


Winsock Kernel (WSK) 应用程序已成功创建套接字后，它可以执行的套接字上的控制操作。 可以在套接字执行管理操作包括设置和检索套接字选项和执行套接字 IOCTL 操作。

WSK 应用程序通过调用执行控制操作，针对套接字[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)函数。 **WskControlSocket**函数所指向的**WskControlSocket**套接字的提供程序调度结构的成员。 一个套接字提供程序调度结构所指向的**调度**套接字对象结构的成员 ( [ **WSK\_套接字**](https://msdn.microsoft.com/library/windows/hardware/ff571182)) 返回在创建套接字期间 WSK 子系统。

下面的代码示例演示如何设置 WSK 应用程序[**因此\_EXCLUSIVEADDRUSE** ](https://msdn.microsoft.com/library/windows/hardware/ff570830)套接字上的数据报套接字选项。

```C++
// Prototype for the control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to set the SO_EXCLUSIVEADDRUSE socket option
// on a datagram socket
NTSTATUS
  SetExclusiveAddrUse(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_DATAGRAM_DISPATCH Dispatch;
  PIRP Irp;
  ULONG SocketOptionState;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_DATAGRAM_DISPATCH)(Socket->Dispatch);

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
    ControlSocketComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Set the socket option state to 1 to set the socket option
  SocketOptionState = 1;

  // Initiate the control operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskSetOption,
      SO_EXCLUSIVEADDRUSE,
      SOL_SOCKET,
      sizeof(ULONG),
      &SocketOptionState,
      0,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}

// Control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the control operation
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

有关每个受支持的套接字选项的详细信息，请参阅[ **WSK 套接字选项**](https://msdn.microsoft.com/library/windows/hardware/ff571186)。

下面的代码示例演示如何执行 WSK 应用程序可以[ **SIO\_WSK\_设置\_远程\_地址**](https://msdn.microsoft.com/library/windows/hardware/ff570820)上建立套接字 IOCTL 操作数据报套接字。

```C++
// Prototype for the control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to perform the SIO_WSK_SET_REMOTE_ADDRESS socket
// IOCTL operation on a datagram socket
NTSTATUS
  SetRemoteAddress(
    PWSK_SOCKET Socket,
    PSOCKADDR RemoteAddress
    )
{
  PWSK_PROVIDER_DATAGRAM_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_DATAGRAM_DISPATCH)(Socket->Dispatch);

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
    ControlSocketComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the IOCTL operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskIoctl,
 SIO_WSK_SET_REMOTE_ADDRESS,
      0,
      sizeof(SOCKADDR_IN),  // AF_INET
      RemoteAddress,
      0,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}

// Control socket IoCompletion routine
NTSTATUS
  ControlSocketComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;

  // Check the result of the control operation
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

有关每个受支持的套接字 IOCTL 操作的详细信息，请参阅[WSK 套接字 IOCTL 操作](https://msdn.microsoft.com/library/windows/hardware/ff571183)。

 

 





