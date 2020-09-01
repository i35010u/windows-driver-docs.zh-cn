---
title: '设备进入低功耗状态 (UMDF 1) '
description: 设备进入低功耗状态
ms.assetid: c3697272-75ec-4de5-b123-3d1c68d2044e
keywords:
- 电源管理方案 WDK UMDF，进入低功耗状态
- 低功耗状态方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83f933733a842a26f74c4ee341b8dfbff8052d7f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190147"
---
# <a name="a-device-enters-a-low-power-state-umdf-1"></a>设备进入低功耗状态 (UMDF 1) 


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果发生以下情况之一，设备会将其工作 (D0) 状态，并进入低功耗状态：

-   设备处于空闲状态 (也就是说，没有) 访问它，并且能够进入低功耗空闲状态，而系统仍处于正常工作 (S0) 状态。

-   系统的电源状态已从其工作 (S0) 状态更改为低功耗状态。  (驱动程序可以调用 [**IWDFDevice2：： GetSystemPowerAction**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-getsystempoweraction) 来确定系统电源状态发生变化的原因。 ) 

对于支持设备的每个基于 UMDF 的函数和筛选器驱动程序，框架按顺序执行以下操作，一次使用驱动程序堆栈最高的驱动程序：

1.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [**IPnpCallbackSelfManagedIo：： OnSelfManagedIoSuspend**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediosuspend) 回调函数。

2.  框架停止所有设备的电源托管 i/o 队列，并调用其 [**IPnpCallbackSelfManagedIo：： OnSelfManagedIoStop**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediostop) 回调函数 (如果它们) 存在。

3.  如果驱动程序是设备的电源策略所有者，则框架将调用其 [**IPowerPolicyCallbackWakeFromS0：： OnArmWakeFromS0**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onarmwakefroms0) 或 [**IPowerPolicyCallbackWakeFromSx：： OnArmWakeFromSx**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onarmwakefromsx) 回调函数。

4.  如果) 存在该驱动程序，则框架将调用该驱动程序的 [**IPnpCallback：： OnD0Exit**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit) 回调函数 (。

若要查看显示这些步骤的关系图，请参阅 [断开 a 设备中用户](a-user-unplugs-a-device.md)的有序删除图形。

 

