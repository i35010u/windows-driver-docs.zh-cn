---
title: 将筛选设备对象附加到目标设备对象
description: 将筛选设备对象附加到目标设备对象
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d48e419c32dcb6bd221fb61264adf87eec4216
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837293"
---
# <a name="attaching-the-filter-device-object-to-the-target-device-object"></a>将筛选设备对象附加到目标设备对象


## <span id="ddk_attaching_the_filter_device_object_to_the_target_device_object_if"></span><span id="DDK_ATTACHING_THE_FILTER_DEVICE_OBJECT_TO_THE_TARGET_DEVICE_OBJECT_IF"></span>


调用 [**IoAttachDeviceToDeviceStackSafe**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe) 将筛选器设备对象附加到目标文件系统或卷的筛选器驱动程序堆栈。

```cpp
devExt = myLegacyFilterDeviceObject->DeviceExtension;

status = IoAttachDeviceToDeviceStackSafe(
           myLegacyFilterDeviceObject,        //SourceDevice
           DeviceObject,                      //TargetDevice
           &devext->AttachedToDeviceObject);  //AttachedToDeviceObject
```

请注意，如果其他任何筛选器已链接到 *目标设备* 指向的设备对象，则 *AttachedToDeviceObject* 输出参数收到的设备对象指针可能与 *目标设备* 不同。

### <a name="span-idattaching_to_a_file_system_by_namespanspan-idattaching_to_a_file_system_by_namespanspan-idattaching_to_a_file_system_by_namespanattaching-to-a-file-system-by-name"></a><span id="Attaching_to_a_File_System_by_Name"></span><span id="attaching_to_a_file_system_by_name"></span><span id="ATTACHING_TO_A_FILE_SYSTEM_BY_NAME"></span>按名称附加到文件系统

每个文件系统都需要创建一个或多个命名控制设备对象。 为了直接附加到特定的文件系统，文件系统筛选器驱动程序将相应的文件系统控制设备对象的名称传递到 [**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) ，以获取设备对象指针。 下面的代码段演示如何获取一个指向原始文件系统的两个控制设备对象之一的指针：

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

如果对 [**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) 的调用成功，则文件系统筛选器驱动程序可以调用 [**IoAttachDeviceToDeviceStackSafe**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe) 以附加到返回的控制设备对象。

**注意**   除了控制设备对象指针 (*rawDeviceObject*) ， [**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) 还会返回一个指向文件对象的指针， (*fileObject*) 以用户模式表示设备对象。 在上述代码片段中，不需要文件对象，因此可通过调用 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)将其关闭。 需要特别注意的是，减少 **plxntb** 返回的文件对象上的引用计数也会导致设备对象上的引用计数也减少。 因此，在上述对 **ObDereferenceObject** 的调用之后， *fileObject* 和 *rawDeviceObject* 指针应被视为无效，除非在为文件对象调用 **ObDereferenceObject** 之前，设备对象上的引用计数增加了对 [**ObReferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)的调用。

 

 

