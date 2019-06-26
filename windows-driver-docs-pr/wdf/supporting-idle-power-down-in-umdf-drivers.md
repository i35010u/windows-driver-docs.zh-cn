---
title: 在 UMDF 驱动程序中支持空闲时关闭电源
description: 在 UMDF 驱动程序中支持空闲时关闭电源
ms.assetid: 128f009e-1847-493e-90e3-2fe8c141b158
keywords:
- 电源管理 WDK UMDF，空闲电源关闭
- 空闲关闭 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39b2273b11f713dd2d292aa2049d23455019ebab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368647"
---
# <a name="supporting-idle-power-down-in-umdf-drivers"></a>在 UMDF 驱动程序中支持空闲时关闭电源


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

某些设备可以进入休眠状态，而系统仍然处于其工作状态。 对于此类设备，框架将启动降低设备的电源后该设备处于空闲状态 （未使用） 预先确定的 （且可设置的） 的时间量。

检测到任何外部事件，这些设备的一些还可以触发总线上的唤醒信号。 总线驱动程序响应此信号，并驱动程序堆栈将设备还原到其工作状态。 （未检测到外部事件的设备仍保留在低功耗状态直到框架要求总线驱动程序以启动设备还原到其工作状态。）

如果你的设备时处于空闲状态，, 可以关闭电源[电源策略所有者](power-policy-ownership-in-umdf.md)必须执行以下两个步骤：

1.  调用[ **IWDFDevice2::AssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)或[ **IWDFDevice3::AssignS0IdleSettingsEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex)指定：
    -   设备将进入低功耗状态
    -   降低其电源状态前，设备必须保持空闲的时间量
    -   设备是否可以检测的外部事件，并触发总线上的唤醒信号
    -   用户是否可以控制设备的空闲状态设置
    -   是否框架可以将设备置于 D3cold 电源状态的空闲超时期限过期时

    如果您的驱动程序已使用版本 1.11 或更高版本的 framework 构建的则可以调用**IWDFDevice3::AssignS0IdleSettingsEx**而不是**IWDFDevice2::AssignS0IdleSettings**。 除了上述功能之外**IWDFDevice3::AssignS0IdleSettingsEx**允许驱动程序指定：
    -   设备的空闲关机功能是启用还是禁用
    -   是否设备系统返回到其工作 (S0) 状态时将返回到其工作 (D0) 状态

2.  实现[IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)接口和以下事件回调函数，如果需要为你的设备：
    -   [**IPowerPolicyCallbackWakeFromS0::OnArmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onarmwakefroms0)，可让设备硬件 （而不在总线），以响应外部的唤醒事件。
    -   [**IPowerPolicyCallbackWakeFromS0::OnDisarmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0)，它表示禁用外部唤醒事件响应设备的功能 （不在总线功能）。
    -   [**IPowerPolicyCallbackWakeFromS0::OnWakeFromS0Triggered**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onwakefroms0triggered)，它告诉总线检测到唤醒信号驱动程序。




框架认为设备不处于空闲状态，并开始计数空闲时间，当满足所有以下条件：

-   无此设备实例创建的电源管理队列已在队列中等待的任何请求或分派给该驱动程序。 如果请求被调度到驱动程序，该驱动程序将其发送到的 I/O 目标，请求仍与队列相关，并且设备将不被视为空闲。 非托管 power – 队列中的请求都不会计入设备空闲。
-   如果该驱动程序之前调用[ **IWDFDevice2::StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)，随后调用驱动程序，具有[ **IWDFDevice2::ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)。
-   如果电源策略所有者是总线驱动程序，没有任何子设备的总线驱动程序都在 D0。

如果您的驱动程序 （或用户） 启用空闲关闭设备，你可能必须使用[ **IWDFDevice2::StopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)方法。 如果设备在其工作 (D0) 状态，此方法将阻止设备驱动程序调用直到空闲[ **IWDFDevice2::ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)。 如果设备处于低功耗状态时，驱动程序调用**IWDFDevice2::StopIdle**，并且该框架的系统是在其工作 (S0) 状态，如果请求总线驱动程序，以将设备还原到其工作 (D0) 状态。 详细了解您的驱动程序可能需要调用**IWDFDevice2::StopIdle**，请参阅该方法的参考页。

如果设备可以唤醒本身从低功耗状态，为设备的总线驱动程序参与了唤醒设备。 内核模式总线驱动程序会执行任何所需在启用和禁用设备的功能，可以从低功耗状态唤醒的总线适配器上。

控制设备的空闲状态功能的注册表项的信息，请参阅[用户控件的设备空闲状态唤醒中和行为 UMDF](user-control-of-device-idle-and-wake-behavior-in-umdf.md)。

 

 





