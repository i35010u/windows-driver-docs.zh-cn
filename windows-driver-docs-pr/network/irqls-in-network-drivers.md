---
title: 网络驱动程序中于 Irql
description: 网络驱动程序中于 Irql
ms.assetid: d8720084-460e-4b62-90de-abfd96cd6364
keywords:
- 网络驱动程序 WDK，于 Irql
- 于 Irql WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e417d5d605c9de6d97b5bce77120ec8eb550ae9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533772"
---
# <a name="irqls-in-network-drivers"></a>网络驱动程序中于 Irql

在系统确定 IRQL 运行每个驱动程序函数调用的 NDIS (一个被动\_级别&lt;调度\_级别&lt;DIRQL)。 例如，微型端口驱动程序的[初始化](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，[暂停](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数，[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)函数，以及[关闭](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)函数通常运行在被动\_级别，但如果系统要求它可以在更高版本的 IRQL 调用重置和关机函数。 因此，NDIS 中间或协议驱动程序永远不会运行在 DIRQL 中断 DIRQL，在代码运行。 所有其他 NDIS 驱动程序函数运行或以下的 IRQL = 调度\_级别。

IRQL 运行驱动程序函数会影响它可以调用哪些 NDIS 函数。 某些函数可以调用仅在 IRQL = 被动\_级别。 其他人可以在调度调用\_级别或更低。 应检查 IRQL 限制每个 NDIS 函数。

驱动程序的中断服务例程 (ISR) 与共享资源的任何驱动程序函数必须能够引发其 IRQL 到 DIRQL 避免出现争用情况。 NDIS 提供此类的机制。