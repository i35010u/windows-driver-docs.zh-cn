---
title: 侦听和接受传入连接
description: 侦听和接受传入连接
ms.assetid: 3ec7d6d0-8b8c-4d98-9e2a-e42b52dcd544
keywords:
- Winsock 内核 WDK 网络，传入连接
- WSK WDK 网络，传入连接
- 传入连接 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 条件接受 WDK Winsock 内核
- 侦听操作 WDK Winsock 内核
- SO_CONDITIONAL_ACCEPT
- 接受连接 WDK Winsock 内核
- WskAccept
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd1b3d6d19f45459402e35b24cf507a6fc4d5665
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844146"
---
# <a name="listening-for-and-accepting-incoming-connections"></a>侦听和接受传入连接


Winsock 内核（WSK）应用程序将侦听套接字绑定到本地传输地址后，套接字开始侦听来自远程传输地址的传入连接。 WSK 应用程序可以通过调用[**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)函数在侦听套接字上接受传入连接。 应用程序传递给**WskAccept**函数的 IRP 会排入队列，直到传入连接到达。

下面的代码示例演示 WSK 应用程序如何通过调用**WskAccept**函数来接受传入连接。

```C++
// Prototype for the accept IoCompletion routine
NTSTATUS
  AcceptComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to accept an incoming connection
NTSTATUS
  AcceptConnection(
    PWSK_SOCKET Socket,
    PVOID AcceptSocketContext,
    PWSK_CLIENT_CONNECTION_DISPATCH AcceptSocketDispatch
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
    AcceptComplete,
    AcceptSocketContext,
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the accept operation on the socket
  Status =
    Dispatch->WskAccept(
      Socket,
      0,  // No flags
      AcceptSocketContext,
      AcceptSocketDispatch,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskAccept()
  return Status;
}

// The accept IoCompletion routine
NTSTATUS
  AcceptComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_SOCKET Socket;
  PVOID AcceptSocketContext;

  // Check the result of the accept operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the accepted socket object from the IRP
    Socket = (PWSK_SOCKET)(Irp->IoStatus.Information);

    // Get the accepted socket's context
    AcceptSocketContext = Context;

    // Perform the next operation on the accepted socket
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

作为调用[**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)函数以接受侦听套接字上的传入连接的替代方法，WSK 应用程序可以在套接字上启用[*WskAcceptEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)事件回调函数。 如果 WSK 应用程序在侦听套接字上启用*WskAcceptEvent*事件回调函数，则在套接字上接受新的传入连接时，WSK 子系统将调用套接字的*WskAcceptEvent*事件回调函数。 有关启用侦听套接字的*WskAcceptEvent*事件回调函数的详细信息，请参阅[启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

下面的代码示例演示 WSK 应用程序如何通过调用侦听套接字的*WskAcceptEvent*事件回调函数的 WSK 子系统接受传入连接。

```cpp
// Dispatch table of event callback functions for accepted sockets
const WSK_CLIENT_CONNECTION_DISPATCH ConnectionDispatch =
{
  .
  . // Function pointers for the event callback functions
  .
};

// Pool tag used for allocating the socket context
#define SOCKET_CONTEXT_POOL_TAG 'tpcs'

