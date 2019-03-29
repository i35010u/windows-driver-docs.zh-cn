---
title: 流指针简介
description: 流指针简介
ms.assetid: 2682b145-5148-4301-b382-9811bb5e8fa6
keywords:
- 流指针 WDK AVStream 有关流指针
- 前移流指针 WDK AVStream
- 流指针 WDK AVStream，改进
- 框架的引用计数 WDK AVStream
- 引用计数 WDK 流指针
- 计数 WDK 流指针的引用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e240abc6a03c7fb4ff0d25b00cc47bf44880ca45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565567"
---
# <a name="introduction-to-stream-pointers"></a>流指针简介





在较旧的流类模型，微型驱动程序是负责维护其自己数据的流请求块 (SRB) 队列。 AVStream 提供此功能通过流指针抽象。 流指针是为特定 AVStream 数据框架的引用。

使用的微型驱动程序[pin 以中心处理](pin-centric-processing.md)（大多数硬件驱动程序），使用流指针管理 pin 队列。 每个 pin 有独立队列的数据缓冲区。 当数据包到达 pin （的读取或写入请求） 时，AVStream 将数据包添加到队列，并可能调用插针的进程调度。

使用筛选器以中心处理的微型驱动程序不应直接使用流指针。 请参阅[筛选器以中心处理](filter-centric-processing.md)有关详细信息。

默认情况下，每个队列具有前导边缘流指针。 （可选） 它可以具有尾随边缘流指针，如果指定的尾随边标志。 微型驱动程序可以通过调用创建新流指针[ **KsStreamPointerClone**](https://msdn.microsoft.com/library/windows/hardware/ff567129)。

可以只在一个方向移动流指针： 到较新帧。 这称为前移流指针。

### <a name="advancing-a-stream-pointer"></a>改进的 Stream 指针

当前进流指针时，则将其移动到较新帧，或翻阅一定数量的其当前框架内的字节数。 例如，微型驱动程序可以继续学习流指针从第一个帧到达第二个帧到达。

若要前进的流指针，以固定为中心的筛选器可以通过调用[ **KsStreamPointerAdvance** ](https://msdn.microsoft.com/library/windows/hardware/ff567125)或[ **KsStreamPointerUnlock** ](https://msdn.microsoft.com/library/windows/hardware/ff567137)与*Eject*参数设置为**TRUE**。

### <a name="frame-reference-counts"></a>框架引用计数

使用流指针指向它们的帧进行引用计数，因为是在窗口之间的前导和尾随边缘中的帧。

完成流指针微型驱动程序时，它可以根据需要调用[ **KsStreamPointerSetStatusCode** ](https://msdn.microsoft.com/library/windows/hardware/ff567136)指定用来完成指定的 I/O 请求数据包 (IRP) 错误代码。 然后，微型驱动程序必须调用[ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130)。 AVStream 然后递减引用计数已删除的流指针之前引用的帧。 无法删除前导边缘，尾随边缘流指针。

 

 




