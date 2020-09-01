---
title: 启用和禁用事件回调函数
description: 启用和禁用事件回调函数
ms.assetid: 52654788-31e2-47c1-8154-f40c42168708
keywords:
- WSK WDK 网络，事件
- 事件 WDK Winsock 内核
- 函数 WDK Winsock 内核
- 事件回调函数 WDK Winsock 内核
- SO_WSK_EVENT_CALLBACK
- WSK_SET_STATIC_EVENT_CALLBACKS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab0afd0f0a29b0cebf5bb1ee5c450565c2f17491
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211781"
---
# <a name="enabling-and-disabling-event-callback-functions"></a>启用和禁用事件回调函数


Winsock 内核 (WSK) 应用程序可以实现事件回调函数，WSK 子系统可以异步调用该函数来在套接字上发生特定 [事件](winsock-kernel-events.md) 时通知应用程序。 WSK 应用程序可以在创建套接字或接受侦听套接字上的套接字时，向 WSK 子系统提供客户端 [调度表](winsock-kernel-dispatch-tables.md) 结构。 此调度表包含指向新套接字的 WSK 应用程序的事件回调函数的指针。 如果 WSK 应用程序未实现特定套接字的任何事件回调函数，则不需要为该套接字的 WSK 子系统提供客户端调度表结构。

除了侦听套接字的 [*WskInspectEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event) 和 [*WskAbortEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event) 事件回调函数外，所有套接字事件回调函数都可以通过使用 [**SO \_ WSK \_ 事件 \_ 回调**](./so-wsk-event-callback.md) 套接字选项启用或禁用。 WSK 应用程序可以在一个套接字上同时启用多个事件回调函数。 但是，WSK 应用程序必须分别禁用每个事件回调函数。

下面的代码示例演示 WSK 应用程序如何使用 SO \_ WSK \_ 事件 \_ 回调套接字选项在面向连接的套接字上启用 [*WskDisconnectEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event) 和 [*WskReceiveEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event) 事件回调函数。

```C++
// Function to enable the WskDisconnectEvent and WskReceiveEvent
// event callback functions on a connection-oriented socket
NTSTATUS
  EnableDisconnectAndRecieveCallbacks(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  WSK_EVENT_CALLBACK_CONTROL EventCallbackControl;
  NTSTATUS Status;

  // Get pointer to the socket's provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

  // Specify the WSK NPI identifier
  EventCallbackControl.NpiId = &NPI_WSK_INTERFACE_ID;

  // Set the event flags for the event callback functions that
  // are to be enabled on the socket
  EventCallbackControl.EventMask =
    WSK_EVENT_DISCONNECT | WSK_EVENT_RECEIVE;

  // Initiate the control operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskSetOption,
      SO_WSK_EVENT_CALLBACK,
      SOL_SOCKET,
      sizeof(WSK_EVENT_CALLBACK_CONTROL),
      &EventCallbackControl,
      0,
      NULL,
      NULL,
      NULL  // No IRP for this control operation
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}
```

下面的代码示例演示 WSK 应用程序如何使用 [**SO \_ WSK \_ 事件 \_ 回调**](./so-wsk-event-callback.md) 套接字选项在面向连接的套接字上禁用 [*WskReceiveEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event) 事件回调函数。

