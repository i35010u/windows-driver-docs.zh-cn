---
title: 微型端口适配器挂起检查和重置操作
description: 微型端口适配器挂起检查和重置操作
ms.assetid: 53ffc5a9-bcba-4189-8845-73adfcf6816d
keywords:
- 微型端口适配器 WDK 网络连接、 检查用于挂起操作
- 微型端口适配器 WDK 网络重置操作
- 适配器 WDK 网络连接、 检查用于挂起操作
- 适配器 WDK 网络重置操作
- MiniportCheckForHangEx
- 挂起并重置 o
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab54d733f705f88d83236b54f95e319bff288635
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565627"
---
# <a name="miniport-adapter-check-for-hang-and-reset-operations"></a>微型端口适配器挂起检查和重置操作

## <a name="overview"></a>概述

> [!WARNING]
> 检查有关挂起 (CFH) 和重置操作的所有 NDIS 6.83 和更高版本的驱动程序不建议使用。 有关详细信息，请参阅[NDIS 6.83 及更高版本的检查有关挂起和重置操作](#check-for-hang-and-reset-operations-in-ndis-683-and-later)。

NDIS 调用 NDIS 微型端口驱动程序的[ *MiniportCheckForHangEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559346)函数来检查表示网络接口卡 (NIC) 的 NDIS 适配器的操作状态。 *MiniportCheckForHangEx*检查适配器的内部状态，并返回**TRUE**如果它检测到该适配器不正常运行。

默认情况下，调用 NDIS *MiniportCheckForHangEx*大约每隔 2 秒。 如果*MiniportCheckForHangEx*返回**TRUE**，NDIS 调用 NDIS 微型端口驱动程序[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)函数。 如果为 2 秒的默认超时值太小，微型端口驱动程序可以设置不同的值在初始化时，如下所示：

1.  设置**CheckForHangTimeInSeconds**的成员[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)为非零值的结构。
2.  传递[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构*MiniportAttributes*的参数[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

有关设置驱动程序属性的详细信息，请参阅[初始化适配器](initializing-a-miniport-adapter.md)。
值**CheckForHangTimeInSeconds**应大于微型端口驱动程序初始化时。 但是，如果您的驱动程序花费的时间比**CheckForHangTimeInSeconds**秒才能完成初始化，此超时时间已到引起 NDIS 以调用您的驱动程序*MiniportCheckForHangEx*函数。 如果*MiniportCheckForHangEx*返回**TRUE**，NDIS 将调用您的驱动程序*MiniportResetEx*函数。 出于此原因，您应将您的驱动程序同步[ *MiniportCheckForHangEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559346)函数与驱动程序初始化因此*MiniportCheckForHangEx*将不会返回 **，则返回 TRUE**如果驱动程序尚未完成初始化。

如果您的微型端口驱动程序未完成的 OID 请求内对两个连续调用*MiniportCheckForHangEx*，NDIS 可以调用的驱动程序*MiniportResetEx*函数。 对于某些 OID 请求，调用 NDIS *MiniportResetEx*如果驱动程序不会完成四个连续调用中的请求*MiniportCheckForHangEx*。

重置操作不会影响[微型端口适配器操作状态](miniport-adapter-states-and-operations.md)。 此外，重置操作正在进行时，可能会更改该适配器的状态。 例如，NDIS 可能调用的驱动程序[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)函数重置操作正在进行中的时。 在这种情况下，该驱动程序可以完成重置或暂停操作，按任意顺序遵循每个操作的常规要求。

对于重置操作，该驱动程序可能会传输请求数据包失败或它可以使它们保持排队和完成这些更高版本。 但是，您应该注意基础驱动程序无法完成暂停操作时其传输数据包处于挂起状态。

微型端口驱动程序可以通过返回成功或失败状态以同步方式完成重置请求。 该驱动程序可以以异步方式完成重置请求，通过返回**NDIS\_状态\_PENDING**。 在这种情况下，该驱动程序必须调用[ **NdisMResetComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563663)以完成操作。

## <a name="check-for-hang-and-reset-operations-in-ndis-683-and-later"></a>检查有关挂起和重置操作 NDIS 6.83 及更高版本

在的 NDIS 6.83 之前的版本，检查有关挂起 (CFH) 和重置操作会建议为 Always On，由于电池寿命问题始终连接 (AOAC) 系统中。 但是，驱动程序可以仍使用 CFH 其他非 AOAC Windows 系统上通过实现的可选[ *MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)并[ *MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)回调函数。 

从 NDIS 6.83，这些回调函数将不建议使用上**所有**而不考虑电源功能的 Windows 系统。 虽然它不是使用 CFH NDIS 6.83 及更高版本的徽标测试冲突，NDIS 驱动程序应使用下表，其使用情况有关的指南。

| 调用方 | 建议 | 说明 |
| --- | --- | --- |
| 面向 AOAC 系统驱动程序 | 必须实现 | 会导致电池寿命问题由于定期检查有关挂起活动 |
| 面向 Windows Server 系统的驱动程序 | 必须实现 | 导致出现问题时强调 CPU |
| 虚拟 （仅限软件） 的微型端口驱动程序 | 必须实现 | 重置不可能无需任何硬件 |
| 其他新的 NDIS 6.83 和更高版本的驱动程序 | 不应实现 |
| 其他现有 NDIS 6.82 和前面部分的代码 | 不需要更改，但应考虑删除检查有关挂起和重置在将来重新修改 |

## <a name="related-topics"></a>相关主题


[微型端口驱动程序硬件重置](hardware-reset.md)

[微型端口驱动程序重置和 Halt 函数](https://msdn.microsoft.com/library/windows/hardware/ff564064)

 

 






