---
title: 使用关键节
description: 使用关键节
keywords:
- 中断服务例程 WDK 内核，关键部分
- Isr WDK 内核，关键部分
- InterruptService
- 同步 WDK 内核，中断
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 625945f5d16e4d93c693621d065817bd7f105024
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825591"
---
# <a name="using-critical-sections"></a>使用关键节





任何包含 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程的驱动程序都很可能需要一个或多个关键部分来同步对 ISR 和其他例程之间的硬件资源或驱动程序数据的访问。

本节包括下列主题：

[SynchCritSection 例程简介](introduction-to-synchcritsection-routines.md)

[编写 SynchCritSection 例程](writing-synchcritsection-routines.md)

 

