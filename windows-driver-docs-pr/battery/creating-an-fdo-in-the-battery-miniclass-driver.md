---
title: 在电池微型类驱动程序中创建 FDO
description: 在电池微型类驱动程序中创建 FDO
ms.assetid: 3178710b-8e4a-4f9c-893b-1d06c4a3f7ff
keywords:
- 电池 miniclass 驱动程序 WDK FDOs
- FDOs WDK 电池
- 功能的设备对象 WDK 电池电量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a77a79e746d437e1731c4114e0c61fa50c65582
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364757"
---
# <a name="creating-an-fdo-in-the-battery-miniclass-driver"></a>在电池微型类驱动程序中创建 FDO


## <span id="ddk_creating_an_fdo_in_the_battery_miniclass_driver_dg"></span><span id="DDK_CREATING_AN_FDO_IN_THE_BATTERY_MINICLASS_DRIVER_DG"></span>


Miniclass 驱动程序应创建 FDO 并将其附加到该设备，设备堆栈，如下所示：

1.  调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)创建 FDO 对于当前的设备，请按如下所示：

    ```cpp
    Status = IoCreateDevice(
             DriverObject,
             sizeof (DeviceExtension),
             NULL,
             FILE_DEVICE_BATTERY,
             0,
             FALSE,
             &Fdo
             );
    ```

    输入的参数[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)是指向传递给驱动程序对象的指针*AddDevice*例程时，设备扩展，NULL 代替的大小设备名称和系统定义的设备类型 (文件\_设备\_电池)。 电池 miniclass 驱动程序可以指定为零*DeviceCharacteristics*参数，这些驱动程序无关。 因此 miniclass 驱动程序将 FALSE 传递多个线程可以将 I/O 请求发送到电池，作为*独占*参数。 **IoCreateDevice**创建 FDO 返回的指针。

2.  在返回 FDO，设置标志和堆栈大小。 例如：

    ```cpp
    Fdo->Flags |= DO_BUFFERED_IO;
    Fdo->Flags |= DO_POWER_PAGABLE;
    Fdo->StackSize = Pdo->StackSize + 2;
    ```

    设置是否\_缓冲\_IO 标志允许 miniclass 驱动程序的 Irp 使用缓冲的 I/O。 设置是否\_电源\_PAGABLE 标志指示驱动程序是可分页，使其无法获得 IRQL power Irp &gt;= 调度\_级别。 最后，由于电池 Irp 需要附加的堆栈位置，miniclass 驱动程序应设置**StackSize**到 PDO 堆栈大小加上两个，这样该驱动程序可以将传递到 PDO IRP。

3.  将设备的 PDO，FDO、 设备类型、 设备名称和任何其他必要的状态的指针指向存储在设备扩展。 例如：

    ```cpp
    NewBatt = (PNEW_BATT) Fdo->DeviceExtension;
    NewBatt->Type = NEW_BATTERY_TYPE;
    NewBatt->Fdo = Fdo;
    NewBatt->Pdo = Pdo;
    NewBatt->IsCacheValid = FALSE;
    ```

    该示例将 FDO 和 PDO 指针存储在设备扩展。 (即插即用管理器提供一个指向作为 PDO *PhysicalDeviceObject*输入到指针*AddDevice*。)此外，上面的示例中跟踪的其自己的电池类型 (新建\_电池\_此假设 miniclass 驱动程序中其他位置定义的类型) 以及任何缓存的信息是否有效。

    确定存储在设备扩展的信息。 例如，智能电池驱动程序可能会保留数量的电池，布尔值，该值指示电池选择器是否存在，以及 （可选） 该电池选择器有关的信息。

4.  调用[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)将附加到设备堆栈 FDO，然后将存储返回的指针，如下所示：

    ```cpp
    NewBatt->LowerDO = IoAttachDeviceToDeviceStack(Fdo,Pdo);
    ```

    在调用返回一个指向此示例将存储在设备扩展中的下一步下一个设备对象。

5.  清除 DO\_设备\_初始化中 FDO 标志，如下所示：

    ```cpp
    Fdo->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

    清除 DO\_设备\_正在初始化标志允许设备对象随后打开的设备堆栈中的组件。

 

 




