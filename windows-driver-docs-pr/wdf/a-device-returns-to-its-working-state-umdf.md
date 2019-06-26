---
title: 设备回到工作状态
description: 设备回到工作状态
ms.assetid: 2b192eea-f731-4d61-be19-95724bf7b04a
keywords:
- 电源管理方案 WDK UMDF，返回到其工作状态的设备
- 返回到工作状态的情况 WDK UMDF 的设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4632df1c4725dc0888ea611187bc2bd5ca0723a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385336"
---
# <a name="a-device-returns-to-its-working-state"></a>设备回到工作状态


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果发生下列其中一项处于低功耗状态的设备将恢复工作状态：

-   设备检测到的外部事件，并触发其总线上的唤醒信号。 内核模式总线驱动程序检测到唤醒信号。

-   设备处于空闲状态，并将驱动程序调用[ **IWDFDevice2::StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)。

-   系统的电源状态已从低功耗状态更改为其工作 (S0) 状态。

在每种情况下，内核模式总线驱动程序将设备 （在总线的子设备） 还原到其工作 (D0) 状态。

对于每个基于 UMDF 的函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，使用驱动程序的最低驱动程序堆栈中启动一个时，驱动程序：

1.  框架将调用的驱动程序[ **IPnpCallback::OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)回调函数 （如果存在）。

2.  如果该驱动程序是设备的电源策略所有者，框架将调用其[ **IPowerPolicyCallbackWakeFromS0::OnDisarmWakeFromS0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0)或[ **IPowerPolicyCallbackWakeFromSx::OnDisarmWakeFromSx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-ondisarmwakefromsx)回调函数。

3.  Framework 重新启动所有的设备的电源管理的 I/O 队列并调用其[ **IQueueCallbackIoResume::OnIoResume** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackioresume-onioresume)回调函数 （如有必要）。

4.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediorestart)回调函数。

若要查看图显示了这些步骤，请参阅[设备中的用户插入](a-user-plugs-in-a-device.md)。

 

 





