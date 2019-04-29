---
title: 总线驱动程序的电源关闭和删除顺序
description: 总线驱动程序的电源关闭和删除顺序
ms.assetid: 71397945-D9DB-43E2-AE06-548684F72B63
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 078a45682635d4670782f75f57fca1b017388f6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390087"
---
# <a name="power-down-and-removal-sequence-for-a-bus-driver"></a>总线驱动程序的电源关闭和删除顺序


下图显示了当关闭框架调用 KMDF 总线驱动程序的事件回调函数的顺序和删除连接到该总线的设备。 在序列图顶部开头操作设备处于工作电源状态 (D0):

![总线驱动程序的电源关闭和删除序列](images/pdo-powerdown.png)

框架不会删除 PDO，直到从系统以物理方式删除该设备。 例如，如果用户禁用的设备在设备管理器或安全删除硬件实用程序中停止，但不会以物理方式删除设备，该框架将保留 PDO。 如果以后重新启用该设备，该框架使用相同的 PDO 和首先启动序列调用[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调，如中所示[强化序列物理设备对象](power-up-sequence-for-a-bus-driver.md)。

**注意**：通常情况下，框架将调用总线驱动程序[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数后它被称为[ *EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)函数的所有子设备的驱动程序枚举。  该框架可能会发生时遇到的设备通电或断电故障的父代、 调用驱动程序的[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)已调用之前[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)函数的所有子设备。  请考虑调用[WdfDeviceInitSetReleaseHardwareOrderOnFailure](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)若要确保框架调用总线驱动程序[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调仅后已删除所有子设备。



 





