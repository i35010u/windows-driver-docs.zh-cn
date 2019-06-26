---
title: 静态枚举
description: 静态枚举
ms.assetid: 58377f17-a9dc-4096-af23-36f8d8dbb87e
keywords:
- 静态枚举 WDK KMDF
- 静态子列出 WDK KMDF
- 遍历静态子列出 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d865a356980ffff0e903109c4c5678ec047f4005
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385955"
---
# <a name="static-enumeration"></a>静态枚举


*静态枚举*是检测和报告对系统的配置的后续更改的能力有限的报告在系统初始化过程中是否存在的设备驱动程序的能力。

如果的数量和类型的设备或功能的子单元连接的预设的且永久性的并且不依赖于系统驱动程序正在其运行的配置，总线驱动程序可以使用静态的枚举。

例如，声卡的驱动程序可能会充当总线驱动程序，并为每个卡的功能，例如 MIDI，音频和游戏杆创建单独的物理设备对象 (PDOs)。

### <a name="static-child-lists"></a>静态子列表

该框架支持驱动程序以支持静态枚举提供静态子列表。 每个静态子列表表示子设备连接到父设备的列表。 父设备的总线驱动程序必须标识父级的子设备、 将它们添加到父设备的静态子列表中，并创建为每个子设备 PDO。

### <a name="creating-a-static-child-list"></a>创建静态子列表

驱动程序创建一个表示设备的功能的设备对象 (FDO) 的框架设备对象每次在 framework 创建的空的静态子列表的设备。

当框架将调用总线驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数，必须调用的回调函数[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建父设备 FDO。 有关创建 FDO 的详细信息，请参阅[功能驱动程序中创建设备对象](creating-device-objects-in-a-function-driver.md)。

该驱动程序必须枚举父设备的子级、 创建的子元素，PDOs 和将子项添加到子列表。

（可选） 该驱动程序可以调用[ **WdfDeviceSetBusInformationForChildren** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetbusinformationforchildren)框架向提供关于总线的信息。 建议执行此操作，因为这样可以更轻松子设备和应用来标识在总线。

若要创建检测到的子设备 PDO，总线驱动程序必须：

1.  调用[ **WdfPdoInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)若要获取[ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构。

2.  初始化 WDFDEVICE\_INIT 结构。

3.  调用[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建一个表示 PDO framework 设备对象。

有关创建 PDO 的详细信息，请参阅[总线驱动程序中创建设备对象](creating-device-objects-in-a-bus-driver.md)。

在调用**WdfDeviceCreate**，该驱动程序必须调用[ **WdfFdoAddStaticChild** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoaddstaticchild)将子设备添加到子列表。

### <a name="modifying-a-static-child-list"></a>修改静态子列表

驱动程序只应是预先确定和永久的设备配置为使用静态子列表，因为很少需要驱动程序来创建它后修改静态子列表。 如果该驱动程序确定子设备变得不可访问，该驱动程序可以调用[ **WdfPdoMarkMissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdomarkmissing)。 (如果子设备仍然可以访问但变得无响应且不可用，驱动程序应设置**失败**的成员[ **WDF\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_state)结构**WdfTrue** ，然后调用[ **WdfDeviceSetDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)。)

### <a name="traversing-a-static-child-list"></a>遍历静态子列表

如果需要检索静态子列表的内容，该驱动程序可以通过执行以下遍历列表：

1.  调用[ **WdfFdoLockStaticChildListForIteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdolockstaticchildlistforiteration)。

2.  调用[ **WdfFdoRetrieveNextStaticChild** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoretrievenextstaticchild)根据需要多次。

3.  调用[ **WdfFdoUnlockStaticChildListFromIteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdounlockstaticchildlistfromiteration)。

 

 





