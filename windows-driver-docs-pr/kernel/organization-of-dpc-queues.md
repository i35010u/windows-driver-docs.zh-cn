---
title: DPC 队列的组织
description: DPC 队列的组织
ms.assetid: df176a6d-d7a7-4d8b-ab1b-fd7f5b89fcbe
keywords:
- DPC 排队 WDK 内核
- 队列 WDK DPC
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3ba36b279b3d7b794991a6e9a3b5634dc83cf3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838524"
---
# <a name="organization-of-dpc-queues"></a>DPC 队列的组织


系统为每个处理器提供一个 DPC 队列。 驱动程序可以控制系统将 DPC 分配到的队列、DPC 在队列中的位置以及处理队列的时间。

分配给特定处理器队列的 Dpc 在该处理器上运行。 默认情况下，当驱动程序调用[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)或[**IOREQUESTDPC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)时，DPC 在当前活动的处理器上排队。 在调用**KeInsertQueueDpc**或**IoRequestDpc**之前，驱动程序可以通过调用[**KeSetTargetProcessorDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kesettargetprocessordpc)来指定处理器队列。

在 Windows Vista 和更高版本的 Windows 上，系统还具有每个处理器的一个线程 DPC 队列。 驱动程序可以使用**KeSetTargetProcessorDpc**来指定线程化 dpc 的处理器队列。

[**KeSetImportanceDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kesetimportancedpc)例程控制在队列中放置 DPC 的位置。 通常，DPC 位于队列末尾;但如果驱动程序首先调用**KeSetImportanceDpc**的*重要性*参数等于**HighImportance**，则 DPC 会置于队列的开头。

对于普通（非线程） Dpc， **KeSetImportanceDpc**还确定**KeInsertQueueDpc**或**IoRequestDpc**是否将立即开始处理 DPC 队列。 以下列表描述了用于处理队列的规则：

-   如果将 DPC 分配给当前处理器且*重要性*不等于**LowImportance**，或者*重要性*等于**LowImportance** ，而 dpc 队列深度为当前，则开始处理 dpc 队列会立即开始处理处理器超过系统定义的限制，或者 DPC 请求速率低于系统定义的最小值。 否则，会延迟处理 DPC，直到满足适当的队列深度和速率要求。

-   如果将 DPC 分配给不同于当前处理器且*重要性*等于**MediumHighImportance**或**HIGHIMPORTANCE**的处理器，则 dpc 队列的处理会立即开始，如果 dpc目标处理器的队列深度超出了系统定义的限制。 否则，会延迟处理 DPC，直到满足适当的队列深度和速率要求。

 

 




