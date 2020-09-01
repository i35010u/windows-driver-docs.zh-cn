---
title: 针对套接字执行控制操作
description: 针对套接字执行控制操作
ms.assetid: 5d6ff02a-dc50-4818-9d0d-ba741fe7dfd8
keywords:
- Winsock 内核 WDK 网络，控制操作
- WSK WDK 网络，控制操作
- 控制操作 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06c12bb734ed317c28f8ceaac79721733d7b879a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212093"
---
# <a name="performing-control-operations-on-a-socket"></a>针对套接字执行控制操作


Winsock 内核 (WSK) 应用程序成功创建套接字后，它可以在套接字上执行控制操作。 可对套接字执行的控制操作包括设置和检索套接字选项和执行套接字 IOCTL 操作。

WSK 应用程序通过调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数在套接字上执行控制操作。 **WskControlSocket**函数由套接字提供程序调度结构的**WskControlSocket**成员指向。 套接字的提供程序调度结构由套接字对象结构的 **调度** 成员指向， ( [**WSK \_ 套**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket) 接字) 在创建套接字期间由 WSK 子系统返回。

下面的代码示例演示 WSK 应用程序如何在数据报套接字上设置 [**SO \_ EXCLUSIVEADDRUSE**](./so-exclusiveaddruse.md) 套接字选项。

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

有关每个受支持的套接字选项的详细信息，请参阅 [**WSK 套接字选项**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-socket-options)。

下面的代码示例演示 WSK 应用程序如何在数据报套接字上执行 [**SIO \_ WSK \_ SET \_ REMOTE \_ ADDRESS**](./sio-wsk-set-remote-address.md) socket IOCTL 操作。

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

有关每个受支持的套接字 IOCTL 操作的详细信息，请参阅 [WSK 套接字 Ioctl 操作](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-socket-ioctl-operations)。

 

