---
title: 使用关键节
description: 使用关键节
ms.assetid: 439ba7ef-6473-40ca-9daa-a8c61d789d97
keywords:
- 中断服务例程 WDK 内核，关键部分
- Isr WDK 内核，关键部分
- InterruptService
- 同步 WDK 内核中断
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a7ab16c71ba6acc0625d42e128d7017278dcca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381671"
---
# <a name="using-critical-sections"></a>使用关键节





包含任何驱动程序[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)例程将很可能需要一个或多临界区同步访问硬件资源或驱动程序间 ISR 和其他例程的数据.

本部分包括以下主题：

[SynchCritSection 例程简介](introduction-to-synchcritsection-routines.md)

[编写 SynchCritSection 例程](writing-synchcritsection-routines.md)

 

 




