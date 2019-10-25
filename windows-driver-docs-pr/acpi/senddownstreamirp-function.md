---
title: SendDownStreamIrp 函数
description: SendDownStreamIrp 函数
ms.assetid: 09a06041-5b26-4796-b9b8-d7d27321d955
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 899f65d78d2e4b05a8eba84d44e082b1f75c9b17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831468"
---
# <a name="senddownstreamirp-function"></a>SendDownStreamIrp 函数


本主题中提供的 `SendDownStreamIrp` 函数的代码示例演示如何实现将同步 IOCTL 请求发送到 ACPI 驱动程序的驱动程序提供的函数。 `SendDownStreamIrp` 函数可用于发送[**ioctl\_acpi\_EVAL\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)请求、 [**ioctl\_acpi\_EVAL\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)请求或[**ioctl\_acpi\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求。

本部分中包含的 `SendDownStreamIrp` 函数的代码示例将执行以下操作序列：

-   创建事件对象。

-   调用[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)创建 IOCTL 请求。

-   调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)以发送 IOCTL 请求。

-   等待 ACPI 驱动程序通知事件对象，这表示请求已完成。

-   返回调用方的请求状态。

```cpp
NTSTATUS
SendDownStreamIrp(
    IN PDEVICE_OBJECT   Pdo,
    IN ULONG            Ioctl,
    IN PVOID            InputBuffer,
    IN ULONG            InputSize,
    IN PVOID            OutputBuffer,
    IN ULONG            OutputSize
)
/*
Routine Description:
    General-purpose function called to send a request to the PDO. 
    The IOCTL argument accepts the control method being passed down
    by the calling function

    This subroutine is only valid for the IOCTLS other than ASYNC EVAL. 

Parameters:
    Pdo             - the request is sent to this device object
    Ioctl           - the request - specified by the calling function
    InputBuffer     - incoming request
    InputSize       - size of the incoming request
    OutputBuffer    - the answer
    OutputSize      - size of the answer buffer

Return Value:
    NT Status of the operation
*/
{
    IO_STATUS_BLOCK     ioBlock;
    KEVENT              myIoctlEvent;
    NTSTATUS            status;
    PIRP                irp;

    // Initialize an event to wait on
    KeInitializeEvent(&myIoctlEvent, SynchronizationEvent, FALSE);

    // Build the request
    irp = IoBuildDeviceIoControlRequest(
        Ioctl, 
        Pdo,
        InputBuffer,
        InputSize,
        OutputBuffer,
        OutputSize,
        FALSE,
        &myIoctlEvent,
        &ioBlock);

    if (!irp) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    // Pass request to Pdo, always wait for completion routine
    status = IoCallDriver(Pdo, irp);

    if (status == STATUS_PENDING) {
        // Wait for the IRP to be completed, and then return the status code
        KeWaitForSingleObject(
            &myIoctlEvent,
            Executive,
            KernelMode,
            FALSE,
            NULL);

        status = ioBlock.Status;
    }

    return status;
}
```

 

 




