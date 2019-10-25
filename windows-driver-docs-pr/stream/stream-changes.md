---
title: 流更改
description: 流更改
ms.assetid: 3bd6a511-c602-4159-87b4-7e1e55c03b2e
keywords:
- 流更改 WDK DVD 解码器
- 格式化 WDK DVD 解码器
- 标头 WDK DVD 解码器
- 流格式化 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 220ef48d354ed5c0efc843e7af513b0bd05ae7aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837690"
---
# <a name="stream-changes"></a>流更改





DVD 流的格式可能会随时更改。 例如，播放期间，音频流格式在 E-AC3 和 LPCM 之间可能会更改。

流中的每个数据样本都包含附加了[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构。 此结构包含**OptionsFlags**成员。

与包含以下标志之一的标头关联的数据示例可以包含空数据数据包，也可以不包含有效数据。

以下 KSSTREAM\_标头**OptionsFlags**成员的值对于 DVD 播放很重要：

<a href="" id="ksstream-header-optionsf-datadiscontinuity"></a>**KSSTREAM\_标头\_OPTIONSF\_DATADISCONTINUITY**  
KSSTREAM\_标头\_OPTIONSF\_DATADISCONTINUITY 位指示紧随前面的示例的数据所属的数据源（或位置）不同。 这表明，使用前面的示例进行的任何处理都必须完成。 此位通常出现在上一帧的中间，这表示解码器应丢弃上一个帧并开始使用新数据进行处理。

<a href="" id="ksstream-header-optionsf-timediscontinuity"></a>**KSSTREAM\_标头\_OPTIONSF\_TIMEDISCONTINUITY**  
KSSTREAM\_标头\_OPTIONSF\_TIMEDISCONTINUITY 位表示在此示例之后的数据中将存在时间间隔。 例如，如果 DVD 流包含编码为单个 I 帧的静止帧，则解码器将收到 I 帧的所有数据，其中包含 KSSTREAM\_标头的最后一个示例\_OPTIONSF\_TIMEDISCONTINUITY 标志。 这表明解码器应该立即解码 I 帧，而不是等待 B 帧数据。

<a href="" id="ksstream-header-optionsf-typechanged"></a>**KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED**  
KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED 位指示与标头连接的示例将成为流的新[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)块。 这允许动态更改数据类型。 例如，将视频从4x3 更改为16x9，或将音频从 E-AC3 更改为 PCM。 只有在处理具有新格式块的数据包之前的所有数据后，解码器才能对新格式块进行所有必要的更改。

当流格式发生变化时，微型驱动程序接收数据包，其中包含 KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED 位，该数据包是在数据包的 OPTIONSFLAGS\_标头结构的**KSSTREAM**成员中设置的。

如果未正确地公开其音频流支持的数据格式，则微型驱动程序可能无法看到 KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED 标志。

**正确公开流支持的数据格式涉及两个步骤：**

1.  SRB\_获取流的\_流\_信息处理程序必须将**StreamFormatsArray**指针设置为指向**NumberOfFormatArrayEntries**指针的数组，其中每个都指向有效的格式块。

2.  SRB\_获取\_数据\_交集处理程序必须将与所建议格式相对应的格式块复制到提供的缓冲区中。

视频格式更改还必须向视频端口连接发送 KSSTREAM 事件，以指示视频格式已更改。 微型驱动程序应使用[**StreamClassStreamNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)（SignalMultipleStreamEvents，pMyHwDevExt-&gt;pMyStreamObject，& 我的\_KSEVENTSETID\_VPNOTIFY，KSEVENT\_VPNOTIFY\_FORMATCHANGE）用途.

当视频格式的某些参数发生变化时，如像素纵横比，解码器将接收格式块。 解码器应指示视频端口重新协商视频端口连接。 解码器用参数*SignalMultipleStreamEvents*调用[**StreamClassStreamNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification) 。

DVD 解码器微型驱动程序必须指明为 VideoPort 流的[**HW\_STREAM\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)条目中的此事件提供支持。 视频端口事件的事件集 ID 是[KSEVENTSETID\_VPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify) ，事件 ID 为[**KSEVENT\_VPNotify\_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vpnotify-formatchange)。

 

 




