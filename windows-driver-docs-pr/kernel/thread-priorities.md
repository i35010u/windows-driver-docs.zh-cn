---
title: 线程优先级
description: 线程优先级
keywords:
- 线程对象 WDK 内核
- 线程优先级 WDK 内核
- WDK 线程优先级
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: b2a41eb0af18e0a9584580c5cab71d37622c9342
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838259"
---
# <a name="thread-priorities"></a>线程优先级





某些驱动程序创建自己的驱动程序或专用于设备的系统线程，并将其线程的基本优先级设置为最低的实时优先级值。 其他顶级驱动程序（特别是文件系统驱动程序）使用系统工作线程，其基本优先级通常设置为最高变量优先级值。 内核计划一个线程，该线程具有最低的实时优先级，可在每个线程之前使用可变优先级运行，这包括系统中几乎每个用户模式线程。

大多数标准驱动程序例程在任意线程上下文中运行，该上下文位于当前处于 "就绪" 状态的所有线程之前。

线程（其各自的运行时优先级）在 IRQL = 被动 \_ 级别运行。 许多标准驱动程序例程以 IRQL &gt; 被动级别运行 \_ ，例如调度 \_ 级别或 DIRQL。

有关线程优先级的详细信息，请参阅 [计划、线程上下文和 IRQL](https://go.microsoft.com/fwlink/p/?linkid=59757) 白皮书。

 

 




