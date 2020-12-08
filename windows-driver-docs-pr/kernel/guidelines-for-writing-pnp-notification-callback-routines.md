---
title: 有关编写 PnP 通知回调例程的指导原则
description: 有关编写 PnP 通知回调例程的指导原则
keywords:
- 通知 WDK PnP，回调例程
- 回调例程 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61bdcb7f03a0a18e2b71bf96d4cda89e068641f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792763"
---
# <a name="guidelines-for-writing-pnp-notification-callback-routines"></a>有关编写 PnP 通知回调例程的指导原则





PnP 管理器以 IRQL = 被动级别调用通知回调例程 \_ 。

若要确保 PnP 子系统的平稳运行，PnP 通知回调例程必须遵循以下准则：

1.  通知回调例程不能阻止。

2.  通知回调例程不得调用，或导致对生成 PnP 事件的同步例程或阻止等待设备安装或删除的任何例程的调用。

    在通知回调期间调用此类例程可能会导致系统死锁。

    例如，驱动程序不能在通知回调例程中调用 [**IoReportTargetDeviceChange**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechange) 。 改为调用 [**IoReportTargetDeviceChangeAsynchronous**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechangeasynchronous) 。

3.  对于未显式失败的任何事件，通知回调例程应返回 success。

    当驱动程序注册事件类别上的通知时，PnP 管理器会向驱动程序通知该类别中的所有事件，即 "存在" 和 "未来"。 如果驱动程序为它不处理的事件返回错误状态，则驱动程序的风险会因错误而失败。

    例如，如果驱动程序失败，则驱动程序将返回错误状态，以拒绝建议的事件。

4.  通知回调例程应为页面代码。

 

