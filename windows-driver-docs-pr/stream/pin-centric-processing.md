---
title: 以引脚为中心的处理
description: 以引脚为中心的处理
ms.assetid: 0b6a02c2-e672-4568-a890-491c721ec3a7
keywords:
- pin 为中心的筛选器 WDK AVStream
- Pin 为中心的 AVStream 筛选 WDK
- 筛选器类型 WDK AVStream
- AVStrMiniPinProcess
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2c620769f218553577cedd85accf4b4bdbefcc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568645"
---
# <a name="pin-centric-processing"></a>以引脚为中心的处理





在编写 AVStream 微型驱动程序时，您提供筛选器，使用两种处理模式之一： pin 为中心的处理或[筛选器以中心处理](filter-centric-processing.md)。

Pin 为中心处理意味着 AVStream 调用微型驱动程序的 pin 过程调度例程，新帧到达 pin 队列中时。

筛选器以中心处理意味着 AVStream 调用微型驱动程序的筛选器过程调度例程，有的数据帧可用时的每个实例化的插针。 请注意，这些定义指定默认行为;微型驱动程序可以通过设置标志来修改默认行为[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。

一般情况下，软件筛选器使用筛选器为中心的处理和硬件筛选器使用 pin 以为中心的处理。 例如，转换或将数据呈现的硬件无法将数据路由上的 pin 以为中心的筛选器。 有极少数情况下可能会在其中撤消这些角色。

若要提供 pin 为中心的筛选器，微型驱动程序提供一个指针指向*AVStrMiniPinProcess*中每个回调例程[ **KSPIN\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff563535)结构;未提供在处理调度[ **KSFILTER\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff562554)结构。

如果微型驱动程序不会修改标志设置中 KSPIN\_描述符\_AVStream 调用供应商提供结构，例如[ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)回调例程在三种情况下：

-   Pin 转换到的最小处理状态。 框架必须已经存在于队列和 pin 必须从转换到的最小处理状态小于至少最小处理状态。

-   到达新帧。 Pin 必须为至少最低的处理状态并且必须在或领先领先于无框架。

-   微型驱动程序显式调用[ **KsPinAttemptProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff563494)。

默认情况下暂停是最小处理状态。

此外，AVStream 不会调用 pin 过程调度如果 pin 的 AND 门已关闭。 如果使用 **KSGATE * * * Xxx*例程，从而添加其他关闭输入插针的并且入口，例如，不会调用过程调度。

当调用 AVStream *AVStrMiniPinProcess*，它提供了指向具有可用的数据的固定对象的指针。 然后可以获取微型驱动程序的处理调度[前沿指针](leading-and-trailing-edge-stream-pointers.md)通过调用[ **KsPinGetLeadingEdgeStreamPointer**](https://msdn.microsoft.com/library/windows/hardware/ff563513)。 微型驱动程序然后处理流数据使用[流指针](stream-pointers.md)API。

使用 pin 以中心处理的微型驱动程序可以修改当调用 AVStream *AVStrMiniPinProcess*中的相关设置标志的调度[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。 标志说明 KSPIN\_描述符\_EX 参考页是专门针对供应商要实现 pin 为中心的筛选器。

如果持有微型驱动程序处理尝试可能会失败[处理 mutex](processing-mutex-in-avstream.md)通过[ **KsPinAcquireProcessingMutex**](https://msdn.microsoft.com/library/windows/hardware/ff563488)。 如果微型驱动程序直接操作使用的入口，可能还会出现问题 **KSGATE * * *\** 调用。

[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083) Windows 驱动程序工具包示例中是模拟的硬件的 pin 以中心捕获驱动程序。 Avshws 示例演示如何实现[AVStream 通过 DMA](avstream-dma-services.md)。

 

 




