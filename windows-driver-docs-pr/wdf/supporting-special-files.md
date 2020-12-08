---
title: 支持特殊文件
description: 支持特殊文件
keywords:
- 特殊文件 WDK KMDF
- 页面文件 WDK KMDF
- 转储文件 WDK KMDF
- 休眠文件 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d17465c91012e48f57c310311a8786f4da74aa2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815573"
---
# <a name="supporting-special-files"></a>支持特殊文件


*特殊文件* 包括页面文件、转储文件和休眠文件。 如果驱动程序的目标设备是系统可能用于这些文件的存储设备，则驱动程序必须执行以下操作：

-   调用 [**WdfDeviceSetSpecialFileSupport**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport) 为每种类型的特殊文件启用或禁用支持。 默认情况下，将禁用每个驱动程序对特殊文件的支持 (。 ) 

    [枚举子设备](enumerating-the-devices-on-a-bus.md)的总线驱动程序还应为每个可支持特殊文件的子设备调用 [**WdfDeviceSetSpecialFileSupport**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport) 。

-   如果一台设备在支持特殊文件时依赖于另一台设备，请调用 [**WdfDeviceAddDependentUsageDeviceObject**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)。

-   （可选）提供 [*EvtDeviceUsageNotification*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification) 或 (从 KMDF 1.11) [*EvtDeviceUsageNotificationEx*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification_ex) 回调函数开始，以便在创建或删除特殊文件时通知该驱动程序。

如果你的驱动程序为设备调用 [**WdfDeviceSetSpecialFileSupport**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport) ，并且在设备上打开了某个特殊文件，则该框架不允许 PnP 管理器删除或停止该设备。

驱动程序调用 [**WdfDeviceAddDependentUsageDeviceObject**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)后，可以调用 [**WdfDeviceRemoveDependentUsageDeviceObject**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceremovedependentusagedeviceobject) 来删除设备对另一台设备的依赖关系。

 

