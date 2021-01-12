---
title: 将 IRP 与 Winsock 内核函数配合使用
description: 将 IRP 与 Winsock 内核函数配合使用
keywords:
- Winsock 内核 WDK 网络，Irp
- WSK WDK 网络，Irp
- Irp WDK Winsock 内核
- 函数 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65555b89ae4acfbe4d55e14e95cf62074888d5f1
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124197"
---
# <a name="using-irps-with-winsock-kernel-functions"></a>将 IRP 与 Winsock 内核函数配合使用


Winsock 内核 (WSK) [网络编程接口 (NPI) ](network-programming-interface.md) 使用 irp 来完成网络 i/o 操作的异步完成。 每个 WSK 函数都采用一个指向 IRP 的指针作为参数。 当 WSK 函数执行的操作完成后，WSK 子系统完成 IRP。

WSK 应用程序用来传递到 WSK 函数的 IRP 可以通过下列方式之一进行。

-   WSK 应用程序通过调用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 函数分配 IRP。 在这种情况下，WSK 应用程序必须至少为一个 i/o 堆栈位置分配 IRP。

-   WSK 应用程序重复使用以前分配的已完成 IRP。 在这种情况下，WSK 必须调用 [**IoReuseIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp) 函数以重新初始化 IRP。

-   WSK 应用程序使用由较高级别的驱动程序或 i/o 管理器向下传递给它的 IRP。 在这种情况下，IRP 必须至少有一个可供 WSK 子系统使用的剩余 i/o 堆栈位置。

当 WSK 应用程序具有用于调用 WSK 函数的 IRP 后，它可以设置一个 [**IoCompletion**](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，以便在由 WSK 子系统完成 irp 后调用 irp。 WSK 应用程序通过调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)函数为 IRP 设置 **IoCompletion** 例程。 **IoCompletion** 例程是必需的，也可以是可选的，具体取决于 IRP 的生成方式。

-   如果 WSK 应用程序分配了 IRP，或重用了之前分配的 IRP，则在调用 WSK 函数之前，必须为 IRP 设置 **IoCompletion** 例程。 在这种情况下，WSK 应用程序必须为传递到 **IoSetCompletionRoutine** 函数的 *InvokeOnSuccess*、 *InvokeOnError* 和 *InvokeOnCancel* 参数指定 **TRUE** ，以确保始终调用 **IoCompletion** 例程。 而且，为 IRP 设置的 **IoCompletion** 例程必须始终返回状态， \_ \_ \_ 以便终止完成 IRP 的处理。 如果在调用 **IoCompletion** 例程后使用 IRP 完成了 WSK 应用程序，则它应调用 [**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp) 函数以释放 IRP，然后再从 **IoCompletion** 例程返回。 如果 WSK 应用程序没有释放 IRP，则它可以重复使用 IRP 来调用另一个 WSK 函数。

-   如果 WSK 应用程序使用由较高的级别驱动程序或 i/o 管理器向下传递给它的 IRP，则应在调用 WSK 函数之前为 IRP 设置 **IoCompletion** 例程，前提是 WSK 函数执行的操作已完成时必须收到通知。 如果 WSK 应用程序未为 IRP 设置 **IoCompletion** 例程，则完成 irp 后，irp 将按正常的 irp 完成处理方式传递回更高级别的驱动程序或 i/o 管理器。 如果 WSK 应用程序为 IRP 设置了 **IoCompletion** 例程，则 **IoCompletion** 例程可能会返回 "成功" 或 " \_ 状态" \_ 需要更多的 \_ 处理 \_ 。 如果 **IoCompletion** 例程返回状态 \_ SUCCESS，则 IRP 完成处理会正常继续。 如果 **IoCompletion** 例程返回 \_ \_ "需要更多的状态处理" \_ ，则 WSK 应用程序必须在处理完由 WSK 函数执行的操作的结果后调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，才能完成 IRP。 WSK 应用程序绝不应释放由较高级别的驱动程序或 i/o 管理器向下传递给它的 IRP。

**注意** 如果 WSK 应用程序为 IRP 设置了 **IoCompletion** 例程，而该 IRP 由较高级别的驱动程序或 i/o 管理器向下传递给它，则 **IoCompletion** 例程必须检查 IRP 的 **PendingReturned** 成员，如果 **也** 成员为 **TRUE**，则调用 [**PendingReturned**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)函数。 有关详细信息，请参阅 [实现 IoCompletion 例程](../kernel/implementing-an-iocompletion-routine.md)。

**注意** WSK 应用程序不应在 **IoCompletion** 例程的上下文中调用新的 WSK 函数。 这样做可能会导致递归调用和耗尽内核模式堆栈。 当在 IRQL = DISPATCH_LEVEL 上执行时，这也可能会导致其他线程不足。

WSK 应用程序不会初始化它传递给 WSK 函数的 Irp，而不是设置 **IoCompletion** 例程。 当 WSK 应用程序将 IRP 传递到 WSK 函数时，WSK 子系统代表应用程序设置下一个 i/o 堆栈位置。

下面的代码示例演示了在套接字上执行接收操作时，WSK 应用程序如何分配并使用 IRP。

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

上一示例中所示的模型，在该模型中，WSK 应用程序分配一个 IRP，然后在完成例程中将其释放，就是在整个 WSK 文档的其余部分中使用的示例模型。

下面的代码示例演示了 WSK 应用程序如何使用由较高级别的驱动程序或由 i/o 管理器在套接字上执行接收操作时传递给它的 IRP。

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

有关使用 Irp 的详细信息，请参阅 [处理 irp](../kernel/handling-irps.md)。

 

