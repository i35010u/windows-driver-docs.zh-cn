---
title: 获取设备配置信息在 IRQL passive_level 调用
description: 获取设备配置信息在 IRQL passive_level 调用
ms.assetid: 672fb3d8-6e64-425b-a035-8f8ecfd624f1
keywords:
- I/O WDK 内核，设备配置空间
- 设备配置空间 WDK I/O
- 配置空间 WDK I/O
- 空间 WDK I/O
- PASSIVE_LEVEL WDK
- 驱动程序堆栈 WDK 配置信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd7b651700e2d811a0ffe3437f45e1b9ed92ea68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352061"
---
# <a name="obtaining-device-configuration-information-at-irql--passivelevel"></a>获取设备配置信息在 IRQL = 被动\_级别





向访问设备配置空间在 IRQL = 被动\_级别，则必须使用[ **IRP\_MN\_读取\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551727)和[ **IRP\_MN\_编写\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551769)。 指示 IRP 堆栈中你想要访问和其中的 I/O 缓冲区是其配置空间。 请参阅的说明[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)更多详细信息的结构。

下面的代码示例演示如何访问设备的配置空间。

```cpp
NTSTATUS
ReadWriteConfigSpace(
    IN PDEVICE_OBJECT  DeviceObject,
    IN ULONG  ReadOrWrite,  // 0 for read, 1 for write
    IN PVOID  Buffer,
    IN ULONG  Offset,
    IN ULONG  Length
    )
{
    KEVENT event;
    NTSTATUS status;
    PIRP irp;
    IO_STATUS_BLOCK ioStatusBlock;
    PIO_STACK_LOCATION irpStack;
    PDEVICE_OBJECT targetObject;

    PAGED_CODE();
    KeInitializeEvent(&event, NotificationEvent, FALSE);
    targetObject = IoGetAttachedDeviceReference(DeviceObject);
    irp = IoBuildSynchronousFsdRequest(IRP_MJ_PNP,
                                       targetObject,
                                       NULL,
                                       0,
                                       NULL,
                                       &event,
                                       &ioStatusBlock);
    if (irp == NULL) {
        status = STATUS_INSUFFICIENT_RESOURCES;
        goto End;
    }
    irpStack = IoGetNextIrpStackLocation(irp);
    if (ReadOrWrite == 0) {
        irpStack->MinorFunction = IRP_MN_READ_CONFIG;
    } else {
        irpStack->MinorFunction = IRP_MN_WRITE_CONFIG;
    }
    irpStack->Parameters.ReadWriteConfig.WhichSpace = PCI_WHICHSPACE_CONFIG;
    irpStack->Parameters.ReadWriteConfig.Buffer = Buffer;
    irpStack->Parameters.ReadWriteConfig.Offset = Offset;
    irpStack->Parameters.ReadWriteConfig.Length = Length;

    // Initialize the status to error in case the bus driver does not 
    // set it correctly.
    irp->IoStatus.Status = STATUS_NOT_SUPPORTED;
    status = IoCallDriver(targetObject, irp);
    if (status == STATUS_PENDING) {
        KeWaitForSingleObject(&event, Executive, KernelMode, FALSE, NULL);
        status = ioStatusBlock.Status;
    }
End:
    // Done with reference
    ObDereferenceObject(targetObject);
    return status;
}
```

 

 




