---
title: Stream 更改
description: Stream 更改
ms.assetid: 3bd6a511-c602-4159-87b4-7e1e55c03b2e
keywords:
- 流更改 WDK DVD 解码器
- 设置格式的 WDK DVD 解码器
- 标头的 WDK DVD 解码器
- 流格式的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35e0355d9292b543a2f51570b30d96a5b6ad50e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534307"
---
# <a name="stream-changes"></a>Stream 更改





DVD 流的格式可能会在更改任何时间。 例如，音频流格式可以 AC3 和 LPCM 之间切换在播放期间。

包含在流中的每个数据样本[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)追加到它的结构。 此结构包含**OptionsFlags**成员。

与包含一个以下标志的标头关联的数据示例可能或不能包含 null 数据数据包或有效的数据。

以下值的 KSSTREAM\_标头**OptionsFlags**成员对 DVD 播放至关重要：

<a href="" id="ksstream-header-optionsf-datadiscontinuity"></a>**KSSTREAM\_标头\_OPTIONSF\_DATADISCONTINUITY**  
KSSTREAM\_标头\_OPTIONSF\_DATADISCONTINUITY 位指示紧随的示例，属于不同的来源 （或位置/位置） 的数据比前面的示例。 这表示任何处理已在使用必须完成前面的示例。 此位通常会出现在上一帧，因此，该值指示解码器应放弃上一帧并开始使用新的数据处理的中间。

<a href="" id="ksstream-header-optionsf-timediscontinuity"></a>**KSSTREAM\_标头\_OPTIONSF\_TIMEDISCONTINUITY**  
KSSTREAM\_标头\_OPTIONSF\_TIMEDISCONTINUITY 位指示将数据立即遵循此示例中的时间间隙。 例如，如果 DVD 流包含一个静态帧编码为单个我帧，解码器收到的所有数据对于 I 帧与最后一个样本包含 KSSTREAM\_标头\_OPTIONSF\_TIMEDISCONTINUITY 标志. 这表示，解码器应立即解码 I 帧并不等待 B 帧数据。

<a href="" id="ksstream-header-optionsf-typechanged"></a>**KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED**  
KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED 位指示连接与此标头的示例将一个新[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)块流。 这样可以动态更改的数据类型。 示例将更改视频的 4 x 3 为 16 x 9，或更改的音频从 AC3 pcm。 只有在处理之前包含新的格式设置块的数据包的所有数据时，解码器应使新的格式设置块的所有必要的更改。

微型驱动程序的流格式更改时，接收数据包中的使用 KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED 中的设置位**OptionsFlags** KSSTREAM成员\_数据包的标头结构。

微型驱动程序可能永远不会看到 KSSTREAM\_标头\_OPTIONSF\_TYPECHANGED 标志，如果没有正确公开其音频流支持的数据格式。

**正确公开流支持的数据格式包括两个步骤：**

1.  SRB\_获取\_流\_必须设置为流的信息处理程序**StreamFormatsArray**指针指向的数组**NumberOfFormatArrayEntries**指针，其中每个指向有效的格式块。

2.  SRB\_获取\_数据\_交集处理程序必须将复制到所提供的缓冲区对应于建议的格式的格式设置块。

视频格式更改还必须向 KSSTREAM 事件以指示已更改的视频格式的视频端口连接到发送信号。 微型驱动程序应使用[ **StreamClassStreamNotification**](https://msdn.microsoft.com/library/windows/hardware/ff568266)(SignalMultipleStreamEvents，pMyHwDevExt-&gt;pMyStreamObject，和我\_KSEVENTSETID\_VPNOTIFY、 KSEVENT\_VPNOTIFY\_格式) 实现此目的。

当某个参数的视频格式发生更改，如像素的纵横比，解码器接收格式设置块。 解码器应发出信号要重新协商的视频端口连接的视频端口。 解码器调用[ **StreamClassStreamNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff568266)与参数*SignalMultipleStreamEvents*。

DVD 解码器微型驱动程序必须支持用于在此事件指示[ **HW\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff559692)条目为视频端口的流。 事件设置的视频端口事件 ID [KSEVENTSETID\_VPNotify](https://msdn.microsoft.com/library/windows/hardware/ff561780)和事件 ID 是[ **KSEVENT\_VPNOTIFY\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff561933).

 

 




