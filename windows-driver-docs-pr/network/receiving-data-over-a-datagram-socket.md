---
title: 通过数据报套接字接收数据
description: 通过数据报套接字接收数据
ms.assetid: 650b7688-967e-4ce6-80ad-8f7b6e1ec009
keywords:
- 接收数据报
- 数据报套接字 WDK Winsock 内核
- WskReceiveFrom
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173313f81984b4cbe9c241563a8366d072d7405c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216950"
---
# <a name="receiving-data-over-a-datagram-socket"></a>通过数据报套接字接收数据


Winsock 内核 (WSK) 应用程序已将数据报套接字绑定到本地传输地址，它可以通过套接字接收数据报。 WSK 应用程序通过调用 [**WskReceiveFrom**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from) 函数接收数据报套接字上的数据报。

下面的代码示例演示 WSK 应用程序如何通过数据报套接字接收数据报。

```C++
// Prototype for the receive datagram IoCompletion routine
NTSTATUS
  ReceiveDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to receive a datagram
NTSTATUS
  ReceiveDatagram(
    PWSK_SOCKET Socket,
    PWSK_BUF DatagramBuffer
    )
{
  PWSK_PROVIDER_DATAGRAM_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the provider dispatch structure
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
    ReceiveDatagramComplete,
    DatagramBuffer,  // Use the datagram buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the receive operation on the socket
  Status =
    Dispatch->WskReceiveFrom(
      Socket,
      DatagramBuffer,
      0,  // No flags are specified
      NULL,  // Not interested in the remote address
      NULL,  // Not interested in any associated control information
      NULL,
      NULL,
      Irp
      );

  // Return the status of the call to WskReceiveFrom()
  return Status;
}

// Receive datagram IoCompletion routine
NTSTATUS
  ReceiveDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_BUF DataBuffer;
  ULONG ByteCount;

  // Check the result of the receive operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the data buffer
    DataBuffer = (PWSK_BUF)Context;
 
    // Get the number of bytes received
    ByteCount = (ULONG)(Irp->IoStatus.Information);

    // Process the received datagram
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

作为调用 [**WskReceiveFrom**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from) 函数以接收数据报套接字上的每个数据报的替代方法，WSK 应用程序可以在套接字上启用 [*WskReceiveFromEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event) 事件回调函数。 如果 WSK 应用程序在数据报套接字上启用 *WskReceiveFromEvent* 事件回调函数，则每当在套接字上接收到新的数据报时，WSK 子系统都会调用套接字的 *WskReceiveFromEvent* 事件回调函数。 有关启用数据报套接字的 *WskReceiveFromEvent* 事件回调函数的详细信息，请参阅 [启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

下面的代码示例演示 WSK 应用程序如何通过调用数据报套接字的 *WskReceiveFromEvent* 事件回调函数来通过 WSK 子系统接收数据报。

```C++
// A datagram socket's WskReceiveFromEvent
// event callback function
NTSTATUS WSKAPI
  WskReceiveFromEvent(
    PVOID SocketContext,
    ULONG Flags,
    PWSK_DATAGRAM_INDICATION DataIndication
    )
{
  // Check for a valid data indication
  if (DataIndication != NULL)
  {
    // Loop through the list of data indication structures
    while (DataIndication != NULL)
    {
      // Process the data in the data indication structure
      ...

      // Move to the next data indication structure
      DataIndication = DataIndication->Next;
    }

    // Return status indicating the datagrams were received
    return STATUS_SUCCESS;
  }

  // Error
  else
  {
    // Close the socket
    ...

    // Return success since no datagrams were indicated
    return STATUS_SUCCESS;
  }
}
```

如果数据报套接字的[*WskReceiveFromEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)事件回调函数不会从*DataIndication*参数指向的[**WSK \_ 数据报 \_ 指示**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_datagram_indication)结构列表中检索所有数据报，则可以通过返回 "挂起" 状态，保留该列表以供进一步处理 \_ 。 在这种情况下，WSK 应用程序必须调用 [**WskRelease**](/previous-versions/windows/hardware/drivers/ff571144(v=vs.85)) 函数，以便在 \_ \_ 完成从列表中的结构检索所有数据报后，将 WSK 数据报指示结构的列表释放回 WSK 子系统。

 

