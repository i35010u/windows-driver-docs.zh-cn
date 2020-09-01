---
title: 以 IRQL PASSIVE_LEVEL 获取设备配置信息
description: 以 IRQL PASSIVE_LEVEL 获取设备配置信息
ms.assetid: 672fb3d8-6e64-425b-a035-8f8ecfd624f1
keywords:
- I/o WDK 内核，设备配置空间
- 设备配置空间 WDK i/o
- 配置空间 WDK i/o
- 太空 WDK i/o
- PASSIVE_LEVEL WDK
- 驱动程序堆栈 WDK 配置信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d46cfb281398bff271814a48b8047e2f11414b4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191167"
---
# <a name="obtaining-device-configuration-information-at-irql--passive_level"></a>获取 IRQL = 被动级别的设备配置信息 \_





若要访问 IRQL = 被动级别的设备配置空间 \_ ，必须使用 [**irp \_ MN \_ READ \_ config**](./irp-mn-read-config.md) 和 [**irp \_ MN \_ WRITE \_ config**](./irp-mn-write-config.md)。 你在 IRP 堆栈中指示你要访问的配置空间和 i/o 缓冲区的位置。 有关更多详细信息，请参阅 [**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 结构的说明。

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

 

