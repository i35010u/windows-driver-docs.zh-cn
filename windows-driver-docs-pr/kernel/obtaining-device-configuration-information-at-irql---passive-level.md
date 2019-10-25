---
title: 获取 IRQL PASSIVE_LEVEL 的设备配置信息
description: 获取 IRQL PASSIVE_LEVEL 的设备配置信息
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
ms.openlocfilehash: cebb5529949268dd829db22c20b9e77a88ff348f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827748"
---
# <a name="obtaining-device-configuration-information-at-irql--passive_level"></a>获取 IRQL = 被动\_级别的设备配置信息





若要以 IRQL = 被动\_级别访问设备配置空间，必须使用[**IRP\_MN\_读取\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)和[**IRP\_MN\_写入\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)。 你在 IRP 堆栈中指示你要访问的配置空间和 i/o 缓冲区的位置。 有关更多详细信息，请参阅[**IO\_STACK\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的说明。

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

 

 




