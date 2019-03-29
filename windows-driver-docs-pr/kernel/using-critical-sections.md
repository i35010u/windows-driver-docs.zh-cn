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
ms.openlocfilehash: f7c92791abf47c6b267f6a5f2e2f5719c50d77aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569435"
---
# <a name="using-critical-sections"></a>使用关键节





包含任何驱动程序[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程将很可能需要一个或多临界区同步访问硬件资源或驱动程序间 ISR 和其他例程的数据.

本部分包括以下主题：

[SynchCritSection 例程简介](introduction-to-synchcritsection-routines.md)

[编写 SynchCritSection 例程](writing-synchcritsection-routines.md)

 

 




