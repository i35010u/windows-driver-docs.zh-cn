---
title: 内核模式驱动程序的设计目标
description: 内核模式驱动程序的设计目标
keywords:
- 内核模式驱动程序 WDK，设计目标
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec660e4e04711be5c1b49699caef4fd6bae0340c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798111"
---
# <a name="design-goals-for-kernel-mode-drivers"></a>内核模式驱动程序的设计目标





内核模式驱动程序共享操作系统的多种设计目标，特别是系统 i/o 管理器的设计目标。 内核模式驱动程序的设计是：

-   [可](portable.md) 从一个平台移植到另一个平台。

-   [可配置](configurable.md) 各种硬件和软件平台。

-   [始终 preemptible 并始终中断](always-preemptible-and-always-interruptible.md)。

-   多处理器平台上[的多处理器安全](multiprocessor-safe.md)。

-   [基于对象](object-based.md)。

-   [使用可重用 irp 的数据包驱动的 i/o](packet-driven-i-o-with-reusable-irps.md)。

-   [支持异步 i/o](supporting-asynchronous-i-o.md)。

 

 




