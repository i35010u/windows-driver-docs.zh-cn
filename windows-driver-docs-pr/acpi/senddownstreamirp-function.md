---
title: SendDownStreamIrp 函数
description: SendDownStreamIrp 函数
ms.assetid: 09a06041-5b26-4796-b9b8-d7d27321d955
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c9a373a1b43f86a6e8feeca3bfab3badfaa8db8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329717"
---
# <a name="senddownstreamirp-function"></a>SendDownStreamIrp 函数


代码示例`SendDownStreamIrp`本主题中提供的函数演示如何实现将同步 IOCTL 请求发送到 ACPI 驱动程序的驱动程序所提供的函数。 `SendDownStreamIrp`函数可用于发送[ **IOCTL\_ACPI\_EVAL\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff536148)请求， [ **IOCTL\_ACPI\_EVAL\_方法\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff536149)请求，或[ **IOCTL\_ACPI\_枚举\_子级**](https://msdn.microsoft.com/library/windows/hardware/ff536147)请求。

代码示例`SendDownStreamIrp`函数包含在本部分中执行以下一系列操作：

-   创建一个事件对象。

-   调用[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)创建 IOCTL 请求。

-   调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)发送 IOCTL 请求。

-   等待，直到 ACPI 驱动程序发出信号的事件对象，它指示请求已完成。

-   返回给调用方请求的状态。

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

 

 




