---
title: 静态枚举
description: 静态枚举
keywords:
- 静态枚举 WDK KMDF
- 静态子列表 WDK KMDF
- 遍历静态子列表 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 824c1e031db443cd6b91748b715eeb5ac926066c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821121"
---
# <a name="static-enumeration"></a>静态枚举


*静态枚举* 是驱动程序在系统初始化期间检测和报告设备是否存在的功能，它具有对系统配置的后续更改的有限功能。

如果设备或功能子单元连接的数量和类型是预先确定的并且是永久性的，并且不依赖于运行驱动程序的系统的配置，则总线驱动程序可以使用静态枚举。

例如，声卡的驱动程序可以充当总线驱动程序，并为每个卡的功能（如 MIDI、音频和操纵杆） (PDOs) 创建单独的物理设备对象。

### <a name="static-child-lists"></a>静态子列表

使用该框架，驱动程序可通过提供静态子列表来支持静态枚举。 每个静态子列表表示连接到父设备的子设备的列表。 父设备的总线驱动程序必须标识父设备的子设备，将其添加到父设备的静态子列表，并为每个子设备创建一个 PDO。

### <a name="creating-a-static-child-list"></a>创建静态子列表

每当驱动程序创建一个框架设备对象（该对象表示设备 (FDO) 的功能设备对象）时，框架都会为该设备创建一个空的静态子列表。

当框架调用总线驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数时，回调函数必须调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 来为父设备创建 FDO。 有关创建 FDO 的详细信息，请参阅 [在函数驱动程序中创建设备对象](creating-device-objects-in-a-function-driver.md)。

然后，该驱动程序必须枚举父设备的子节点，为子级创建 PDOs，并将该子项添加到子列表中。

或者，驱动程序可以调用 [**WdfDeviceSetBusInformationForChildren**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetbusinformationforchildren) 来向框架提供有关总线的信息。 建议这样做，因为这样可以更轻松地让子设备和应用识别总线。

若要为检测到的子设备创建 PDO，总线驱动程序必须：

1.  调用 [**WdfPdoInitAllocate**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate) 以获取 [**WDFDEVICE \_ INIT**](./wdfdevice_init.md) 结构。

2.  初始化 WDFDEVICE \_ INIT 结构。

3.  调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 创建表示 PDO 的框架设备对象。

有关创建 PDO 的详细信息，请参阅 [在总线驱动程序中创建设备对象](creating-device-objects-in-a-bus-driver.md)。

调用 **WdfDeviceCreate** 之后，驱动程序必须调用 [**WdfFdoAddStaticChild**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoaddstaticchild) ，将子设备添加到子列表中。

### <a name="modifying-a-static-child-list"></a>修改静态子列表

由于驱动程序只应为预先确定和永久的设备配置使用静态子列表，因此，在创建静态子列表后，不需要驱动程序修改它。 如果驱动程序确定子设备不可访问，则驱动程序可以调用 [**WdfPdoMarkMissing**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdomarkmissing)。  (如果子设备仍可访问，但不响应且不可用，则驱动程序应将 [**WDF \_ 设备 \_ 状态**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_state)结构的 **失败** 成员设置为 **WdfTrue** ，然后调用 [**WdfDeviceSetDeviceState**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)。 ) 

### <a name="traversing-a-static-child-list"></a>遍历静态子列表

如果需要检索静态子列表的内容，则驱动程序可以通过执行以下操作遍历该列表：

1.  调用 [**WdfFdoLockStaticChildListForIteration**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdolockstaticchildlistforiteration)。

2.  根据需要调用 [**WdfFdoRetrieveNextStaticChild**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoretrievenextstaticchild) 多次。

3.  调用 [**WdfFdoUnlockStaticChildListFromIteration**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdounlockstaticchildlistfromiteration)。

 

