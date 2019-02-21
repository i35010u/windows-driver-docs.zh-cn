---
title: NDIS 驱动程序类型
description: NDIS 驱动程序类型
ms.assetid: ed7bd8b4-75d5-4ecd-beb2-df8ac1ce96b3
keywords:
- 网络驱动程序 WDK、 NDIS 驱动程序
- NDIS WDK 支持的驱动程序类型
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: eff0dd928da2288cc50f5ae3af963279885d2a19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525450"
---
# <a name="ndis-driver-types"></a>NDIS 驱动程序类型

将网络驱动程序从网络硬件抽象处理网络驱动程序接口规范 (NDIS) 库。 NDIS 还指定分层的网络驱动程序，从而减少了管理硬件，从较高级别驱动程序，例如网络传输的较低级驱动程序方面之间的标准接口。 NDIS 还维护状态信息和网络驱动程序，包括指向函数、 句柄、 和参数块，用于链接和其他系统值的参数。

NDIS 支持以下主要类型的网络驱动程序：

-   [微型端口驱动程序](ndis-miniport-drivers2.md)

-   [协议驱动程序](ndis-protocol-drivers2.md)

-   [筛选器驱动程序](ndis-filter-drivers.md)

-   [中间驱动程序](ndis-intermediate-drivers.md)

>[!NOTE]
> 这些主题分别详细介绍每种类型的 NDIS 驱动程序。 有关 NDIS 驱动程序堆栈和一个显示所有四个的 NDIS 驱动程序类型之间的关系图的详细信息，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。