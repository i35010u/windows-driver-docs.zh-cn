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
ms.openlocfilehash: 72d98502c42266a36ca4d90242b265b35af7f666
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386596"
---
# <a name="flushing-cached-data-during-pio-operations"></a>执行 PIO 操作期间刷新缓存数据





在某些平台上中处理器的指令和数据缓存在 PIO 读取操作期间出现缓存协调性异常。

**请注意**  若要在其读取操作期间保持数据完整性，使用 PIO 的驱动程序必须遵循此原则：调用[ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)末尾的每个读取操作。

例如，使其设备从到系统内存的 PIO 传输驱动程序应调用**KeFlushIoBuffers**末尾的每个设备传输操作。 另举一例，读取一系列设备注册到系统内存的驱动程序应调用**KeFlushIoBuffers**序列的末尾。 否则，此类驱动程序可能会尝试访问是仍在处理器的数据缓存，而不是在系统内存中，在某些平台上的数据。

 

**KeFlushIoBuffers** nothing 如果处理器可以依赖于到中保存了缓存一致性，因此对此支持例程的调用具有这种平台中几乎没有开销。

 

 




