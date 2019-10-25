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
ms.openlocfilehash: 948a83f986373952c698efce0c88dbdadd5cb070
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835996"
---
# <a name="using-critical-sections"></a>使用关键节





任何包含[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程的驱动程序都很可能需要一个或多个关键部分来同步对 ISR 和其他例程之间的硬件资源或驱动程序数据的访问。

本部分包括下列主题：

[SynchCritSection 例程简介](introduction-to-synchcritsection-routines.md)

[编写 SynchCritSection 例程](writing-synchcritsection-routines.md)

 

 




