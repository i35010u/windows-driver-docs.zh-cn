---
title: “选择 WAN 驱动程序模型”简介
description: “选择 WAN 驱动程序模型”简介
keywords:
- WAN 微型端口驱动程序 WDK 网络，驱动程序型号
- WAN 微型端口驱动程序 WDK 网络，NDIS WAN 与 CoNDIS WAN 驱动程序
- 驱动程序型号 WDK WAN
- CoNDIS 驱动程序 WDK 网络，WAN 驱动程序
- CoNDIS WAN 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b5fa4f9b4a5d9c4fb89de9e9c1f0e6d3c3de731
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787279"
---
# <a name="introduction-to-choosing-a-wan-driver-model"></a>“选择 WAN 驱动程序模型”简介





Microsoft Windows 2000 及更高版本的操作系统支持两个 WAN 驱动程序模型： NDIS WAN 和 CoNDIS WAN。

NDIS WAN 微型端口驱动程序在 NDIS 模型上构建，用于连接的微型端口驱动程序。 对于 NDIS 版本5.0 和更高版本的驱动程序，不支持 NDIS WAN 微型端口驱动程序。 新驱动程序应基于 CoNDIS WAN 驱动程序体系结构。

CoNDIS WAN 驱动程序在面向连接的 NDIS (CoNDIS) 驱动程序模型之上构建而成。

 (MCMs) 的 CoNDIS WAN 微型端口驱动程序和微型端口呼叫管理器可以：

-   调用与面向非 WAN 连接的小型端口驱动程序调用的相同 NDIS 函数。

-   导出非 WAN 连接面向的小型小型端口驱动程序导出的一组相同的 *MiniportXxx* 函数。

-   提供其他 WAN 特定功能。

有关 CoNDIS 驱动程序的详细信息，请参阅 [面向连接的 NDIS](connection-oriented-ndis.md)。

如果你正在编写新的 WAN 驱动程序，我们建议你使用 CoNDIS WAN 模型。

Microsoft 将继续支持现有的 NDIS WAN 微型端口驱动程序。 不需要为旧硬件编写 CoNDIS 驱动程序。

以下主题介绍使用 CoNDIS WAN 模型的主要优点：

[CoNDIS WAN 更灵活](condis-wan-is-more-flexible.md)

[CoNDIS WAN 更简单](condis-wan-is-less-complex.md)

[CoNDIS WAN 的其他优势](other-benefits-of-condis-wan.md)

[适用于 CoNDIS WAN 驱动程序的其他 NDIS 功能](other-ndis-features-available-to-condis-wan-drivers.md)

 

 





