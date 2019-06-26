---
title: 启用和禁用事件回调函数
description: 启用和禁用事件回调函数
ms.assetid: 52654788-31e2-47c1-8154-f40c42168708
keywords:
- WSK WDK 网络、 事件
- 事件 WDK Winsock 内核
- WDK Winsock 内核函数
- 事件回调函数 WDK Winsock 内核
- SO_WSK_EVENT_CALLBACK
- WSK_SET_STATIC_EVENT_CALLBACKS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbe301f93b4a0115e7a1c27e623a00832a16b4e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378699"
---
# <a name="enabling-and-disabling-event-callback-functions"></a>启用和禁用事件回调函数


Winsock Kernel (WSK) 应用程序可以实现事件回叫函数，WSK 子系统以异步方式调用以通知应用程序时某些[事件](winsock-kernel-events.md)套接字上发生。 WSK 应用程序可以提供客户端[调度表](winsock-kernel-dispatch-tables.md)WSK 子系统时它将创建一个套接字或接受上侦听套接字的套接字的结构。 此调度表包含指向新的套接字 WSK 应用程序的事件回调函数的指针。 如果 WSK 应用程序未实现特定套接字时，任何事件回调函数，则不需要提供客户端调度到此套接字的 WSK 子系统的表结构。

所有套接字的事件回调函数，但侦听套接字的除外[ *WskInspectEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_inspect_event)并[ *WskAbortEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_abort_event)事件可以启用或禁用通过使用回调函数[**因此\_WSK\_事件\_回调**](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-event-callback)套接字选项。 WSK 应用程序可以同时启用套接字上的多个事件回调函数。 但是，WSK 应用程序必须单独禁用每个事件的回调函数。

以下代码示例演示如何 WSK 应用程序可以使用 SO\_WSK\_事件\_回调套接字选项，若要启用[ *WskDisconnectEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect_event)和[ *WskReceiveEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event)面向连接的套接字上的事件回调函数。

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

下面的代码示例演示如何使用一个应用程序，WSK [**因此\_WSK\_事件\_回调**](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-event-callback)套接字选项来禁用[ *WskReceiveEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event)面向连接的套接字上的事件回调函数。

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

侦听套接字[ *WskInspectEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_inspect_event)并[ *WskAbortEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_abort_event)事件回调函数才会启用 WSK应用程序启用条件性接受套接字上的模式。 WSK 应用程序启用条件通过设置接受模式上侦听套接字[**因此\_条件\_接受**](https://docs.microsoft.com/windows-hardware/drivers/network/so-conditional-accept)套接字的套接字在绑定之前的选项为本地传输地址的套接字。 有关如何设置套接字选项的详细信息，请参阅[套接字上执行管理操作](performing-control-operations-on-a-socket.md)。

条件接受已启用上侦听模式之后套接字，套接字*WskInspectEvent*并*WskAbortEvent*事件回调函数不能禁用。 有关有条件地接受侦听套接字上的传入连接的详细信息，请参阅[用于侦听和接受传入连接](listening-for-and-accepting-incoming-connections.md)。

侦听套接字可以自动启用事件回调函数上都可以接受的侦听套接字的面向连接的套接字[ *WskAcceptEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event)事件回调函数。 WSK 应用程序会自动启用这些回调函数，通过启用侦听套接字上的面向连接的套接字事件回调函数。 有关此过程的详细信息，请参阅[**因此\_WSK\_事件\_回调**](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-event-callback)。

如果 WSK 应用程序始终启用它会创建每个套接字上的某些事件回调函数，该应用程序可以配置要通过使用自动启用这些事件的回调函数的 WSK 子系统[ **WSK\_设置\_静态\_事件\_回调**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-set-static-event-callbacks)客户端管理操作。 在这种方式中启用的事件回调函数始终处于启用状态，无法禁用或重新启用 WSK 应用程序的更高版本。 如果 WSK 应用程序始终启用它会创建每个套接字上的某些事件回调函数，该应用程序应使用此方法来自动启用这些事件的回调函数，因为它将产生更好的性能。

下面的代码示例演示如何 WSK 应用程序可以使用 WSK\_设置\_静态\_事件\_回调客户端管理操作来自动启用[ *WskReceiveFromEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from_event)数据报套接字上的事件的回调函数和[ *WskReceiveEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event)上面向连接的事件的回调函数套接字。

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

如果 WSK 应用程序使用 WSK\_设置\_静态\_事件\_回调客户端管理操作来自动启用某些事件的回调函数，它必须执行此操作之前创建任何套接字。

 

 





