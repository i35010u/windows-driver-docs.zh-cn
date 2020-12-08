---
title: '设备返回到其工作状态 (UMDF 1) '
description: 设备回到工作状态
keywords:
- 电源管理方案 WDK UMDF，设备返回到其工作状态
- 设备返回到工作状态方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81eedd61a1ed07b3b827af8f8da58c2ce27e0eb0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840473"
---
# <a name="a-device-returns-to-its-working-state-umdf-1"></a>设备返回到其工作状态 (UMDF 1) 


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果发生以下情况之一，则处于低功耗状态的设备将恢复为其工作状态：

-   设备检测到外部事件，并在其总线上触发唤醒信号。 内核模式总线驱动程序检测唤醒信号。

-   设备处于空闲状态，驱动程序调用 [**IWDFDevice2：： StopIdle**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)。

-   系统的电源状态已从低功耗状态更改为其工作 (S0) 状态。

在上述每种情况下，内核模式总线驱动程序都将设备 (总线的子设备恢复) 其工作 (D0) 状态。

对于支持设备的每个基于 UMDF 的函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈中最低的驱动程序开始：

1.  如果) 存在该驱动程序，则框架将调用该驱动程序的 [**IPnpCallback：： OnD0Entry**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) 回调函数 (。

2.  如果驱动程序是设备的电源策略所有者，则框架将调用其 [**IPowerPolicyCallbackWakeFromS0：： OnDisarmWakeFromS0**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0) 或 [**IPowerPolicyCallbackWakeFromSx：： OnDisarmWakeFromSx**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-ondisarmwakefromsx) 回调函数。

3.  框架将重新启动所有设备的电源托管 i/o 队列，并在) 必要时调用其 [**IQueueCallbackIoResume：： OnIoResume**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackioresume-onioresume) 回调函数 (。

4.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [**IPnpCallbackSelfManagedIo：： OnSelfManagedIoRestart**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediorestart) 回调函数。

若要查看显示这些步骤的关系图，请参阅 [用户插入设备](a-user-plugs-in-a-device.md)。

 

