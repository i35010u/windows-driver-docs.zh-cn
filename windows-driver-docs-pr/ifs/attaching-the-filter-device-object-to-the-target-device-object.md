---
title: 将筛选设备对象附加到目标设备对象
description: 将筛选设备对象附加到目标设备对象
ms.assetid: 1df293db-417a-4fee-afb8-06ab527331fb
keywords:
- 筛选器驱动程序 WDK 文件系统，将附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 附加到文件系统卷的筛选器
- WDK 卷文件系统，将附加筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 632edab4f8ae70809e4ab42e31f9a62dd1d23282
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385317"
---
# <a name="attaching-the-filter-device-object-to-the-target-device-object"></a>将筛选设备对象附加到目标设备对象


## <span id="ddk_attaching_the_filter_device_object_to_the_target_device_object_if"></span><span id="DDK_ATTACHING_THE_FILTER_DEVICE_OBJECT_TO_THE_TARGET_DEVICE_OBJECT_IF"></span>


调用[ **IoAttachDeviceToDeviceStackSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)将筛选器设备对象附加到的目标文件系统或卷的筛选器驱动程序堆栈。

```cpp
devExt = myLegacyFilterDeviceObject->DeviceExtension;

status = IoAttachDeviceToDeviceStackSafe(
           myLegacyFilterDeviceObject,        //SourceDevice
           DeviceObject,                      //TargetDevice
           &devext->AttachedToDeviceObject);  //AttachedToDeviceObject
```

请注意，由接收设备对象指针*AttachedToDeviceObject*输出参数可能不同于*目标设备*如果任何其他筛选器已链接在上面的设备对象指向*目标设备*。

### <a name="span-idattachingtoafilesystembynamespanspan-idattachingtoafilesystembynamespanspan-idattachingtoafilesystembynamespanattaching-to-a-file-system-by-name"></a><span id="Attaching_to_a_File_System_by_Name"></span><span id="attaching_to_a_file_system_by_name"></span><span id="ATTACHING_TO_A_FILE_SYSTEM_BY_NAME"></span>将附加到通过名称的文件系统

每个文件系统需要创建一个或多个命名控件的设备对象。 若要附加到特定的文件系统直接，文件系统筛选器驱动程序，将传递到相应的文件系统控制设备对象的名称[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)若要获取的设备对象指针。 下面的代码段演示如何获取此类指针到两个控制设备对象之一的原始文件系统：

```cpp
RtlInitUnicodeString(&nameString, L"\\Device\\RawDisk");

status = IoGetDeviceObjectPointer(
            &nameString,                    //ObjectName
            FILE_READ_ATTRIBUTES,           //DesiredAccess
            &fileObject,                    //FileObject
            &rawDeviceObject);              //DeviceObject

if (NT_SUCCESS(status)) {
            ObDereferenceObject(fileObject);
}
```

如果在调用[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)成功，文件系统筛选器驱动程序然后可以调用[ **IoAttachDeviceToDeviceStackSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)将附加到返回的控件设备对象。

**请注意**  除了控制设备对象指针 (*rawDeviceObject*)， [ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)返回指向的指针文件对象 (*的文件对象*)，表示在用户模式下的设备对象。 在上面的代码段中，文件对象不需要因此通过调用关闭[ **ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)。 务必要注意返回的文件对象的引用计数的递减**IoGetDeviceObjectPointer**导致设备对象也是递减引用计数。 从而*的文件对象*并*rawDeviceObject*指针应同时考虑无效上述调用后**ObDereferenceObject**，除非的引用计数设备对象就会递增额外调用[ **ObReferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)之前**ObDereferenceObject**称为文件对象。

 

 

 




