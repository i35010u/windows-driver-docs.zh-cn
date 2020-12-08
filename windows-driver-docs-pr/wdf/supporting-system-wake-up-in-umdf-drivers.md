---
title: 在 UMDF 驱动程序中支持系统唤醒
description: 在 UMDF 驱动程序中支持系统唤醒
keywords:
- 电源管理 WDK UMDF，系统唤醒
- 系统唤醒 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bec0bd278c7cee68c5ea9ac6669f4e953ee5cc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815577"
---
# <a name="supporting-system-wake-up-in-umdf-drivers"></a>在 UMDF 驱动程序中支持系统唤醒


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当系统处于低功耗状态时，某些设备可以检测到外部事件，例如传入网络数据包，并唤醒系统。 例如，如果 PCI 设备具有系统唤醒功能，如设备的电源管理功能 (PMC) 寄存器中所示，则会通过在 PCI 总线上的 PME) 信号 (PME 发出电源管理事件来唤醒系统。

如果设备可以将系统从系统范围内的低功耗状态唤醒，则 [电源策略所有者](power-policy-ownership-in-umdf.md)中的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数必须执行以下两个步骤：

1.  调用 [**IWDFDevice2：： AssignSxWakeSettings**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings) 以指定：
    -   设备将进入的低功耗状态
    -   用户是否可以控制设备的空闲设置
    -   设备的唤醒功能是已启用还是已禁用

2.  如果你的设备需要，可以实现 [IPowerPolicyCallbackWakeFromSx](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx) 接口和以下事件回调函数：
    -   [**IPowerPolicyCallbackWakeFromSx：： OnArmWakeFromSx**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onarmwakefromsx)，可让设备硬件响应外部唤醒事件。
    -   [**IPowerPolicyCallbackWakeFromSx：： OnDisarmWakeFromSx**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-ondisarmwakefromsx)，它禁止设备响应外部唤醒事件。
    -   [**IPowerPolicyCallbackWakeFromSx：： OnWakeFromSxTriggered**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onwakefromsxtriggered)，它通知驱动程序总线检测到唤醒信号。

总线驱动程序还参与了对系统的唤醒。 设备总线的内核模式驱动程序执行总线适配器上的任何必要功能，以启用和禁用设备从低功耗状态唤醒的能力。

有关控制设备的唤醒功能的注册表项的信息，请参阅 [在 UMDF 中控制设备空闲和唤醒行为的用户](user-control-of-device-idle-and-wake-behavior-in-umdf.md)。

 

