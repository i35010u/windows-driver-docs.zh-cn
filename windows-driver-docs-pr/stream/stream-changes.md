---
title: 流更改
description: 流更改
keywords:
- 流更改 WDK DVD 解码器
- 格式化 WDK DVD 解码器
- 标头 WDK DVD 解码器
- 流格式化 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a63e5c469341b97aee38209dc824c145201b8b70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805927"
---
# <a name="stream-changes"></a>流更改





DVD 流的格式可能会随时更改。 例如，播放期间，音频流格式在 E-AC3 和 LPCM 之间可能会更改。

流中的每个数据样本都包含附加到它的 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header) 结构。 此结构包含 **OptionsFlags** 成员。

与包含以下标志之一的标头关联的数据示例可以包含空数据数据包，也可以不包含有效数据。

KSSTREAM \_ 标头 **OptionsFlags** 成员的以下值对于 DVD 播放很重要：

<a href="" id="ksstream-header-optionsf-datadiscontinuity"></a>**KSSTREAM \_ 标头 \_ OPTIONSF \_ DATADISCONTINUITY**  
KSSTREAM \_ 标头 \_ OPTIONSF \_ DATADISCONTINUITY 位指示其后面紧跟的示例属于与上一个示例不同 (或位置/位置) 的数据。 这表明，使用前面的示例进行的任何处理都必须完成。 此位通常出现在上一帧的中间，这表示解码器应丢弃上一个帧并开始使用新数据进行处理。

<a href="" id="ksstream-header-optionsf-timediscontinuity"></a>**KSSTREAM \_ 标头 \_ OPTIONSF \_ TIMEDISCONTINUITY**  
KSSTREAM \_ 标头 \_ OPTIONSF \_ TIMEDISCONTINUITY 位表示在此示例之后的数据中将存在时间间隔。 例如，如果 DVD 流包含编码为单个 I 帧的静止帧，则解码器会收到 I 帧的所有数据，其中最后一个包含 KSSTREAM \_ 标头 \_ OPTIONSF \_ TIMEDISCONTINUITY 标志的示例。 这表明解码器应该立即解码 I 帧，而不是等待 B 帧数据。

<a href="" id="ksstream-header-optionsf-typechanged"></a>**KSSTREAM \_ 标头 \_ OPTIONSF \_ TYPECHANGED**  
KSSTREAM \_ 标头 \_ OPTIONSF \_ TYPECHANGED 位表示与标头连接的示例将成为流的新 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 块。 这允许动态更改数据类型。 例如，将视频从4x3 更改为16x9，或将音频从 E-AC3 更改为 PCM。 只有在处理具有新格式块的数据包之前的所有数据后，解码器才能对新格式块进行所有必要的更改。

当流格式发生变化时，微型驱动程序接收数据包，该数据包具有在 \_ 数据包的 \_ \_ OptionsFlags 标头结构的 **KSSTREAM** 成员中设置的 KSSTREAM 标头 OPTIONSF TYPECHANGED 位 \_ 。

\_ \_ \_ 如果微型驱动程序未正确公开其音频流支持的数据格式，则不能看到 KSSTREAM 标头 OPTIONSF TYPECHANGED 标志。

**正确公开流支持的数据格式涉及两个步骤：**

1.  流的 SRB \_ 获取 \_ 流 \_ 信息处理程序必须将 **StreamFormatsArray** 指针设置为指向 **NumberOfFormatArrayEntries** 指针的数组，其中每个都指向有效的格式块。

2.  SRB \_ 获取 \_ 数据 \_ 交集处理程序必须将与所建议格式相对应的格式块复制到提供的缓冲区中。

视频格式更改还必须向视频端口连接发送 KSSTREAM 事件，以指示视频格式已更改。 微型驱动程序应使用 [**StreamClassStreamNotification**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification) (SignalMultipleStreamEvents、pMyHwDevExt- &gt; pMyStreamObject &我 \_ \_ 的 KSEVENTSETID VPNOTIFY，KSEVENT \_ VPNOTIFY \_ FORMATCHANGE) 实现此目的。

当视频格式的某些参数发生变化时，如像素纵横比，解码器将接收格式块。 解码器应指示视频端口重新协商视频端口连接。 解码器用参数 *SignalMultipleStreamEvents* 调用 [**StreamClassStreamNotification**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification) 。

DVD 解码器微型驱动程序必须指明为 VideoPort 流的 [**HW \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information) 条目中的此事件提供支持。 视频端口事件的事件集 ID 为 [KSEVENTSETID \_ VPNotify](./kseventsetid-vpnotify.md) ，事件 id 为 [**KSEVENT \_ VPNotify \_ FORMATCHANGE**](./ksevent-vpnotify-formatchange.md)。

 

