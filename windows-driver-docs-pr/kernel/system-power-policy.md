---
title: 系统电源策略
description: 系统电源策略
keywords:
- 系统范围电源策略 WDK 内核
- 电源策略 WDK 内核
- 电源 WDK 内核
- 系统电源策略 WDK 内核
- AC 电源 WDK 内核
- DC power WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cf6951d81d626413a3f3c24520880a445f0a171
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839227"
---
# <a name="system-power-policy"></a>系统电源策略





作为系统电源策略管理器的角色，电源管理器会跟踪系统活动，确定相应的系统电源状态，并发送 [**IRP \_ MJ \_ power**](./irp-mj-power.md) 请求来查询或更改系统电源状态。 它还提供了一些接口，应用程序通过这些接口可以读取和写入电源策略设置 (查看 Microsoft Windows SDK) 。

Power manager 维护两个单独的电源策略-一种用于 AC (墙电流) ，一个用于 DC (电池或 UPS) ，根据当前电源自动切换这两个策略。 通常情况下，AC 电源策略会对性能进行强调，而 DC 电源策略则强调节省了性能。 若要查明系统何时从一种策略更改为另一种策略，驱动程序可以使用系统的 \\ 回调 \\ PowerState 回调对象注册通知。 有关详细信息，请参阅 [**ExCreateCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback) 和 [回叫对象](callback-objects.md)。

符合 APCI 规范的计算机会自动从 AC 切换到电池电源，并从一个电池切换到另一个电池，因为每个此类电源都处于离线状态。 如果计算机硬件允许操作系统选择电源，则电源管理器会跟踪哪个电池电量最少，但仍可正常运行，并选择它以接通计算机电源。

一旦 AC 电源变为可用，计算机硬件就会自动开始为电池充电。 如果硬件允许操作系统选择要收取的电池电量，则电源管理器将选择电量最少的充电电量;这会增加系统在所有时间都至少具有一个充足收费的电池的机会。

无论使用何种其他设置，如果充电或提供系统电源的电池报告硬件状况为 "严重"，并且处于正在放电状态的两秒钟或更长时间，则 power manager 会将 DC 电源策略用于严重电池。 在这种情况下，电源策略通常需要过渡到休眠或关闭状态。

 

