---
title: 设备进入低功耗状态
description: 设备进入低功耗状态
ms.assetid: c3697272-75ec-4de5-b123-3d1c68d2044e
keywords:
- 电源管理方案 WDK UMDF，进入低功耗状态
- 低功耗状态方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 393aed47b83ff5689122eb47125c8bab84b4746c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210883"
---
# <a name="a-device-enters-a-low-power-state"></a>设备进入低功耗状态


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果发生以下情况之一，则设备将保持其工作（D0）状态并进入低功耗状态：

-   设备处于空闲状态（即，未被访问），并且能够进入低功耗空闲状态，同时系统仍处于正常工作（S0）状态。

-   系统的电源状态已从其工作（S0）状态更改为低功耗状态。 （驱动程序可以调用[**IWDFDevice2：： GetSystemPowerAction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-getsystempoweraction)来确定系统电源状态发生变化的原因。）

对于支持设备的每个基于 UMDF 的函数和筛选器驱动程序，框架按顺序执行以下操作，一次使用驱动程序堆栈最高的驱动程序：

1.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[**IPnpCallbackSelfManagedIo：： OnSelfManagedIoSuspend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediosuspend)回调函数。

2.  框架停止所有设备的电源托管 i/o 队列，并调用其[**IPnpCallbackSelfManagedIo：： OnSelfManagedIoStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediostop)回调函数（如果存在）。

3.  如果驱动程序是设备的电源策略所有者，则框架将调用其[**IPowerPolicyCallbackWakeFromS0：： OnArmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onarmwakefroms0)或[**IPowerPolicyCallbackWakeFromSx：： OnArmWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onarmwakefromsx)回调函数。

4.  框架调用驱动程序的[**IPnpCallback：： OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)回调函数（如果存在）。

若要查看显示这些步骤的关系图，请参阅[断开 a 设备中用户](a-user-unplugs-a-device.md)的有序删除图形。

 

 





