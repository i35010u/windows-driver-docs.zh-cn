---
title: 使用关键节
description: 使用关键节
ms.assetid: 439ba7ef-6473-40ca-9daa-a8c61d789d97
keywords:
- 中断服务例程 WDK 内核，关键部分
- Isr WDK 内核，关键部分
- InterruptService
- 同步 WDK 内核，中断
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1a897e6707ab3dbb57c71e40df8376406a37803
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187045"
---
# <a name="using-critical-sections"></a>使用关键节





任何包含 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程的驱动程序都很可能需要一个或多个关键部分来同步对 ISR 和其他例程之间的硬件资源或驱动程序数据的访问。

本节包括下列主题：

[SynchCritSection 例程简介](introduction-to-synchcritsection-routines.md)

[编写 SynchCritSection 例程](writing-synchcritsection-routines.md)

 

