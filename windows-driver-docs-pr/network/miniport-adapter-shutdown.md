---
title: 微型端口适配器关闭
description: 微型端口适配器关闭
ms.assetid: 57d964f1-03c7-4b54-9d04-1d187c96e052
keywords:
- 微型端口适配器 WDK 网络、 关闭
- 适配器 WDK 网络、 关闭
- MiniportShutdownEx
- 微型端口驱动程序 WDK 网络，系统关闭
- NDIS 微型端口驱动程序 WDK，系统关闭
- 关闭 WDK 网络
- 系统关闭 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45b590e7beacc491731c442dee3e248743db82ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373955"
---
# <a name="miniport-adapter-shutdown"></a>微型端口适配器关闭





NDIS 微型端口驱动程序必须注册[ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)微型端口驱动程序初始化期间的函数。

NDIS 调用 NDIS 微型端口驱动程序的[ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)系统关闭时的功能。 *MiniportShutdownEx*将硬件恢复到已知状态。

*ShutdownAction* NDIS 传递给参数[ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)通知关机的原因的微型端口驱动程序。

可以调用关闭处理程序由于用户操作，而在此情况下它运行在 IRQL = 被动\_级别。 它也可以调用作为不可恢复的系统错误结果，这种情况下它可以运行的任何 irql。

[*MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)应调用无**Ndis * Xxx*** 函数。 微型端口驱动程序可以读取和写入 I/O 端口或禁用要返回到已知状态的硬件的 DMA 引擎调用函数。

与不同[ *MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)， [ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)应释放任何已分配的资源。 *MiniportShutdownEx*应只是停止 nic。

## <a name="related-topics"></a>相关主题


[适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)

[正在停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[编写 NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)

 

 






