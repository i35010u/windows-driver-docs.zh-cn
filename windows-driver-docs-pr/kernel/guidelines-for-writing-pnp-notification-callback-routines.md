---
title: 有关编写 PnP 通知回调例程的指导原则
description: 有关编写 PnP 通知回调例程的指导原则
ms.assetid: 2153b4c2-f60f-4ac9-8eee-66c5f3a9f414
keywords:
- 通知 WDK 即插即用，回调例程
- 回调例程 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5039783581195c83de12d581933407409743e9b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387014"
---
# <a name="guidelines-for-writing-pnp-notification-callback-routines"></a>有关编写 PnP 通知回调例程的指导原则





PnP 管理器调用通知回调例程在 IRQL = 被动\_级别。

若要确保的即插即用的子系统的顺利操作，即插即用通知回调例程必须遵循以下准则：

1.  不能阻止通知回调例程。

2.  通知回调例程不得调用，或导致对，同步生成即插即用事件的例程或阻止等待设备安装或删除的任何例程的调用。

    通知回调期间调用此类例程可使系统死锁。

    例如，驱动程序必须调用[ **IoReportTargetDeviceChange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreporttargetdevicechange)通知的回调例程中。 调用[ **IoReportTargetDeviceChangeAsynchronous** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreporttargetdevicechangeasynchronous)相反。

3.  通知回调例程应返回成功，它不会显式失败的任何事件。

    当驱动程序注册通知的事件类别时，即插即用管理器会通知中该类别中，现在和将来的所有事件的驱动程序。 如果驱动程序返回错误状态的事件不处理，错误地失败新查询事件的驱动程序风险。

    驱动程序正确返回了错误状态时，例如，驱动程序失败的查询通知，以便禁止该事件的建议。

4.  通知回调例程应分页的代码。

 

 




