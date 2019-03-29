---
title: 内核模式驱动程序的设计目标
description: 内核模式驱动程序的设计目标
ms.assetid: 2799556e-0359-4388-acf3-74d90eb86a0f
keywords:
- 内核模式驱动程序 WDK，设计目标
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16e01631509e6ae9bc58d0c88bf15bdc9b2a3e02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565036"
---
# <a name="design-goals-for-kernel-mode-drivers"></a>内核模式驱动程序的设计目标





内核模式驱动程序共享许多操作系统，特别是那些系统 I/O 管理器的设计目标。 内核模式驱动程序设计为：

-   [可移植](portable.md)从到另一个平台。

-   [可配置](configurable.md)到各种硬件和软件平台。

-   [始终 preemptible 且始终不中断](always-preemptible-and-always-interruptible.md)。

-   [包含多个处理器安全](multiprocessor-safe.md)在多处理器平台上。

-   [基于对象的](object-based.md)。

-   [使用可重用的 Irp I/O 驱动数据包](packet-driven-i-o-with-reusable-irps.md)。

-   能够[支持异步 I/O](supporting-asynchronous-i-o.md)。

 

 




