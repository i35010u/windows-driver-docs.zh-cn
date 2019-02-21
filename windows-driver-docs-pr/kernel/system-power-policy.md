---
title: 系统电源策略
description: 系统电源策略
ms.assetid: 98b1a777-3ac1-40c2-a902-cb5326c20621
keywords:
- 整个系统电源策略 WDK 内核
- 电源策略 WDK 内核
- 电源供应 WDK 内核
- 系统电源策略 WDK 内核
- AC 电源 WDK 内核
- DC 电源 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a722ef366095010410ad23ab2ab648776d594ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554221"
---
# <a name="system-power-policy"></a>系统电源策略





在系统电源策略管理器作为其角色时，电源管理器将跟踪的系统活动、 确定相应的系统电源状态，以及发送[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求来查询或更改系统电源状态。 它还提供了的接口，通过该应用程序可以读取和写入电源策略设置 （请参阅 Microsoft Windows SDK）。

电源管理器维护两个独立的电源策略 — 一个用于交流 （墙上当前），一个 dc （电池或 UPS） — 并且这两种策略，具体取决于当前的电源之间自动切换。 通常情况下，AC 电源策略着重于性能通过节省，而对性能的 DC 电源策略强调节省。 若要了解系统到另一个策略从更改时，驱动程序可以注册通知系统的与\\回调\\PowerState 回调对象。 有关详细信息，请参阅[ **ExCreateCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff544560)并[回调对象](callback-objects.md)。

自动符合 APCI 规范的计算机从 AC 切换到电池电量，并从到另一个电池，为每个此类电源源脱机。 如果计算机硬件允许操作系统选择电源，电源管理器跟踪哪些电池至少充电但仍然正常工作，以及选择它以打开计算机电源。

只要交流电源可用时，计算机硬件也会自动启动，电池充电。 如果硬件允许操作系统选择要计费的电池，电源管理器将选择为要重新充电; 至少电量耗尽的电池这会增加，系统将在所有时间都至少一个良好充电的电池的可能性。

而不考虑任何其他设置，电源管理器执行电池电量严重短缺的 DC 电源策略如果电池充电或提供系统电源的报告"严重"的硬件条件，并且两秒或更长时间处于 discharging 状态。 在此情况下的电源策略通常需要转换为休眠或关机状态。

 

 




