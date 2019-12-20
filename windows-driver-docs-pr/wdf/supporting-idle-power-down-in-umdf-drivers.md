---
title: 在 UMDF 驱动程序中支持空闲时关闭电源
description: 在 UMDF 驱动程序中支持空闲时关闭电源
ms.assetid: 128f009e-1847-493e-90e3-2fe8c141b158
keywords:
- 电源管理 WDK UMDF，空闲关机
- 空闲的关闭 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e50c1eacf39891cf6607c8d360c8866dfabc4295
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210763"
---
# <a name="supporting-idle-power-down-in-umdf-drivers"></a>在 UMDF 驱动程序中支持空闲时关闭电源


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

某些设备可能进入睡眠状态，而系统仍处于正常工作状态。 对于此类设备，框架在设备处于空闲（未使用）状态的情况下启动降低设备的电量。

其中一些设备还可以在检测到外部事件时在总线上触发唤醒信号。 总线驱动程序会响应此信号，驱动程序堆栈会将设备还原到其工作状态。 （未检测到外部事件的设备仍处于低功耗状态，直到框架要求总线驱动程序启动将设备还原到其工作状态。）

如果设备处于空闲状态，则[电源策略所有者](power-policy-ownership-in-umdf.md)必须执行以下两个步骤：

1.  调用[**IWDFDevice2：： AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)或[**IWDFDevice3：： AssignS0IdleSettingsEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex)来指定：
    -   设备将进入的低功耗状态
    -   设备在电源状态降低之前必须保持空闲的时间量
    -   设备是否可以检测外部事件，并在总线上触发唤醒信号
    -   用户是否可以控制设备的空闲设置
    -   当空闲超时期限过期时，框架是否可以将设备置于 D3cold 电源状态

    如果驱动程序是用 framework 1.11 或更高版本生成的，则可以调用**IWDFDevice3：： AssignS0IdleSettingsEx**而不是**IWDFDevice2：： AssignS0IdleSettings**。 除了上述功能之外， **IWDFDevice3：： AssignS0IdleSettingsEx**还允许驱动程序指定：
    -   设备的空闲关机功能是已启用还是已禁用
    -   当系统恢复到工作（S0）状态时，设备是否将恢复为其工作（D0）状态

2.  如果你的设备需要，可以实现[IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)接口和以下事件回调函数：
    -   [**IPowerPolicyCallbackWakeFromS0：： OnArmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onarmwakefroms0)，它使设备硬件（而不是总线）能够响应外部唤醒事件。
    -   [**IPowerPolicyCallbackWakeFromS0：： OnDisarmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0)，它禁用设备的功能（而不是总线的能力）来响应外部唤醒事件。
    -   [**IPowerPolicyCallbackWakeFromS0：： OnWakeFromS0Triggered**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onwakefroms0triggered)，它通知驱动程序总线检测到唤醒信号。




当满足以下所有条件时，框架会将设备视为处于空闲状态，并开始计算空闲时间：

-   为此设备实例创建的任何电源管理队列都没有在队列中等待的任何请求，或已将其分派给驱动程序。 如果请求已分派给驱动程序，并且驱动程序将其发送到 i/o 目标，则请求仍与队列相关，并且不会将设备视为空闲。 非电源管理队列中的请求不会计入设备空闲。
-   如果驱动程序之前调用[**IWDFDevice2：： StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)，则驱动程序随后称为[**IWDFDevice2：： ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)。
-   如果电源策略所有者是总线驱动程序，则总线驱动程序的任何子设备都不是 D0。

如果你的驱动程序（或用户）对你的设备启用了空闲电源，则可能必须使用[**IWDFDevice2：： StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)方法。 如果设备处于工作（D0）状态，则此方法会阻止设备置于空闲状态，直到驱动程序调用[**IWDFDevice2：： ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)。 如果当驱动程序调用**IWDFDevice2：： StopIdle**时设备处于低功耗状态，并且系统处于正常工作（S0）状态，则框架将请求总线驱动程序将设备还原到其工作（D0）状态。 有关驱动程序何时需要调用**IWDFDevice2：： StopIdle**的详细信息，请参阅该方法的参考页。

如果设备可以从低功耗状态唤醒，则设备总线的驱动程序将参与唤醒设备。 内核模式总线驱动程序在总线适配器上执行任何必要的功能，以启用和禁用设备从低功耗状态唤醒的能力。

有关控制设备的空闲功能的注册表项的信息，请参阅[在 UMDF 中控制设备空闲和唤醒行为的用户](user-control-of-device-idle-and-wake-behavior-in-umdf.md)。

 

 





