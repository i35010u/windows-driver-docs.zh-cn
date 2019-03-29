---
title: 线程优先级
description: 线程优先级
ms.assetid: 87a9641c-0569-45c1-acb8-adf5856dc60d
keywords:
- 线程对象 WDK 内核
- 线程优先级 WDK 内核
- WDK 线程优先级
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: a2adf291d734656e85d37a40c09139dba0ab8356
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569432"
---
# <a name="thread-priorities"></a>线程优先级





某些驱动程序创建其自己的驱动程序或设备专用系统线程，并将其线程的基本优先级设置为实时优先级值最低。 其他最高级别的驱动程序，尤其是文件系统驱动程序，使用通常设置为最高的变量的优先级值的基本优先级的系统工作线程数。 内核计划具有最低实时优先级变量优先级，其中包括系统中的几乎每个用户模式线程运行之前每个线程的线程。

大多数标准驱动程序例程在任意线程上下文中，当前处于就绪状态的所有线程之前运行。

线程，无论其各自的运行时优先级，运行在 IRQL = 被动\_级别。 许多标准驱动程序例程运行在 IRQL&gt;被动\_级别，例如调度\_级别或 DIRQL。

有关线程优先级的详细信息，请参阅[计划，线程上下文和 IRQL](https://go.microsoft.com/fwlink/p/?linkid=59757)白皮书。

 

 




