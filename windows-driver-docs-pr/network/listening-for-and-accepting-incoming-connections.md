---
title: 侦听和接受传入连接
description: 侦听和接受传入连接
ms.assetid: 3ec7d6d0-8b8c-4d98-9e2a-e42b52dcd544
keywords:
- Winsock 内核 WDK 网络的传入连接
- WSK WDK 网络的传入连接
- 传入连接 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 条件接受 WDK Winsock 内核
- 侦听操作 WDK Winsock 内核
- SO_CONDITIONAL_ACCEPT
- 接受连接 WDK Winsock 内核
- WskAccept
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52b327b972090ef5be6981e79bcf1b9bd290584
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522174"
---
# <a name="listening-for-and-accepting-incoming-connections"></a>侦听和接受传入连接


Winsock Kernel (WSK) 应用程序将侦听套接字绑定到本地传输地址后，套接字开始侦听来自远程传输地址的传入连接。 WSK 应用程序可以通过调用接受传入连接上侦听套接字[ **WskAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff571109)函数。 应用程序传递到 IRP **WskAccept**函数会排队，直到到达的传入连接。

下面的代码示例演示如何 WSK 应用程序可以接受传入连接，通过调用**WskAccept**函数。

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

作为调用的替代方法[ **WskAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff571109)函数以接受传入的连接上侦听套接字、 WSK 应用程序可以启用[ *WskAcceptEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571120)套接字上的事件的回调函数。 如果启用了 WSK 应用程序*WskAcceptEvent*侦听套接字上的事件回调函数，WSK 子系统调用的套接字*WskAcceptEvent*每当新传入事件的回调函数套接字上接受连接。 有关启用侦听套接字的详细信息*WskAcceptEvent*事件回调函数，请参阅[启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

下面的代码示例演示如何 WSK 应用程序可以接受传入连接，通过调用侦听套接字的 WSK 子系统*WskAcceptEvent*事件回调函数。

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

WSK 应用程序可以配置侦听套接字来有条件地接受套接字接收的传入连接。 WSK 应用程序启用条件通过设置接受模式上侦听套接字[**因此\_条件\_接受**](https://msdn.microsoft.com/library/windows/hardware/ff570829)套接字的套接字在绑定之前的选项为本地传输地址的套接字。 有关如何设置套接字选项的详细信息，请参阅[套接字上执行管理操作](performing-control-operations-on-a-socket.md)。

如果条件接受侦听套接字上已启用模式，WSK 子系统首先调用的套接字[ *WskInspectEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571137)事件回调函数的新的传入连接请求时套接字上接收。 一个套接字*WskInspectEvent*事件回调函数可以检查传入的连接请求，以确定是否应接受或拒绝该请求。 若要接受请求，套接字*WskInspectEvent*事件回调函数返回**InspectAccept**。 若要拒绝请求，套接字*WskInspectEvent*事件回调函数返回**InspectReject**。 如果套接字*WskInspectEvent*事件的回调函数不能立即确定是否应接受或拒绝请求，它将返回**InspectPend**。 在这种情况下，WSK 应用程序必须调用[ **WskInspectComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff571136)函数之后，完成的传入连接请求的检查过程。 如果传入的连接请求将删除之前完全建立套接字连接，WSK 子系统会调用 WSK 应用程序的[ *WskAbortEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571108)事件回调函数。

下面的代码示例演示如何 WSK 应用程序可以通过调用侦听套接字的 WSK 子系统检查传入的连接请求*WskInspectEvent*事件回调函数。

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

如果 WSK 应用程序确定，它会接受具有条件接受模式已启用侦听套接字上传入的连接请求，将建立传入连接，并可以通过调用到任一应用程序通常接受[ **WskAccept** ](https://msdn.microsoft.com/library/windows/hardware/ff571109)函数或调用的套接字的 WSK 子系统[ *WskAcceptEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571120)所述的事件的回调函数以前。

 

 





