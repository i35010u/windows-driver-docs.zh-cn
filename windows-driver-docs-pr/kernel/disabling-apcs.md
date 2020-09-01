---
title: 禁用 APC
description: 禁用 APC
ms.assetid: 0578df31-1467-4bad-ba62-081d61278deb
keywords:
- 异步过程调用 WDK 内核
- Apc WDK 内核
- 禁用 Apc
- 关键区域 WDK 内核
- 受保护区域 WDK 内核
- 引发当前 IRQLs
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d736eca6da0693173ba79fd6533866268d7181ce
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185658"
---
# <a name="disabling-apcs"></a>禁用 APC


系统提供了三种机制来禁用当前线程的 Apc：

-   **关键区域。** 当某个线程在关键区域内时，不会执行其用户的 Apc 和普通内核 Apc。 特殊内核 Apc 仍在执行。 有关这些 APC 类型的详细信息，请参阅 [apc 的类型](types-of-apcs.md)。

-   **受保护区域。** 当某个线程处于受保护的区域内时，将不会执行其任何 Apc。

-   **向 APC \_ 级别或更高版本引发当前 IRQL。** 在 IRQL &gt; = APC 级别执行的线程在 \_ 禁用所有 apc 后执行。

请注意，这些设置适用于当前线程，不会影响任何其他线程的行为。

必须在禁用特定类型的 Apc 的情况调用某些驱动程序支持例程。 例如，必须在禁用普通内核 Apc 的情况下调用获取 executive 资源 (（如 [**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))) ）的例程。 必须在启用特定类型的 Apc 的情况调用其他例程。 例如，必须在启用特殊内核 Apc 的情况下调用依赖于 i/o 完成例程的任何例程 (例如 [**IoVolumeDeviceToDosName**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iovolumedevicetodosname)) 。 每个例程的文档指定例程是否对 APC 执行状态有任何特定限制。

驱动程序可以通过调用相应的例程来显式输入关键或受保护的区域。 有关详细信息，请参阅 [关键区域和受保护区域](critical-regions-and-guarded-regions.md)。 驱动程序还可以通过调用 KeRaiseIrql，将当前 IRQL 显式提升到 APC \_ 级别。 [**KeRaiseIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql) 然后，该驱动程序必须通过调用 [**KeLowerIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)来将 IRQL 减小到其原始值。 使用受保护的区域比引发和降低当前的 IRQL 更快，但是受保护的区域仅在 Windows Server 2003 和更高版本的 Windows 中可用。

以下 mutex 操作具有与进入或离开关键或受保护的区域或引发或降低当前 IRQL 相同的效果：

-   保留 mutex 对象会将持有者隐式置于关键区域中。

-   保留受保护的 mutex 会将持有者隐式放置在受保护的区域内。

-   保留快速 mutex 会将当前的 IRQL 隐式提升到 APC \_ 级别。

有关 mutex 对象的详细信息，请参阅 [Mutex 对象](mutex-objects.md)。 有关快速和受保护的互斥体的详细信息，请参阅 [快速互斥体和受保护的互斥体](fast-mutexes-and-guarded-mutexes.md)。

 

