---
title: 支持特殊文件
description: 支持特殊文件
ms.assetid: 350e715f-be36-4999-99a2-6175d9763b3f
keywords:
- 特殊文件 WDK KMDF
- 分页文件 WDK KMDF
- 转储文件 WDK KMDF
- 休眠文件 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30c1be82ea7ff5bdf2cf6d11df75bf9328ec3e9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368047"
---
# <a name="supporting-special-files"></a>支持特殊文件


*特殊文件*包括分页文件、 转储文件和休眠文件。 如果您的驱动程序的目标设备，则系统可能会使用这些文件的存储设备驱动程序必须执行以下操作：

-   调用[ **WdfDeviceSetSpecialFileSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)启用或禁用对每种类型的特殊文件的支持。 （每个驱动程序支持特殊文件禁用默认情况下。）

    总线驱动程序的[枚举子设备](enumerating-the-devices-on-a-bus.md)还应调用[ **WdfDeviceSetSpecialFileSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)每个子设备可以支持特殊文件。

-   调用[ **WdfDeviceAddDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)、 支持特殊文件时，如果一台设备依赖于另一台设备。

-   （可选） 提供[ *EvtDeviceUsageNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification) （从 KMDF 1.11） 或[ *EvtDeviceUsageNotificationEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification_ex)回调函数，以便创建或删除特殊文件时，将通知该驱动程序。

如果您的驱动程序调用[ **WdfDeviceSetSpecialFileSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)对于设备，并且如果在设备上打开的特殊文件，该框架不允许即插即用管理器中删除或停用设备。

驱动程序已调用后[ **WdfDeviceAddDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)，它可以调用[ **WdfDeviceRemoveDependentUsageDeviceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceremovedependentusagedeviceobject)若要删除对另一台设备的设备的依赖关系。

 

 





