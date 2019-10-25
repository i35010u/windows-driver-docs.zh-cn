---
title: 网络驱动程序中的 IRQL
description: 网络驱动程序中的 IRQL
ms.assetid: d8720084-460e-4b62-90de-abfd96cd6364
keywords:
- 网络驱动程序 WDK，IRQLs
- IRQLs WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: fb7042b4f1f60b50f014ece6d4ba295d1dc239ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844158"
---
# <a name="irqls-in-network-drivers"></a>网络驱动程序中的 IRQL

NDIS 调用的每个驱动程序函数都在系统确定的 IRQL （被动\_级别之一）上运行，&lt; 调度\_级别 &lt; DIRQL）。 例如，微型端口驱动程序的[初始化](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数、[中断](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数、[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数和[关闭](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)函数通常在被动\_级别运行，但可以在更高如果系统需要，则为 IRQL。 中断代码在 DIRQL 运行，因此 NDIS 中间或协议驱动程序永远不会在 DIRQL 上运行。 所有其他 NDIS 驱动程序函数都在 IRQL = 调度\_级别下运行。

驱动程序函数运行的 IRQL 会影响它可以调用的 NDIS 函数。 只能在 IRQL = 被动\_级别调用某些函数。 其他人可以在调度\_级别或更低级别进行调用。 应检查每个 NDIS 函数是否有 IRQL 限制。

与驱动程序的中断服务例程（ISR）共享资源的任何驱动程序函数都必须能够将其 IRQL 提升为 DIRQL，以防出现争用情况。 NDIS 提供此类机制。