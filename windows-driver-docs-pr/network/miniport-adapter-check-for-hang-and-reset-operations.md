---
title: 微型端口适配器挂起检查和重置操作
description: 微型端口适配器挂起检查和重置操作
ms.assetid: 53ffc5a9-bcba-4189-8845-73adfcf6816d
keywords:
- 小型端口适配器 WDK 网络，检查挂起操作
- 微型端口适配器 WDK 网络，重置操作
- 适配器 WDK 网络，检查挂起操作
- 适配器 WDK 网络，重置操作
- MiniportCheckForHangEx
- 挂起并重置 o
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 411396de557625c94f2281377a8e5626aa2597b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844258"
---
# <a name="miniport-adapter-check-for-hang-and-reset-operations"></a>微型端口适配器挂起检查和重置操作

## <a name="overview"></a>概述

> [!WARNING]
> 对于所有 NDIS 6.83 和更高版本的驱动程序，不建议进行检查挂起（CFH）和重置操作。 有关详细信息，请参阅[NDIS 6.83 和更高版本中的检查挂起和重置操作](#check-for-hang-and-reset-operations-in-ndis-683-and-later)。

NDIS 调用 NDIS 微型端口驱动程序的[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)函数来检查表示网络接口卡（NIC）的 ndis 适配器的操作状态。 *MiniportCheckForHangEx*检查适配器的内部状态，如果它检测到适配器运行不正常，则返回**TRUE** 。

默认情况下，NDIS 大约每2秒调用*MiniportCheckForHangEx* 。 如果*MiniportCheckForHangEx*返回**TRUE**，ndis 将调用 ndis 微型端口驱动程序的[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数。 如果默认超时值为2秒太小，则微型端口驱动程序可以在初始化时设置不同的值，如下所示：

1.  将[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)的**CheckForHangTimeInSeconds**成员设置为非零值\_注册\_属性结构。
2.  在[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的*MiniportAttributes*参数中传递[**NDIS\_微型端口\_适配器\_注册\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构。

有关设置驱动程序属性的详细信息，请参阅[初始化适配器](initializing-a-miniport-adapter.md)。
**CheckForHangTimeInSeconds**的值应大于微型端口驱动程序的初始化时间。 但是，如果驱动程序的初始化时间超过**CheckForHangTimeInSeconds**秒，此超时将过期，导致 NDIS 调用驱动程序的*MiniportCheckForHangEx*函数。 如果*MiniportCheckForHangEx*返回**TRUE**，NDIS 将调用驱动程序的*MiniportResetEx*函数。 出于此原因，应将驱动程序的[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)函数与驱动程序初始化同步，以便当驱动程序未完成初始化时， *MiniportCheckForHangEx*不会返回**TRUE** 。

如果微型端口驱动程序未在两次连续调用*MiniportCheckForHangEx*的情况下完成 OID 请求，NDIS 可以调用驱动程序的*MiniportResetEx*函数。 对于某些 OID 请求，如果驱动程序未在四次连续调用*MiniportCheckForHangEx*的情况下完成请求，NDIS 将调用*MiniportResetEx* 。

Reset 操作不会影响[微型端口适配器操作状态](miniport-adapter-states-and-operations.md)。 此外，当重置操作正在进行时，适配器的状态可能会发生更改。 例如，如果正在执行重置操作，NDIS 可能会调用驱动程序的[*MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)函数。 在这种情况下，驱动程序可以按任意顺序完成重置或暂停操作，同时满足每个操作的一般要求。

对于 reset 操作，驱动程序可能会导致传输请求数据包失败，或者可以将它们保留在队列中，稍后再完成。 但是，你应注意，如果某个过量驱动程序的传输数据包处于挂起状态，则无法完成暂停操作。

微型端口驱动程序可以通过返回成功或失败状态来同步完成重置请求。 驱动程序可以通过返回**NDIS\_状态\_挂起**来异步完成重置请求。 在这种情况下，驱动程序必须调用[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)来完成此操作。

## <a name="check-for-hang-and-reset-operations-in-ndis-683-and-later"></a>NDIS 6.83 和更高版本中的检查挂起和重置操作

在6.83 之前的 NDIS 版本中，由于电池寿命问题，不建议对 Always On、始终连接（AOAC）系统进行检查挂起（CFH）和重置操作。 但是，驱动程序仍然可以通过实现可选的[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)和[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)回调函数，在其他非 AOAC WINDOWS 系统上使用 CFH。 

从 NDIS 6.83 开始，无论在什么情况下，都不会在**所有**Windows 系统上都建议这些回调函数。 尽管它不是在 NDIS 6.83 和更高版本中使用 CFH 的徽标测试冲突，但 NDIS 驱动程序应使用下表来获取有关其使用情况的指导。

| 呼叫 | 建议 | 注释 |
| --- | --- | --- |
| 面向 AOAC 系统的驱动程序 | 不得实现 | 由于定期检查挂起活动导致电池寿命问题 |
| 面向 Windows Server 系统的驱动程序 | 不得实现 | 导致 CPU 压力时出现问题 |
| 虚拟（仅限软件）微型端口驱动程序 | 不得实现 | 在没有硬件的情况下重置 |
| 其他新的 NDIS 6.83 和更高版本的驱动程序 | 不应实现 |
| 其他现有的 NDIS 6.82 和更早的代码 | 无需更改，但应考虑删除签入挂起并重置以后的改编 |

## <a name="related-topics"></a>相关主题


[微型端口驱动程序硬件重置](hardware-reset.md)

[微型端口驱动程序重置和暂停函数](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






