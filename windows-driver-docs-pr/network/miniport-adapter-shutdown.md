---
title: 微型端口适配器关闭
description: 微型端口适配器关闭
ms.assetid: 57d964f1-03c7-4b54-9d04-1d187c96e052
keywords:
- 微型端口适配器 WDK 网络，关闭
- 适配器 WDK 网络，关闭
- MiniportShutdownEx
- 微型端口驱动程序 WDK 网络，系统关闭
- NDIS 微型端口驱动程序 WDK，系统关闭
- 关闭 WDK 网络
- 系统关闭 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 811ce6079baed36cc9ff0d16c6e7781779e8dc5a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218005"
---
# <a name="miniport-adapter-shutdown"></a>微型端口适配器关闭





在微型端口驱动程序初始化期间，NDIS 微型端口驱动程序必须注册 [*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 函数。

系统关闭时，NDIS 会调用 NDIS 微型端口驱动程序的 [*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 函数。 *MiniportShutdownEx* 将硬件还原到已知状态。

NDIS 传递到[*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)的*ShutdownAction*参数将通知端口关闭的原因。

关闭处理程序可以作为用户操作的结果进行调用，在这种情况下，它将以 IRQL = 被动 \_ 级别运行。 还可以通过无法恢复的系统错误（在这种情况下，它可以在任何 IRQL 上运行）来调用它。

[*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 不应调用 **Ndis * Xxx*** 函数。 微型端口驱动程序可以调用用于读取和写入 i/o 端口的功能，或禁用 DMA 引擎以将硬件返回到已知状态。

与 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)不同， [*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 不应释放任何分配的资源。 *MiniportShutdownEx* 应仅停止 NIC。

## <a name="related-topics"></a>相关主题


[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)

[停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[编写 NDIS 微型端口驱动程序](./initializing-a-miniport-driver.md)

 

