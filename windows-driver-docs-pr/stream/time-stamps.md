---
title: 时间戳
description: 时间戳
ms.assetid: a97a57df-294a-4cbb-85d3-56d33ece65c9
keywords:
- 视频捕获 WDK AVStream，时间戳
- 捕获视频 WDK AVStream，时间戳
- 时间戳 WDK 视频捕获
- 时钟 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 509b0a1b4879e0edb8474a971d8b2f0bdf20f801
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377741"
---
# <a name="time-stamps"></a>时间戳


微型驱动程序应该时间戳数据包来同步多个数据流。 内核模式时钟开始计数时它们先过渡带的时间**KSSTATE\_停止**状态。 此后，时钟将递增时间戳按规律性间隔的 100 纳秒为单位的流转换到直到**KSSTATE\_停止**状态。

传输的每个数据包对应于单个帧或视频或辅助数据字段。 涉及到帧精确视频捕获的视频捕获驱动程序编写人员可以选择提供所有其他筛选器可用作参考的时钟。 数字视频的微型驱动程序是应提供时钟，以使用筛选器关系图中的微型驱动程序的一个示例。 或者，运行以异步方式向其他多媒体流，如 USB 和 IEEE 1394 会议摄像机的视频捕获微型驱动程序应时间的戳与时钟其数据数据包提供的另一个组件，例如音频数字化器。

如果 Stream 类微型驱动程序提供了主时钟，还应指定以下值中的[ **HW\_流\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_object)结构：

```cpp
PHW_STREAM_OBJECT *pStreamObject;
 
PStreamObject->HWClockFunction = (PHW_CLOCK_FUNCTION)StreamClockRoutine;
PStreamObject->ClockSupportFlags = CLOCK_SUPPORT_CAN_READ_ONBOARD_CLOCK | CLOCK_SUPPORT_CAN_RETURN_STREAM_TIME;
```

 

 




