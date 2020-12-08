---
title: 网络驱动程序中的 IRQL
description: 网络驱动程序中的 IRQL
keywords:
- 网络驱动程序 WDK，IRQLs
- IRQLs WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: c9f4490c0a2a0c6f99cf5a598512ee1d3893a36f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789761"
---
# <a name="irqls-in-network-drivers"></a>网络驱动程序中的 IRQL

NDIS 调用的每个驱动程序函数都在系统确定的 IRQL 上运行， (被动 \_ 级别 &lt; 调度 \_ 级别 &lt; DIRQL) 之一。 例如，微型端口驱动程序的 [初始化](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数、 [中断](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数、 [重置](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数和 [关闭](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 函数通常在被动 \_ 级别运行，但如果重置和关闭函数在系统需要它的情况下可以以更高的 IRQL 调用。 中断代码在 DIRQL 运行，因此 NDIS 中间或协议驱动程序永远不会在 DIRQL 上运行。 所有其他 NDIS 驱动程序函数都在 IRQL = 调度级别下运行 \_ 。

驱动程序函数运行的 IRQL 会影响它可以调用的 NDIS 函数。 只能在 IRQL = 被动级别调用某些函数 \_ 。 其他人可以在派单 \_ 或更低的级别调用。 应检查每个 NDIS 函数是否有 IRQL 限制。

与驱动程序的中断服务例程（ (ISR) 共享资源的任何驱动程序函数必须能够将其 IRQL 提升为 DIRQL，以防出现争用情况。 NDIS 提供此类机制。
