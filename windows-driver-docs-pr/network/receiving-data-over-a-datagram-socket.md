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
ms.openlocfilehash: 3c0d272ce226776387d5f53a772d7cec34621541
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349628"
---
# <a name="receiving-data-over-a-datagram-socket"></a>通过数据报套接字接收数据


Winsock Kernel (WSK) 应用程序已绑定到本地传输地址的数据报套接字后它可通过套接字接收数据报。 WSK 应用程序通过调用通过数据报套接字接收数据报[ **WskReceiveFrom** ](https://msdn.microsoft.com/library/windows/hardware/ff571141)函数。

下面的代码示例演示如何 WSK 应用程序可以通过数据报套接字接收数据报。

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

作为调用的替代方法[ **WskReceiveFrom** ](https://msdn.microsoft.com/library/windows/hardware/ff571141)函数将通过数据报套接字接收每个数据报、 WSK 应用程序可以启用[ *WskReceiveFromEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571142)套接字上的事件的回调函数。 如果启用了 WSK 应用程序*WskReceiveFromEvent*数据报套接字上的事件回调函数，WSK 子系统调用的套接字*WskReceiveFromEvent*每当新事件的回调函数套接字上接收的数据报。 有关启用数据报套接字的详细信息*WskReceiveFromEvent*事件回调函数，请参阅[启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

下面的代码示例演示如何 WSK 应用程序可以接收数据报 WSK 子系统通过调用数据报套接字*WskReceiveFromEvent*事件回调函数。

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

如果数据报套接字[ *WskReceiveFromEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571142)事件回调函数不会检索所有的数据报中的列表[ **WSK\_数据报\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff571164)指向结构*DataIndication*参数，它可以保留供进一步处理通过返回状态列表\_PENDING。 在这种情况下，WSK 应用程序必须调用[ **WskRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff571144)函数，以释放 WSK 列表\_数据报\_指示结构回 WSK 子系统后它已完成列表中的结构中检索所有的数据报。

 

 





