---
title: 在电池微型类驱动程序中创建 FDO
description: 在电池微型类驱动程序中创建 FDO
keywords:
- 电池 miniclass 驱动程序 WDK，FDOs
- FDOs WDK 电池
- 功能设备对象 WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bdea66fac9c2c1022d8571f5cb9b641832cb300
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784353"
---
# <a name="creating-an-fdo-in-the-battery-miniclass-driver"></a>在电池微型类驱动程序中创建 FDO


## <span id="ddk_creating_an_fdo_in_the_battery_miniclass_driver_dg"></span><span id="DDK_CREATING_AN_FDO_IN_THE_BATTERY_MINICLASS_DRIVER_DG"></span>


Miniclass 驱动程序应创建 FDO 并将其附加到设备的设备堆栈，如下所示：

1.  调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 为当前设备创建 FDO，如下所示：

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

    [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)的输入参数是指向传递到 *AddDevice* 例程的驱动程序对象、设备扩展的大小、NULL 代替设备名称以及系统定义的设备类型 (文件 \_ 设备 \_ 电池) 的指针。 电池 miniclass 驱动程序可以将 *DeviceCharacteristics* 参数指定为零，这与这些驱动程序无关。 多个线程可以向电池发送 i/o 请求，因此 miniclass 驱动程序将 FALSE 作为 *独占* 参数传递。 **IoCreateDevice** 返回指向所创建的 FDO 的指针。

2.  在返回的 FDO 中，设置标志和堆栈大小。 例如：

    ```cpp
    Fdo->Flags |= DO_BUFFERED_IO;
    Fdo->Flags |= DO_POWER_PAGABLE;
    Fdo->StackSize = Pdo->StackSize + 2;
    ```

    设置 " \_ 缓冲 \_ IO" 标记允许 miniclass 驱动程序对 irp 使用缓冲 i/o。 设置 DO \_ POWER \_ PAGABLE 标志指示该驱动程序是可分页的，并阻止它获取 IRQL &gt; = 调度级别的电源 irp \_ 。 最后，由于电池 Irp 需要额外的堆栈位置，miniclass 驱动程序应将 **StackSize** 设置为 PDO 堆栈大小加2，以便驱动程序可以将 IRP 向下传递到 pdo。

3.  将指针存储到设备的 PDO 上，指向 FDO 的指针、设备类型、设备名称，以及设备扩展中的任何其他必需状态。 例如：

    ```cpp
    NewBatt = (PNEW_BATT) Fdo->DeviceExtension;
    NewBatt->Type = NEW_BATTERY_TYPE;
    NewBatt->Fdo = Fdo;
    NewBatt->Pdo = Pdo;
    NewBatt->IsCacheValid = FALSE;
    ```

    该示例将指向 FDO 和 PDO 的指针存储在设备扩展中。  (PnP 管理器提供了一个指向 PDO 的指针作为 *AddDevice* 的 *PhysicalDeviceObject* 指针输入。 ) 另外，上面的示例将跟踪其自己的电池类型 (新 \_ 电池 \_ 类型，在此假设 miniclass 驱动程序) 中的其他位置定义，以及任何缓存信息是否有效。

    你确定设备扩展中存储的信息。 例如，智能电池驱动程序可能会保留电池的数量、指示电池选择器是否存在的布尔值，以及有关电池选择器的信息（可选）。

4.  调用 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) ，将 FDO 附加到设备堆栈，然后存储返回的指针，如下所示：

    ```cpp
    NewBatt->LowerDO = IoAttachDeviceToDeviceStack(Fdo,Pdo);
    ```

    调用将返回一个指向下一个较低设备对象的指针，此示例将此对象存储在设备扩展中。

5.  清除 FDO 中的 "执行 \_ 设备 \_ 初始化" 标志，如下所示：

    ```cpp
    Fdo->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

    清除 "对设备进行初始化" 标志后，就可以在 \_ \_ 设备堆栈中的组件之后打开设备对象。

 