// A listening socket's WskAcceptEvent event callback function
NTSTATUS WSKAPI
  WskAcceptEvent(
    PVOID SocketContext,
    ULONG Flags,
    PSOCKADDR LocalAddress,
    PSOCKADDR RemoteAddress,
    PWSK_SOCKET AcceptSocket,
    PVOID *AcceptSocketContext,
    CONST WSK_CLIENT_CONNECTION_DISPATCH **AcceptSocketDispatch
    )
{
  PWSK_APP_SOCKET_CONTEXT SocketContext;

  // Check for a valid new socket
  if (AcceptSocket != NULL)
  {
    // Allocate the socket context
    SocketContext =
      (PWSK_APP_SOCKET_CONTEXT)
        ExAllocatePoolWithTag(
          NonPagedPool,
          sizeof(WSK_APP_SOCKET_CONTEXT),
          SOCKET_CONTEXT_POOL_TAG
          );

    // Check result of allocation
    if (SocketContext == NULL)
    {
      // Reject the socket
      return STATUS_REQUEST_NOT_ACCEPTED;
    }

    // Initialize the socket context
    SocketContext->Socket = AcceptSocket;
    ...

    // Set the accepted socket's client context
    *AcceptSocketContext = SocketContext;

    // Set the accepted socket's dispatch table of callback functions
    *AcceptSocketDispatch = ConnectionDispatch;

    // Perform additional operations on the accepted socket
    ...

    // Return status indicating that the socket was accepted
    return STATUS_SUCCESS:
  }

  // Error with listening socket
  else
  {
    // Handle error
    ...

    // Return status indicating that no socket was accepted
    return STATUS_REQUEST_NOT_ACCEPTED;
  }
}
```

WSK 应用程序可将侦听套接字配置为有条件地接受在套接字上接收的传入连接。 WSK 应用程序通过在将套接字绑定到本地传输地址之前设置套接字[ **\_条件\_accept**](https://docs.microsoft.com/windows-hardware/drivers/network/so-conditional-accept) socket 选项，在侦听套接字上启用条件接受模式。 有关如何设置套接字选项的详细信息，请参阅[在套接字上执行控制操作](performing-control-operations-on-a-socket.md)。

如果在侦听套接字上启用条件接受模式，则每当在套接字上接收到新的传入连接请求时，WSK 子系统将首先调用套接字的[*WskInspectEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event)事件回调函数。 套接字的*WskInspectEvent*事件回调函数可以检查传入的连接请求，以确定是否应接受或拒绝该请求。 若要接受请求，套接字的*WskInspectEvent*事件回调函数将返回**InspectAccept**。 若要拒绝请求，套接字的*WskInspectEvent*事件回调函数将返回**InspectReject**。 如果套接字的*WskInspectEvent*事件回调函数无法立即确定是否应接受或拒绝该请求，则它将返回**InspectPend**。 在这种情况下，WSK 应用程序必须在完成传入连接请求的检查过程后调用[**WskInspectComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_complete)函数。 如果在完全建立套接字连接之前删除传入连接请求，则 WSK 子系统将调用 WSK 应用程序的[*WskAbortEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event)事件回调函数。

下面的代码示例演示 WSK 应用程序如何通过调用侦听套接字的*WskInspectEvent*事件回调函数的 WSK 子系统来检查传入的连接请求。

```C++
// Inspect ID for a pending inspection
WSK_INSPECT_ID PendingInspectID

// A listening socket's WskInspectEvent event callback function
WSK_INSPECT_ACTION WSKAPI
  WskInspectEvent(
    PVOID SocketContext,
    PSOCKADDR LocalAddress,
    PSOCKADDR RemoteAddress,
    PWSK_INSPECT_ID InspectID
    )
{
  // Check for a valid inspect ID
  if (InspectID != NULL)
  {
    // Inspect local and/or remote address of the incoming
    // connection request to determine if the connection should
    // be accepted or rejected.
    ...

    // If the incoming connection should be accepted
    if (...)
    {
      // Return status indicating that the incoming
      // connection request was accepted
      return InspectAccept;
    }

    // If the incoming connection should be rejected
    else if (...)
    {
      // Return status indicating that the incoming
      // connection request was rejected
      return InspectReject;
    }

    // Cannot determine immediately
    else
    {
      // Save the inspect ID while the inspection is pending.
      // This will be passed to WskInspectComplete when the
      // inspection process is completed.
      PendingInspectID = *InspectID;

      // Return status indicating that the result of the
      // inspection process for the incoming connection
      // request is pending
      return InspectPend;
    }
  }

  // Error with listening socket
  else
  {
    // Handle error
    ...

    // Return status indicating that a socket was not accepted
    return InspectReject;
  }
}

// A listening socket's WskAbortEvent event callback function
NTSTATUS WSKAPI
  WskAbortEvent(
    PVOID SocketContext,
    PWSK_INSPECT_ID InspectID
    )
{
  // Terminate the inspection for the incoming connection
  // request with a matching inspect ID. To test for a matching
  // inspect ID, the contents of the WSK_INSPECT_ID structures
  // must be compared, not the pointers to the structures.
  ...
}
```

如果 WSK 应用程序确定它将在启用了条件接受模式的侦听套接字上接受传入连接请求，则将建立传入连接，并可通过调用如前文所述， [**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)函数或 WSK 子系统调用套接字的[*WskAcceptEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)事件回调函数。

 

 





