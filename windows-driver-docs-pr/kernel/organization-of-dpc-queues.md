---
title: DPC 队列的组织
description: DPC 队列的组织
ms.assetid: df176a6d-d7a7-4d8b-ab1b-fd7f5b89fcbe
keywords:
- DPC 队列 WDK 内核
- WDK DPC 队列
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8895aecb8cb3ac08235b911f34bd26d978967c80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519982"
---
# <a name="organization-of-dpc-queues"></a>DPC 队列的组织


系统为每个处理器提供了一个 DPC 队列。 驱动程序可以的控制其排队系统将分配到的位置在队列中 DPC DPC 和处理队列的时间。

分配给特定处理器的队列的 Dpc 的处理器上运行。 默认情况下，当驱动程序调用[ **KeInsertQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552185)或[ **IoRequestDpc**](https://msdn.microsoft.com/library/windows/hardware/ff549657)，DPC 排队当前处于活动状态的处理器上。 驱动程序可以通过调用指定处理器队列[ **KeSetTargetProcessorDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff553278)之前调用**KeInsertQueueDpc**或**IoRequestDpc**.

在 Windows Vista 和更高版本的 Windows 上，系统还具有一个线程的 DPC 队列的每个处理器。 驱动程序可以使用**KeSetTargetProcessorDpc**指定线程 Dpc 的处理器队列。

[ **KeSetImportanceDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff553259)例程 DPC 队列中的放置位置的控件。 通常情况下，将 DPC 放在队列; 末尾但是，如果该驱动程序首先调用**KeSetImportanceDpc**与*重要性*参数等于**HighImportance**，DPC 位于队列开始处。

对于普通 （非线程） Dpc **KeSetImportanceDpc**还确定是否**KeInsertQueueDpc**或**IoRequestDpc**会立即开始处理 DPC队列。 以下列表描述用于处理队列的规则：

-   处理的 DPC 队列会立即开始如果 DPC 分配给当前的处理器和*重要性*不等于**LowImportance**，或者，如果*重要性*是等于**LowImportance**和当前处理器的 DPC 队列深度超过系统定义的限制或 DPC 请求速率已低于系统定义的最小值。 否则，处理 DPC 会推迟到满足相应的队列深度和速率要求。

-   处理的 DPC 队列会立即开始目标处理器上如果 DPC 分配到不同于当前处理器的处理器和*重要性*等于**MediumHighImportance**或**HighImportance**，或如果目标处理器的 DPC 队列深度超过系统定义的限制。 否则，处理 DPC 会推迟到满足相应的队列深度和速率要求。

 

 




