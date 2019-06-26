---
title: 通过数据报套接字发送数据
description: 通过数据报套接字发送数据
ms.assetid: 5748ac2a-177f-4fe9-a55b-85eec45d5afa
keywords:
- 发送数据报
- 数据报套接字 WDK Winsock 内核
- WskSendTo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf31762e2c838a660b15d63045dbabefd0a862a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386848"
---
# <a name="sending-data-over-a-datagram-socket"></a>通过数据报套接字发送数据


Winsock Kernel (WSK) 应用程序已绑定到本地传输地址的数据报套接字后它可以通过套接字发送数据报。 WSK 应用程序通过调用通过数据报套接字发送数据报[ **WskSendTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_to)函数。

下面的代码示例显示如何 WSK 应用程序可以通过数据报套接字发送数据报。

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

WSK 应用程序已设置固定的远程传输地址或数据报套接字，一个固定的目标传输地址*RemoteAddress*参数传递给[ **WskSendTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_to)函数是可选的可以是**NULL**。 如果**NULL**，数据报发送到固定的远程传输地址或固定的目标传输地址。 如果非**NULL**，数据报发送到指定的远程传输地址。

有关如何设置固定的远程传输地址的数据报套接字的详细信息，请参阅[ **SIO\_WSK\_设置\_远程\_地址**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-set-remote-address)。

有关如何设置固定的目标传输地址的数据报套接字的详细信息，请参阅[ **SIO\_WSK\_设置\_SENDTO\_地址**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-wsk-set-sendto-address).

 

 





