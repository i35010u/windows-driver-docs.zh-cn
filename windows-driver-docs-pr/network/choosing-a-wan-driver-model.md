---
title: 选择 WAN 驱动程序模型
description: 选择 WAN 驱动程序模型
ms.assetid: 63976cfa-6f7b-44d0-a4c5-de82254bedbd
keywords:
- WAN 微型端口驱动程序 WDK 网络驱动程序模型
- WAN 微型端口驱动程序 WDK 网络 NDIS WAN vs 的 CoNDIS WAN 驱动程序
- 驱动程序模型 WDK WAN
- CoNDIS 驱动程序 WDK 网络连接、 WAN 驱动程序
- WAN 的 CoNDIS 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee4578db0bbfc142fde6664de4afb52238e4d6da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563769"
---
# <a name="choosing-a-wan-driver-model"></a>选择 WAN 驱动程序模型





Microsoft Windows 2000 和更高版本操作系统支持两种 WAN 驱动程序模型：NDIS WAN 和 CoNDIS WAN。

NDIS WAN 微型端口驱动程序是无连接的微型端口驱动程序在 NDIS 模型上生成的。 NDIS 版本 5.0 和更高版本的驱动程序不支持 NDIS WAN 的微型端口驱动程序。 新的驱动程序应基于的 CoNDIS WAN 驱动程序体系结构。

WAN 的 CoNDIS 驱动程序是基于面向连接的 NDIS (CoNDIS) 驱动程序模型。

WAN 的 CoNDIS 微型端口驱动程序和微型端口调用管理器 (MCMs) 可以：

-   调用非 WAN 面向连接的微型端口驱动程序调用的相同 NDIS 函数。

-   导出属于同一套*MiniportXxx*非 WAN 面向连接的微型端口驱动程序导出的函数。

-   提供其他特定于 WAN 的功能。

有关的 CoNDIS 驱动程序的详细信息，请参阅[Connection-Oriented NDIS](connection-oriented-ndis.md)。

如果你正在编写新的 WAN 驱动程序，我们建议你使用的 CoNDIS WAN 模型。

Microsoft 将继续支持现有 NDIS WAN 的微型端口驱动程序。 不需要编写的 CoNDIS 旧硬件的驱动程序。

下面的主题介绍使用 WAN 的 CoNDIS 模型的主要优点：

[WAN 的 CoNDIS 是更加灵活](condis-wan-is-more-flexible.md)

[WAN 的 CoNDIS 是不太复杂](condis-wan-is-less-complex.md)

[其他权益的 CoNDIS WAN](other-benefits-of-condis-wan.md)

[提供的 CoNDIS WAN 驱动程序的其他 NDIS 功能](other-ndis-features-available-to-condis-wan-drivers.md)

 

 





