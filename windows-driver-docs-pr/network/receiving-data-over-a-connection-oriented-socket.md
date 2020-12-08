---
title: 通过面向连接的套接字接收数据
description: 通过面向连接的套接字接收数据
keywords:
- 面向连接的套接字 WDK Winsock 内核
- WskReceive
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1364403a7303f10839e1e0ae506c78ad7e6a1b90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793367"
---
# <a name="receiving-data-over-a-connection-oriented-socket"></a>通过面向连接的套接字接收数据


Winsock 内核 (WSK) 应用程序已将面向连接的套接字连接到远程传输地址，它可以通过套接字接收数据。 WSK 应用程序还可以通过面向连接的套接字接收数据，该套接字在侦听套接字上接受。 WSK 应用程序通过调用 [**WskReceive**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive) 函数，在面向连接的套接字上接收数据。

下面的代码示例演示 WSK 应用程序如何通过面向连接的套接字接收数据。

```C++
// Prototype for the receive IoCompletion routine
NTSTATUS
  ReceiveComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to receive data
NTSTATUS
  ReceiveData(
    PWSK_SOCKET Socket,
    PWSK_BUF DataBuffer
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  PIRP Irp;
  NTSTATUS Status;

  // Get pointer to the provider dispatch structure
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
    ReceiveComplete,
    DataBuffer,  // Use the data buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the receive operation on the socket
  Status =
    Dispatch->WskReceive(
      Socket,
      DataBuffer,
      0,  // No flags are specified
      Irp
      );

  // Return the status of the call to WskReceive()
  return Status;
}

// Receive IoCompletion routine
NTSTATUS
  ReceiveComplete(
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

    // Process the received data
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

作为调用 [**WskReceive**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive) 函数通过面向连接的套接字接收数据的一种替代方法，WSK 应用程序可以在套接字上启用 [*WskReceiveEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event) 事件回调函数。 如果 WSK 应用程序在面向连接的套接字上启用 *WskReceiveEvent* 事件回调函数，则每当在套接字上收到新数据时，WSK 子系统都会调用套接字的 *WskReceiveEvent* 事件回调函数。 有关启用面向连接的套接字的 *WskReceiveEvent* 事件回调函数的详细信息，请参阅 [启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

下面的代码示例演示 WSK 应用程序如何通过调用面向连接的套接字的 *WskReceiveEvent* 事件回调函数的 WSK 子系统来接收数据。

```C++
// A connection-oriented socket's WskReceiveEvent
// event callback function
NTSTATUS WSKAPI
  WskReceiveEvent(
    PVOID SocketContext,
    ULONG Flags,
    PWSK_DATA_INDICATION DataIndication,
    SIZE_T BytesIndicated,
    SIZE_T *BytesAccepted
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

    // Return status indicating the data was received
    return STATUS_SUCCESS;
  }

  // Error
  else
  {
    // Close the socket
    ...

    // Return success since no data was indicated
    return STATUS_SUCCESS;
  }
}
```

如果面向连接的套接字的 [*WskReceiveEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)事件回调函数未检索 *DataIndication* 参数指向的 [**WSK \_ 数据 \_ 指示**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_data_indication)结构列表中包含的所有数据，则它可以通过返回 "挂起" 状态，保留该列表以供进一步处理 \_ 。 在这种情况下，WSK 应用程序必须调用 [**WskRelease**](/previous-versions/windows/hardware/drivers/ff571144(v=vs.85)) 函数，以便在 \_ \_ 完成从列表中的结构检索所有数据后，将 WSK 数据指示结构的列表释放回 WSK 子系统。

如果面向连接的套接字的 *WskReceiveEvent* 事件回调函数只接受收到的数据的总字节数，则必须将 *BytesAccepted* 参数指向的变量设置为实际接受的数据字节数。 但是，如果套接字的 *WskReceiveEvent* 事件回调函数接受所有接收到的数据，则不需要设置 *BytesAccepted* 参数指向的变量。

 

