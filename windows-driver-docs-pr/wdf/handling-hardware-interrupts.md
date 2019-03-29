---
title: 处理硬件中断
description: 介绍如何 WDF 驱动程序创建到服务硬件中断的中断对象和您的驱动程序将中断数据缓冲区的访问权限的同步。
ms.assetid: 08460510-6e5f-4c02-8086-9caa9b4b4c2d
keywords:
- 硬件中断 WDK KMDF
- 中断 WDK KMDF
- 基于框架的驱动程序 WDK KMDF，硬件中断
- 内核模式驱动程序 WDK KMDF，硬件中断
- KMDF WDK，硬件中断
- 内核模式驱动程序框架 WDK，硬件中断
- framework 对象 WDK KMDF，中断对象
- 中断对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff84de5b481d95c621001b1bb695340a51b9f7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575701"
---
# <a name="handling-hardware-interrupts"></a>处理硬件中断


在本部分中的主题介绍 Windows 驱动程序框架 (WDF) 驱动程序如何创建服务硬件中断的 framework 中断对象和您的驱动程序将中断数据缓冲区的访问权限的同步。




## <a name="in-this-section"></a>本节内容


-   [创建一个中断对象](creating-an-interrupt-object.md)
-   [启用和禁用中断](enabling-and-disabling-interrupts.md)
-   [服务中断](servicing-an-interrupt.md)
-   [同步中断代码](synchronizing-interrupt-code.md)
-   [支持被动级别中断](supporting-passive-level-interrupts.md)
-   [使用中断以唤醒设备](using-an-interrupt-to-wake-a-device.md)
-   [处理同时处于活动状态的中断](handling-active-both-interrupts.md)

 

 





