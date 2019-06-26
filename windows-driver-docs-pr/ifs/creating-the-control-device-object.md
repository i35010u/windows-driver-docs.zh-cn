---
title: 创建控制设备对象
description: 创建控制设备对象
ms.assetid: 9f89fd24-59b8-4529-b151-4e91e6334173
keywords:
- 控制设备对象 WDK 文件系统
- CDOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca04fd82f9048a8f388a665f2a5b1c4cd662bba8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366789"
---
# <a name="creating-the-control-device-object"></a>创建控制设备对象


## <span id="ddk_creating_the_control_device_object_if"></span><span id="DDK_CREATING_THE_CONTROL_DEVICE_OBJECT_IF"></span>


文件系统筛选器驱动程序的[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程通常会开始通过创建*控制设备对象*。 控制设备对象的用途是允许应用程序直接与通信筛选器驱动程序，即使之前筛选器附加到文件系统卷或卷设备对象。

请注意，文件系统也创建控件的设备对象。 当文件系统筛选器驱动程序将自身附加到文件系统中，而不是单独的文件系统卷时，它会通过将其附加到文件系统控制设备对象。

以下示例创建一个控制设备对象：

```cpp
RtlInitUnicodeString(&nameString, MYLEGACYFILTER_FULLDEVICE_NAME);
status = IoCreateDevice(
        DriverObject,                  //DriverObject
        0,                             //DeviceExtensionSize
        &nameString,                   //DeviceName
        FILE_DEVICE_DISK_FILE_SYSTEM,  //DeviceType
        FILE_DEVICE_SECURE_OPEN,       //DeviceCharacteristics
        FALSE,                         //Exclusive
        &gControlDeviceObject);        //DeviceObject

RtlInitUnicodeString(&linkString, MYLEGACYFILTER_DOSDEVICE_NAME);
status = IoCreateSymbolicLink(&linkString, &nameString);
```

与文件系统不同的文件系统筛选器驱动程序不需要命名其控制的设备对象。 在用户模式应用程序可以访问自调用筛选器驱动程序与设备名称[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)不能用于控制设备对象。 如果将非**NULL**传入值*DeviceName*参数，此值将成为控制设备对象的名称。 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)然后可以调用例程[ **IoCreateSymbolicLink** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesymboliclink)例程，如链接中前面的代码示例所示为对应用程序可见的用户模式名称的对象的内核模式名称。

**请注意**  控制设备对象是可以安全地命名的设备对象的唯一类型，因为它未附加到驱动程序堆栈的唯一设备对象。 因此，可以根据需要命名控件设备对象的文件系统筛选器驱动程序。 请注意，必须命名为文件系统的控制设备对象。 筛选设备对象应永远不会命名为。

 

分配给的值*DeviceType*参数应为 ntifs.h，如文件中定义的设备类型之一\_设备\_磁盘\_文件\_系统。

如果将非**NULL**传入值*DeviceName*参数， *DeviceCharacteristics*标志必须包括文件\_设备\_安全\_打开。 此标志指示要执行安全检查所有打开的请求发送到控件设备对象上的 I/O 管理器。 针对指定的设备对象的 ACL 进行这些安全检查。

文件系统筛选器驱动程序以确定调度例程中的其自己控制设备对象的有效方法是将设备指针和指向控制设备对象的以前存储全局指针进行比较。 因此，前面的示例将存储*DeviceObject*返回的指针[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)到`gControlDeviceObject`，全局定义的指针变量。

 

 




