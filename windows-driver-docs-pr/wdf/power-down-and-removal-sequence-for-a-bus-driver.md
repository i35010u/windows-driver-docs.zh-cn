---
title: 总线驱动程序的电源关闭和删除顺序
description: 总线驱动程序的电源关闭和删除顺序
ms.assetid: 71397945-D9DB-43E2-AE06-548684F72B63
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9b27e05cd85276eab3dc2b7fe0f30afa68fb2544
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190449"
---
# <a name="power-down-and-removal-sequence-for-a-bus-driver"></a>总线驱动程序的电源关闭和删除顺序


下图显示了在关闭和删除已连接到总线的设备时，框架调用 KMDF 总线驱动程序的事件回调函数的顺序。 序列从图形顶部开始，其操作设备处于工作电源状态 (D0) ：

![总线驱动程序的关机和删除序列](images/pdo-powerdown.png)

在物理上将设备从系统中删除之前，框架不会删除 PDO。 例如，如果用户设备管理器在 "安全删除硬件" 实用程序中禁用该设备，或在 "安全删除硬件" 实用程序中停止该设备，但并不实际删除该设备，则该框架将保留 PDO。 如果以后重新启用了设备，则该框架将使用同一 PDO，并通过调用 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调来启动启动序列，如 [物理设备对象的开机序列](power-up-sequence-for-a-bus-driver.md)中所示。

**注意**：通常，框架在为驱动程序枚举的所有子设备调用[*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)函数后，会调用总线驱动程序的[*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数。  如果父项出现设备断电或关机故障，则在为所有子设备调用[*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)函数之前，框架可能会调用驱动程序的[*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 。  请考虑调用 [WdfDeviceInitSetReleaseHardwareOrderOnFailure](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure) ，以确保框架仅在删除所有子设备后才调用总线驱动程序的 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调。



