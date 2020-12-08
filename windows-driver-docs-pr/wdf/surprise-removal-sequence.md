---
title: 意外删除顺序
description: 意外删除顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d6713265e01915d5e883310cedca58b2871168
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836585"
---
# <a name="surprise-removal-sequence"></a>意外删除顺序


如果用户在未发出警告的情况下删除设备，只需在不使用设备管理器或安全删除硬件实用程序的情况下将其删除，该设备将被视为 "意外删除"。 发生这种情况时，框架将遵循略微不同的删除顺序。 如果另一个驱动程序在设备上调用 [**IoInvalidateDeviceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate) ，则它还会跟随意外删除序列，即使设备仍在物理上存在也是如此。 在意外删除序列中，框架在调用删除序列中的任何其他回调之前调用 [*EvtDeviceSurpriseRemoval*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal) 回调。 序列完成后，框架会销毁设备对象。 所有可移动设备的驱动程序必须确保关机和启动路径中的回调都可以处理故障，尤其是因删除硬件而导致的失败。 任何访问硬件的尝试都不应无限期等待，但会受到超时或监视定时器的限制。

下图显示了意外删除中涉及的回调：

![意外删除序列](images/surprise-removal.png)

如果设备在被删除时未处于工作状态，则框架将在 [*EvtDeviceSurpriseRemoval*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)之后立即调用 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)事件回调。 它省略了在设备从工作状态退出时已执行的干预步骤。

 

