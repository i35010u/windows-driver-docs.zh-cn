---
title: 通过面向连接的套接字发送数据
description: 通过面向连接的套接字发送数据
ms.assetid: 290f3a8a-6bdc-4dd9-a9bf-4eede37bf1e5
keywords:
- 面向连接的套接字 WDK Winsock 内核
- WskSend
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4fe2aef88176a0b7acff4a4a695cc822637b29d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841973"
---
# <a name="sending-data-over-a-connection-oriented-socket"></a>通过面向连接的套接字发送数据


Winsock 内核（WSK）应用程序将面向连接的套接字连接到远程传输地址后，它可以通过套接字发送数据。 WSK 应用程序还可以通过一个面向连接的套接字发送数据，该套接字在侦听套接字上接受。 WSK 应用程序通过调用[**WskSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send)函数，在面向连接的套接字上发送数据。

下面的代码示例演示 WSK 应用程序如何通过面向连接的套接字发送数据。

```C++
// Prototype for the send IoCompletion routine
NTSTATUS
  SendComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    );

// Function to send data
NTSTATUS
  SendData(
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
    SendComplete,
    DataBuffer,  // Use the data buffer for the context
    TRUE,
    TRUE,
    TRUE
    );

  // Initiate the send operation on the socket
  Status =
    Dispatch->WskSend(
      Socket,
      DataBuffer,
      0,  // No flags
      Irp
      );

  // Return the status of the call to WskSend()
  return Status;
}

// Send IoCompletion routine
NTSTATUS
  SendComplete(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PVOID Context
    )
{
  UNREFERENCED_PARAMETER(DeviceObject);

  PWSK_BUF DataBuffer;
  ULONG ByteCount;

  // Check the result of the send operation
  if (Irp->IoStatus.Status == STATUS_SUCCESS)
  {
    // Get the pointer to the data buffer
    DataBuffer = (PWSK_BUF)Context;

    // Get the number of bytes sent
    ByteCount = (ULONG)(Irp->IoStatus.Information);

    // Re-use or free the data buffer
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

 

 