```C++
// Prototype for the disable disconnect IoCompletion routine
NTSTATUS
  DisableDisconnectComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to disable the WskDisconnectEvent event
// callback functions on a connection-oriented socket
NTSTATUS
  DisableDisconnectCallback(
    PWSK_SOCKET Socket
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  PIRP Irp;
  WSK_EVENT_CALLBACK_CONTROL EventCallbackControl;
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
 DisableDisconnectComplete,
    Socket,  // Use the socket object for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Specify the WSK NPI identifier
  EventCallbackControl.NpiId = &NPI_WSK_INTERFACE_ID;

  // Set the event flag for the event callback function that
  // is to be disabled on the socket along with the disable flag
  EventCallbackControl.EventMask =
    WSK_EVENT_DISCONNECT | WSK_EVENT_DISABLE;

  // Initiate the control operation on the socket
  Status =
    Dispatch->WskControlSocket(
      Socket,
      WskSetOption,
      SO_WSK_EVENT_CALLBACK,
      SOL_SOCKET,
      sizeof(WSK_EVENT_CALLBACK_CONTROL),
      &EventCallbackControl,
      0,
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskControlSocket()
  return Status;
}

// Disable disconnect IoCompletion routine
NTSTATUS
  DisableDisconnectComplete(
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
    // The WskDisconnectEvent event callback
    // function is now disabled

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

对于侦听套接字，仅当 WSK 应用程序在套接字上启用条件接受模式时，才会启用 [*WskInspectEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event) 和 [*WskAbortEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event) 事件回调功能。 WSK 应用程序通过在将套接字绑定到本地传输地址之前为套接字设置 " [**SO \_ 条件 \_ 接受**](./so-conditional-accept.md) 套接字" 选项，在侦听套接字上启用条件接受模式。 有关如何设置套接字选项的详细信息，请参阅 [在套接字上执行控制操作](performing-control-operations-on-a-socket.md)。

在侦听套接字上启用条件接受模式后，不能禁用套接字的 *WskInspectEvent* 和 *WskAbortEvent* 事件回调功能。 有关在侦听套接字上有条件地接受传入连接的详细信息，请参阅 [侦听和接受传入连接](listening-for-and-accepting-incoming-connections.md)。

侦听套接字可以在面向连接的套接字上自动启用事件回调函数，该接口由侦听套接字的 [*WskAcceptEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event) 事件回调函数接受。 WSK 应用程序通过在侦听套接字上启用面向连接的套接字事件回调函数，自动启用这些回调函数。 有关此过程的详细信息，请 [**参阅 \_ WSK \_ 事件 \_ 回调**](./so-wsk-event-callback.md)。

如果 WSK 应用程序在其创建的每个套接字上始终启用特定的事件回调函数，则该应用程序可以将 WSK 子系统配置为使用 [**WSK \_ 设置 \_ 静态 \_ 事件 \_ 回调**](./wsk-set-static-event-callbacks.md) 客户端控制操作来自动启用这些事件回调函数。 以这种方式启用的事件回调函数始终处于启用状态，并且不能在以后由 WSK 应用程序禁用或重新启用。 如果 WSK 应用程序在其创建的每个套接字上始终启用特定的事件回调函数，应用程序应使用此方法来自动启用这些事件回调函数，因为它将产生更好的性能。

下面的代码示例演示 WSK 应用程序如何使用 WSK \_ 设置 \_ 静态 \_ 事件 \_ 回调客户端控制操作，在面向连接的套接字上自动启用 [*WskReceiveFromEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event) 事件回调函数和面向连接的套接字上的 [*WskReceiveEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event) 事件回调函数。

```C++
// Function to set static event callbacks
NTSTATUS
  SetStaticEventCallbacks(
    PWSK_APP_BINDING_CONTEXT BindingContext,
    )
{
  WSK_EVENT_CALLBACK_CONTROL EventCallbackControl;
  NTSTATUS Status;

  // Specify the WSK NPI identifier
  EventCallbackControl.NpiId = &NPI_WSK_INTERFACE_ID;

  // Set the event flags for the event callback functions that
  // are to be automatically enabled on every new socket
  EventCallbackControl.EventMask =
    WSK_EVENT_RECEIVE_FROM | WSK_EVENT_RECEIVE;

  // Perform client control operation
  Status =
    BindingContext->
      WskProviderDispatch->
        WskControlClient(
          BindingContext->WskClient,
          WSK_SET_STATIC_EVENT_CALLBACKS,
          sizeof(WSK_EVENT_CALLBACK_CONTROL),
          &EventCallbackControl,
          0,
          NULL,
          NULL,
          NULL  // No IRP for this control operation
          );

  // Return status of client control operation
  return Status;
}
```

如果 WSK 应用程序使用 WSK \_ 设置 \_ 静态 \_ 事件 \_ 回调客户端控制操作来自动启用特定的事件回调函数，则必须在创建任何套接字之前执行此操作。

 

