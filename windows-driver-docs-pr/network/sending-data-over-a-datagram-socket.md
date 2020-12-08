---
title: 通过数据报套接字发送数据
description: 通过数据报套接字发送数据
keywords:
- 发送数据报
- 数据报套接字 WDK Winsock 内核
- WskSendTo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a563d15ba5752316a9e921e72b7c556b7d145af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840273"
---
# <a name="sending-data-over-a-datagram-socket"></a>通过数据报套接字发送数据


Winsock 内核 (WSK) 应用程序已将数据报套接字绑定到本地传输地址，它可以通过套接字发送数据报。 WSK 应用程序通过调用 [**WskSendTo**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_to) 函数在数据报套接字上发送数据报。

下面的代码示例演示 WSK 应用程序如何通过数据报套接字发送数据报。

```C++
// Prototype for the send datagram IoCompletion routine
NTSTATUS
  SendDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to send a datagram
NTSTATUS
  SendDatagram(
    PWSK_SOCKET Socket,
    PWSK_BUF DatagramBuffer,
    PSOCKADDR RemoteAddress
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
    SendDatagramComplete,
    DatagramBuffer,  // Use the datagram buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the send operation on the socket
  Status =
    Dispatch->WskSendTo(
      Socket,
      DatagramBuffer,
      0,  // No flags
      RemoteAddress,
      0,
      NULL,  // No associated control info
      Irp
      );

  // Return the status of the call to WskSendTo()
  return Status;
}

// Send datagram IoCompletion routine
NTSTATUS
  SendDatagramComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_BUF DatagramBuffer;
  ULONG ByteCount;

  // Check the result of the send operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the datagram buffer
    DatagramBuffer = (PWSK_BUF)Context;

    // Get the number of bytes sent
    ByteCount = (ULONG)(Irp->IoStatus.Information);

    // Re-use or free the datagram buffer
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

如果 WSK 应用程序已为数据报套接字设置固定远程传输地址或固定目标传输地址，则传递到 [**WskSendTo**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_to)函数的 *RemoteAddress* 参数是可选的，并且可以为 **NULL**。 如果 **为 NULL**，则将数据报发送到固定远程传输地址或固定目标传输地址。 如果非 **NULL**，则将数据报发送到指定的远程传输地址。

有关为数据报套接字设置固定远程传输地址的详细信息，请参阅 [**SIO \_ WSK \_ SET \_ remote \_ address**](./sio-wsk-set-remote-address.md)。

有关为数据报套接字设置固定目标传输地址的详细信息，请参阅 [**SIO \_ WSK \_ SET \_ SENDTO \_ address**](./sio-wsk-set-sendto-address.md)。

 

