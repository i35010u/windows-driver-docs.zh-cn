---
title: 通过面向连接的套接字接收数据
description: 通过面向连接的套接字接收数据
ms.assetid: 189fa236-25d6-4eea-ad77-df76363576db
keywords:
- 面向连接的套接字 WDK Winsock 内核
- WskReceive
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50d984c939ed015fb5e1638385257e3f07c7b9de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358315"
---
# <a name="receiving-data-over-a-connection-oriented-socket"></a>通过面向连接的套接字接收数据


Winsock Kernel (WSK) 应用程序具有连接到远程传输地址的面向连接的套接字后它可通过套接字接收数据。 WSK 应用程序还可以通过面向连接的套接字，它接受在侦听套接字上接收数据。 WSK 应用程序通过调用通过面向连接的套接字接收数据[ **WskReceive** ](https://msdn.microsoft.com/library/windows/hardware/ff571139)函数。

下面的代码示例显示如何 WSK 应用程序可以通过面向连接的套接字接收数据。

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

作为调用的替代方法[ **WskReceive** ](https://msdn.microsoft.com/library/windows/hardware/ff571139)函数通过面向连接的套接字接收数据，WSK 应用程序可以启用[ *WskReceiveEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571140)套接字上的事件的回调函数。 如果启用了 WSK 应用程序*WskReceiveEvent*面向连接的套接字上的事件回调函数，WSK 子系统调用的套接字*WskReceiveEvent*每当事件回调函数套接字上收到新的数据。 有关启用面向连接的套接字的详细信息*WskReceiveEvent*事件回调函数，请参阅[启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

下面的代码示例显示如何 WSK 应用程序可以接收数据，调用面向连接的套接字的 WSK 子系统*WskReceiveEvent*事件回调函数。

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

如果面向连接的套接字[ *WskReceiveEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571140)事件回调函数不会检索包含在列表中的数据的所有[ **WSK\_数据\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff571165)指向结构*DataIndication*参数，它可以保留供进一步处理通过返回状态列表\_PENDING。 在这种情况下，WSK 应用程序必须调用[ **WskRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff571144)函数，以释放 WSK 列表\_数据\_指示结构回 WSK 子系统后完成列表中的结构中检索的所有数据。

如果面向连接的套接字*WskReceiveEvent*事件的回调函数只接受的接收数据的字节总数的一部分，但它必须设置该变量指向的*BytesAccepted*参数的实际已被接受的数据的字节数。 但是，如果对套接字*WskReceiveEvent*事件的回调函数接受所有接收到的数据，它不需要设置变量，指向*BytesAccepted*参数。

 

 





