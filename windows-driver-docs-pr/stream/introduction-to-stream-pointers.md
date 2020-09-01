---
title: 流指针简介
description: 流指针简介
ms.assetid: 2682b145-5148-4301-b382-9811bb5e8fa6
keywords:
- 流指针 WDK AVStream，关于流指针
- 前移流指针 WDK AVStream
- 流指针 WDK AVStream，前进
- 帧引用计数 WDK AVStream
- 引用计数 WDK 流指针
- 计数引用 WDK 流指针
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e1f53e831cbaae66730fb7b1336cf115bdc0490
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190911"
---
# <a name="introduction-to-stream-pointers"></a>流指针简介





在较旧的流类模型中，微型驱动程序负责维护其自己的数据流请求块 (SRB) 队列。 AVStream 通过流指针抽象提供此功能。 流指针是对特定 AVStream 数据帧的引用。

使用以微型驱动程序 [为中心的处理](pin-centric-processing.md) (大多数硬件驱动程序) 使用流指针来管理 pin 队列。 每个 pin 都具有独立的数据缓冲区队列。 当数据包到达 pin 时 () 读取或写入请求时，AVStream 会将数据包添加到队列中，并可能调用 pin 的进程调度。

使用以筛选器为中心的处理的微型驱动程序不应直接使用流指针。 有关详细信息，请参阅以 [筛选为中心的处理](filter-centric-processing.md) 。

默认情况下，每个队列都具有一个前导边缘流指针。 或者，如果指定了尾部边缘标志，则它可以有一个尾随边缘流指针。 微型驱动程序可以通过调用 [**KsStreamPointerClone**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)创建新的流指针。

只能在一个方向上移动流指针：到较新的帧。 这称为前进流指针。

### <a name="advancing-a-stream-pointer"></a>前进流指针

当你前进流指针时，请将其移动到较新的帧，或将其前进到其当前帧中的一些字节。 例如，微型驱动程序可以将第一个帧到达的流指针前进到第二个帧到达。

若要前进流指针，可以在以零为中心的情况下调用 [**KsStreamPointerAdvance**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvance) 或 [**KsStreamPointerUnlock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock) ，并将 *Eject* 参数设置为 **TRUE**。

### <a name="frame-reference-counts"></a>帧引用计数

具有指向它们的流指针的帧具有引用计数，就像是在主边缘和尾随边缘之间的窗口中。

当微型驱动程序使用流指针完成后，它可以选择性地调用 [**KsStreamPointerSetStatusCode**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointersetstatuscode) 来指定一个错误代码，该代码用于完成给定 i/o 请求数据包 (IRP) 。 然后，微型驱动程序必须调用 [**KsStreamPointerDelete**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)。 然后，AVStream 将减少删除的流指针之前引用的帧上的引用计数。 不能删除前导边缘和尾随边缘流指针。

 

