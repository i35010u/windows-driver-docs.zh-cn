---
title: 系统电源策略
description: 系统电源策略
ms.assetid: 98b1a777-3ac1-40c2-a902-cb5326c20621
keywords:
- 系统范围电源策略 WDK 内核
- 电源策略 WDK 内核
- 电源 WDK 内核
- 系统电源策略 WDK 内核
- AC 电源 WDK 内核
- DC power WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8d9f89e29ed50f3fa1571e239fcd3c554af1246
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836136"
---
# <a name="system-power-policy"></a>系统电源策略





作为系统电源策略管理器的角色，电源管理器会跟踪系统活动，确定相应的系统电源状态，并将[**IRP\_MJ 发送\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) requests 来查询或更改系统电源状态。 它还提供了应用程序可用于读取和写入电源策略设置的接口（请参阅 Microsoft Windows SDK）。

Power manager 维护两个单独的电源策略-一个用于交流（墙电流），另一个用于 DC （电池或 UPS），并根据当前电源自动在这两个策略之间切换。 通常情况下，AC 电源策略会对性能进行强调，而 DC 电源策略则强调节省了性能。 若要查明系统何时从一种策略更改为另一种策略，驱动程序可以使用系统的 \\回调注册通知\\PowerState 回调对象。 有关详细信息，请参阅[**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)和[回叫对象](callback-objects.md)。

符合 APCI 规范的计算机会自动从 AC 切换到电池电源，并从一个电池切换到另一个电池，因为每个此类电源都处于离线状态。 如果计算机硬件允许操作系统选择电源，则电源管理器会跟踪哪个电池电量最少，但仍可正常运行，并选择它以接通计算机电源。

一旦 AC 电源变为可用，计算机硬件就会自动开始为电池充电。 如果硬件允许操作系统选择要收取的电池电量，则电源管理器将选择电量最少的充电电量;这会增加系统在所有时间都至少具有一个充足收费的电池的机会。

无论使用何种其他设置，如果充电或提供系统电源的电池报告硬件状况为 "严重"，并且处于正在放电状态的两秒钟或更长时间，则 power manager 会将 DC 电源策略用于严重电池。 在这种情况下，电源策略通常需要过渡到休眠或关闭状态。

 

 




