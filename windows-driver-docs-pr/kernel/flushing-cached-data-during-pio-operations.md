---
title: 执行 PIO 操作期间刷新缓存数据
description: 执行 PIO 操作期间刷新缓存数据
ms.assetid: 8b15f1c4-d3c9-4d61-be37-ee1593f9d5e5
keywords:
- 刷新缓存的数据
- KeFlushIoBuffers
- PIO 传输操作 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 619a5b3727d5fb7cba0d8dde734050439905c41e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191477"
---
# <a name="flushing-cached-data-during-pio-operations"></a>执行 PIO 操作期间刷新缓存数据





在某些平台上，处理器中的指令和数据缓存表现出在 PIO 读取操作期间缓存一致性异常。

**注意**   若要在读取操作期间维护数据完整性，使用 PIO 的驱动程序必须遵循此准则：在每个读取操作结束时调用[**KeFlushIoBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 。

例如，使 PIO 从其设备传输到系统内存的驱动程序应在每个设备传输操作结束时调用 **KeFlushIoBuffers** 。 作为另一个示例，读取设备寄存器序列到系统内存的驱动程序应在序列的末尾调用 **KeFlushIoBuffers** 。 否则，此类驱动程序可能会尝试访问在某些平台上仍位于处理器数据缓存中的数据，而不是在系统内存中。

 

如果可以依赖于处理器来维护缓存的一致性， **KeFlushIoBuffers**不会执行任何操作，因此，对此支持例程的调用在此类平台上几乎没有任何开销。

 

