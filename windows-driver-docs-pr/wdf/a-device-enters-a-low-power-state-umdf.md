---
title: 在设备进入低功耗状态
description: 在设备进入低功耗状态
ms.assetid: c3697272-75ec-4de5-b123-3d1c68d2044e
keywords:
- 电源管理方案 WDK UMDF，进入低功耗状态
- 低功耗状态方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e59be072171bff0ac111d6ca0c69d7a1bf776208
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545246"
---
# <a name="a-device-enters-a-low-power-state"></a>在设备进入低功耗状态


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

设备会使其工作 (D0) 状态，并进入低功耗状态，如果发生以下情况之一：

-   设备处于空闲状态 （的，没有访问） 并能够进入低能耗空闲状态，而系统仍然处于其工作 (S0) 状态。

-   系统的电源状态已从其工作 (S0) 状态更改为低功耗状态。 (驱动程序可以调用[ **IWDFDevice2::GetSystemPowerAction** ](https://msdn.microsoft.com/library/windows/hardware/ff556936)以确定系统的电源状态更改的原因。)

对于每个基于 UMDF 的函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，一个驱动程序时，开始驱动程序堆栈中最高的驱动程序：

1.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoSuspend** ](https://msdn.microsoft.com/library/windows/hardware/ff556790)回调函数。

2.  该框架将停止所有设备的电源管理的 I/O 队列并调用其[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoStop** ](https://msdn.microsoft.com/library/windows/hardware/ff556787)回调函数 （如果存在）。

3.  如果该驱动程序是设备的电源策略所有者，框架将调用其[ **IPowerPolicyCallbackWakeFromS0::OnArmWakeFromS0** ](https://msdn.microsoft.com/library/windows/hardware/ff556817)或[ **IPowerPolicyCallbackWakeFromSx::OnArmWakeFromSx** ](https://msdn.microsoft.com/library/windows/hardware/ff556826)回调函数。

4.  框架将调用的驱动程序[ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)回调函数 （如果存在）。

若要查看图显示了这些步骤，请参阅图有序地删除[用户断开设备](a-user-unplugs-a-device.md)。

 

 





