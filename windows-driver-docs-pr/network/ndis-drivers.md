---
title: NDIS 驱动程序类型
description: NDIS 驱动程序类型
keywords:
- 网络驱动程序 WDK，NDIS 驱动程序
- NDIS WDK，支持的驱动程序类型
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2e9c14d31a63348f1b8bc213e381f4ff7ce605f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798031"
---
# <a name="ndis-driver-types"></a>NDIS 驱动程序类型

网络驱动程序接口规范 (NDIS) 库将网络硬件与网络驱动程序进行抽象化。 NDIS 还指定了分层网络驱动程序之间的标准接口，从而抽象了从上层驱动程序管理硬件的较低级别的驱动程序，如网络传输。 NDIS 还会维护网络驱动程序的状态信息和参数，包括指向函数、句柄和链接的参数块以及其他系统值的指针。

NDIS 支持以下主要类型的网络驱动程序：

-   [微型端口驱动程序](ndis-miniport-drivers2.md)

-   [协议驱动程序](ndis-protocol-drivers2.md)

-   [筛选器驱动程序](ndis-filter-drivers.md)

-   [中间驱动程序](ndis-intermediate-drivers.md)

>[!NOTE]
> 这些主题分别详细说明每种类型的 NDIS 驱动程序。 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅 [NDIS 驱动程序堆栈](ndis-driver-stack.md)。
