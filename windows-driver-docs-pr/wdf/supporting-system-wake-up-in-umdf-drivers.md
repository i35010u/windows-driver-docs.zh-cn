---
title: 在 UMDF 驱动程序中支持系统唤醒
description: 在 UMDF 驱动程序中支持系统唤醒
ms.assetid: 945b1751-f3a1-4a29-8fb7-6690f91af7d9
keywords:
- 电源管理 WDK UMDF 系统唤醒
- 系统唤醒 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fe488171296241e1cf0134cb04745de4c312dc3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368027"
---
# <a name="supporting-system-wake-up-in-umdf-drivers"></a>在 UMDF 驱动程序中支持系统唤醒


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

低功耗状态系统时，某些设备可以检测外部事件，例如传入的网络数据包，并将系统然后唤醒。 例如，如果 PCI 设备具有系统唤醒功能，则设备电源管理功能 (PMC) 注册中所示，它通过引发 PCI 总线上的电源管理事件 (PME) 信号唤醒系统。

如果你的设备可以从系统范围内低功耗状态，将系统唤醒[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)中的回调函数[电源策略所有者](power-policy-ownership-in-umdf.md)必须执行以下两个步骤：

1.  调用[ **IWDFDevice2::AssignSxWakeSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)指定：
    -   设备将进入低功耗状态
    -   用户是否可以控制设备的空闲状态设置
    -   设备的唤醒功能是启用还是禁用

2.  实现[IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)接口和以下事件回调函数，如果需要为你的设备：
    -   [**IPowerPolicyCallbackWakeFromSx::OnArmWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onarmwakefromsx)，它实现了设备硬件对外部唤醒事件作出响应。
    -   [**IPowerPolicyCallbackWakeFromSx::OnDisarmWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-ondisarmwakefromsx)，它表示禁用设备的外部唤醒事件响应的能力。
    -   [**IPowerPolicyCallbackWakeFromSx::OnWakeFromSxTriggered**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onwakefromsxtriggered)，它告诉总线检测到唤醒信号驱动程序。

总线驱动程序还参与唤醒系统。 设备的总线的内核模式驱动程序采取任何必要上启用和禁用设备的功能，可以从低功耗状态唤醒的总线适配器。

控制设备的唤醒功能的注册表项的信息，请参阅[用户控件的设备闲置，在 UMDF 唤醒行为](user-control-of-device-idle-and-wake-behavior-in-umdf.md)。

 

 





