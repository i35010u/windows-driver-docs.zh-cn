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
ms.openlocfilehash: 34b825004033204c86704bc4edc5d2c8e8fde762
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187345"
---
# <a name="time-stamps"></a>时间戳


微型驱动程序应将数据包时间戳以同步多个数据流。 当第一次转换为 **KSSTATE \_ 停止** 状态时，内核模式时钟开始计算时间。 此后，时钟周期应以100毫微秒单位的固定间隔递增时间戳，直到流转换到 **KSSTATE \_ 停止** 状态。

传输的每个数据包都对应于一个帧或视频或辅助数据的一个字段。 与帧准确视频捕获相关的视频捕获驱动程序编写器可以选择提供所有其他筛选器都可用作参考的时钟。 数字视频微型驱动程序是应提供要在筛选器图中使用的时钟的微型驱动程序示例。 此外，视频捕获微型驱动程序（以异步方式运行到其他多媒体流，如 USB 和 IEEE 1394 摄像机）应使用另一个组件（如音频数字化仪）提供的时钟来标记其数据包。

如果 Stream 类微型驱动程序提供主时钟，则它应在 [**HW \_ 流 \_ 对象**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object) 结构中指定以下值：

```cpp
PHW_STREAM_OBJECT *pStreamObject;
 
PStreamObject->HWClockFunction = (PHW_CLOCK_FUNCTION)StreamClockRoutine;
PStreamObject->ClockSupportFlags = CLOCK_SUPPORT_CAN_READ_ONBOARD_CLOCK | CLOCK_SUPPORT_CAN_RETURN_STREAM_TIME;
```

 

