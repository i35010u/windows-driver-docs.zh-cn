---
title: AVStream 中的数据范围交集
description: AVStream 中的数据范围交集
ms.assetid: 44281574-8258-47a3-857d-fd44bb949f17
keywords:
- 数据交集 WDK AVStream
- 交集 WDK AVStream
- 数据格式以 WDK AVStream
- 数据范围 WDK AVStream
- 范围 WDK AVStream
- 格式 WDK AVStream
- 将数据区域固定 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba6d8656959f8125ef7da6d970b153d773317042
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563219"
---
# <a name="data-range-intersections-in-avstream"></a>AVStream 中的数据范围交集





数据格式是一组描述连接的某些方面的参数。 例如，音频数据格式可能会指定特定格式的音频 X 每秒的示例和每个样本的 Y 位。

数据区域，指定有效参数的顺序。 例如，音频数据范围可以指定特定格式的音频在每个样本的第二个和 C D 位每一个 B 示例。

微型驱动程序提供了一系列支持的特定 pin 中的数据范围**DataRanges**的相应成员[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)结构。

在 AVStream，微型驱动程序可以通过提供指向提供微型驱动程序的回调例程中提供自己的数据范围的交集处理程序**IntersectHandler**的成员[ **KSPIN\_描述符\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)。 若要使 AVStream 相交范围，请将此成员设置为**NULL**。 请参阅[ *AVStrMiniIntersectHandlerEx* ](https://msdn.microsoft.com/library/windows/hardware/ff556326)若要了解如何定义的回调例程。

如果微型驱动程序提供 intersect 处理程序，当交集需要进行时，微型驱动程序收到与匹配的两个数据区域中主要类型、 子格式和说明符。 此外，与匹配的数据范围所需的属性。

如果范围相交和中提供足够的缓冲区空间**数据**的参数*AVStrMiniIntersectHandlerEx*回调例程交集例程选择中的格式交集，并返回到调用方缓冲区中指向**数据**。

如果两个数据区域不相交，该处理程序将返回状态\_否\_匹配项。

如果已指定微型驱动程序[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)调度，则 AVStream 调用此调度通知微型驱动程序 AVStream 在针上设置特定的格式。 提供一个指向你*AVStrMiniPinSetDataFormat*中的回调例程**SetDataFormat**的成员[ **KSPIN\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff563535)结构。 (客户端的微型驱动程序[流式传输类](https://msdn.microsoft.com/library/windows/hardware/ff568275)接收[ **SRB\_设置\_数据\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff568201)而不是*AVStrMiniPinSetDataFormat*。)

微型驱动程序可以通过返回状态来拒绝建议的格式\_否\_与来自*AVStrMiniPinSetDataFormat*。

首次调用除了[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)创建 pin 之前，你的微型驱动程序可能会收到第二个*AVStrMiniPinSetDataFormat*调用之前，pin 将转换为运行状态。 如果 AVStream 或流类客户端是视频捕获微型驱动程序和接收此类通知*此调度包含实际的图面上参数*。 如果可能，微型驱动程序不应失败这第二种格式更改。 不要假定第二个调度调用将会发生。

微型驱动程序应捕获数据中任何格式已包含在上次成功*AVStrMiniPinSetDataFormat*调度。

 

 




