---
title: 将 IRP 与 Winsock 内核函数配合使用
description: 将 IRP 与 Winsock 内核函数配合使用
ms.assetid: eb7af09c-2312-4127-a0dc-324b208c1455
keywords:
- Winsock 内核 WDK 网络 Irp
- 网络、 WSK WDK Irp
- Irp WDK Winsock 内核
- WDK Winsock 内核函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f980dfd44c4337e4f94c83ead5104f48b2655b7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360733"
---
# <a name="using-irps-with-winsock-kernel-functions"></a>将 IRP 与 Winsock 内核函数配合使用


Winsock Kernel (WSK)[网络编程接口 (NPI)](network-programming-interface.md) Irp 用于异步网络 I/O 操作完成。 每个 WSK 函数将一个指针，到 IRP 作为参数。 WSK 子系统完成 IRP WSK 函数执行的操作完成后。

通过以下方式之一可以源自 IRP WSK 应用程序用来将传递给 WSK 函数。

-   WSK 应用程序通过调用分配 IRP [ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)函数。 在此情况下，WSK 应用程序必须分配至少一个 I/O 堆栈位置 IRP。

-   WSK 应用程序重复使用以前分配的已完成的 IRP。 在这种情况下，必须调用 WSK [ **IoReuseIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp)函数以重新初始化 IRP。

-   WSK 应用程序使用 IRP 的已传递给它的更高级别驱动程序或 I/O 管理器。 在此情况下，IRP 必须具有至少一个剩余 I/O 堆栈位置可用于 WSK 子系统。

WSK 应用程序具有 IRP 使用后调用 WSK 函数中，可以设置[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP IRP 完成 WSK 子系统时要调用的例程。 WSK 应用程序设置**IoCompletion** IRP 通过调用的例程[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)函数。 具体如何源于 IRP，取决于**IoCompletion**例程是必需还是可选。

-   如果 WSK 应用程序分配 IRP，或正在重用的以前分配，则必须设置 IRP **IoCompletion**之前调用 WSK 函数 IRP 的例程。 在这种情况下，必须指定 WSK 应用程序 **，则返回 TRUE**有关*InvokeOnSuccess*， *InvokeOnError*，并*InvokeOnCancel*参数传递给**IoSetCompletionRoutine**函数来确保**IoCompletion**始终调用例程。 此外， **IoCompletion** IRP 必须始终返回状态设置的例程\_详细\_处理\_必需终止 IRP 完成处理。 如果 WSK 应用程序执行此操作使用后的 IRP **IoCompletion**已调用例程，然后应调用[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)函数来释放之前 IRP返回从**IoCompletion**例程。 如果 WSK 应用程序不会释放 IRP，它可重用到另一个 WSK 函数调用的 IRP。

-   如果 WSK 应用程序使用 IRP 传递向下到它通过更高级别驱动程序或 I/O 管理器，它应设置**IoCompletion**例程的之前调用 WSK 函数，仅当它必须是 IRP 时收到通知操作执行由 WSK 函数已完成。 如果未设置 WSK 应用程序不会**IoCompletion** IRP 的例程，然后完成 IRP IRP 将传递备份到更高级别驱动程序或根据正常 IRP 完成处理的 I/O 管理器。 如果 WSK 应用程序设置**IoCompletion** IRP，为日常**IoCompletion**例程可以返回状态\_成功或状态\_详细\_处理\_必需。 如果**IoCompletion**例程将返回状态\_成功后，IRP 完成处理将继续正常运行。 如果**IoCompletion**例程将返回状态\_详细\_处理\_必需的 WSK 应用程序必须完成 IRP 通过调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)它完成处理的由 WSK 函数执行的操作结果后。 WSK 应用程序应永远不会释放已传递给它通过更高级别驱动程序或 I/O 管理器的 IRP。

**请注意**  如果 WSK 应用程序设置**IoCompletion**例程的 IRP 传递向下到它通过更高级别驱动程序或 I/O 管理器，则**IoCompletion**例程必须检查**PendingReturned** IRP 和调用的成员[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)函数如果**PendingReturned**成员是**TRUE**。 有关详细信息，请参阅[实现 IoCompletion 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-an-iocompletion-routine)。

 

WSK 应用程序不会初始化将传递给设置以外的 WSK 函数 Irp **IoCompletion**例程。 WSK 应用程序将 IRP 传递给 WSK 函数时, WSK 子系统设置代表应用程序的下一步 I/O 堆栈位置。

下面的代码示例演示如何分配和执行上一个套接字的接收操作时使用 IRP WSK 应用程序。

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

在上一示例中，其中 WSK 应用程序分配 IRP，然后将其释放完成例程中所示的模型是 WSK 文档的其余所有示例中使用的模型。

下面的代码示例演示如何 WSK 应用程序可以使用 IRP 传递给它通过更高级别驱动程序或 I/O 管理器执行套接字的接收操作时。

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
    PWSK_BUF DataBuffer,
    PIRP Irp;  // IRP from a higher level driver or the I/O manager
    )
{
  PWSK_PROVIDER_CONNECTION_DISPATCH Dispatch;
  NTSTATUS Status;

  // Get pointer to the provider dispatch structure
  Dispatch =
    (PWSK_PROVIDER_CONNECTION_DISPATCH)(Socket->Dispatch);

  // Set the completion routine for the IRP such that it is
  // only called if the receive operation succeeds.
  IoSetCompletionRoutine(
    Irp,
    ReceiveComplete,
    DataBuffer,  // Use the data buffer for the context
    TRUE,
    FALSE,
    FALSE
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

  // Since the completion routine was only specified to
  // be called if the operation succeeds, this should
  // always be true.
  ASSERT(Irp->IoStatus.Status == STATUS_SUCCESS);

  // Check the pending status of the IRP
  if (Irp->PendingReturned == TRUE)
  {
    // Mark the IRP as pending
    IoMarkIrpPending(Irp);
  }

  // Get the pointer to the data buffer
  DataBuffer = (PWSK_BUF)Context;
 
  // Get the number of bytes received
  ByteCount = (ULONG)(Irp->IoStatus.Information);

  // Process the received data
  ...

  // Return STATUS_SUCCESS to continue the
  // completion processing of the IRP.
  return STATUS_SUCCESS;
}
```

有关使用 Irp 的详细信息，请参阅[处理 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)。

 

 





