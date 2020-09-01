---
title: AVStream 中的数据范围交集
description: AVStream 中的数据范围交集
ms.assetid: 44281574-8258-47a3-857d-fd44bb949f17
keywords:
- 数据交集 WDK AVStream
- 交集 WDK AVStream
- 数据格式 WDK AVStream
- 数据范围 WDK AVStream
- 范围 WDK AVStream
- 格式化 WDK AVStream
- 固定数据范围 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab9d2104fb4ff72f4ff870a7cefe4e3a459399c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193049"
---
# <a name="data-range-intersections-in-avstream"></a>AVStream 中的数据范围交集





数据格式是一组描述连接的某些方面的参数。 例如，音频数据格式可能会指定特定格式的音频，每秒 X 个样本和每个样本的 Y 位。

数据范围指定有效参数序列。 例如，音频数据范围可以指定特定格式的音频，每秒 A-B 个样本，每个样本有3-D 位。

微型驱动程序为相应的[**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构的**DataRanges**成员中的特定 pin 提供其支持的数据范围列表。

在 AVStream 中，微型驱动程序可以提供自己的数据范围交集处理程序，方法是在[**KSPIN \_ \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)的**IntersectHandler**成员中提供一个指向微型驱动程序提供的回调例程的指针 若要让 AVStream 与范围相交，请将此成员设置为 **NULL**。 请参阅 [*AVStrMiniIntersectHandlerEx*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksintersecthandlerex) ，了解如何定义回调例程。

如果微型驱动程序提供了交集处理程序，则当需要进行交集时，微型驱动程序会收到两个在主要类型、subformat 和说明符中匹配的数据区域。 此外，数据范围的必需属性也匹配。

如果在*AVStrMiniIntersectHandlerEx*回调例程的**Data**参数中提供了交集和足够的缓冲区空间，则交集例程将选择交集中的格式，并将其返回到**数据**所指向的缓冲区中的调用方。

如果两个数据范围不相交，则处理程序返回状态 " \_ 无 \_ 匹配"。

如果微型驱动程序指定了 [*AVStrMiniPinSetDataFormat*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat) 调度，则 AVStream 将调用此调度来通知微型驱动程序 AVStream 正在设置特定的 pin 格式。 提供一个指针，该指针指向[**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)结构的**SetDataFormat**成员中的*AVStrMiniPinSetDataFormat*回调例程。 作为 [stream 类](/windows-hardware/drivers/ddi/_stream/index) 的客户端的 (微型驱动程序 [**将接收 SRB \_ 设置 \_ 数据 \_ 格式**](./srb-set-data-format.md) ，而不是 *AVStrMiniPinSetDataFormat*。 ) 

微型驱动程序可以通过从 AVStrMiniPinSetDataFormat 返回 "无匹配" 状态来拒绝建议的格式 \_ \_ 。 *AVStrMiniPinSetDataFormat*

除了在创建 pin 之前对 [*AVStrMiniPinSetDataFormat*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat) 的初始调用以外，微型驱动程序还可以在 pin 转换为运行状态之前接收到第二个 *AVStrMiniPinSetDataFormat* 调用。 如果 AVStream 或 stream 类客户端是视频捕获微型驱动程序，而你收到此类通知，则 *此调度包含实际的 surface 参数*。 如果可能，微型驱动程序不应失败这一第二种格式更改。 不要假设发生第二次调度调用。

微型驱动程序应捕获上次成功的 *AVStrMiniPinSetDataFormat* 调度中包含的任何格式的数据。

 

