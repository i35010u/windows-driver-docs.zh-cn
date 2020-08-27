---
description: 创建传感器设备
title: 创建传感器设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31925027973ed4ee345890098ce5ba6e3bb2225d
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968918"
---
# <a name="creating-the-sensor-devices"></a>创建传感器设备


传感器线路基于其传感器数据表中的视差提供的示例线路。 这些线路旨在将每个传感器与视差 BS2 可编程微控制器集成。

例如，"Ultrasonic 距离" 传感器的数据表显示以下线路图和图像：

![ultrasonic 距离传感器](images/ping_datasheet.png)

在此图中，BS2 上的引脚15接收传感器数据。 每个传感器的固件非常类似。 它包含两个主要函数： PollSensor 和 RetrieveInterval。

PollSensor 函数中找到的代码随传感器的不同而异。 对于 Ultrasonic 距离传感器，PollSensor 函数会发出与 Ultrasonic 传感器的脉冲，侦听响应，然后测量响应发生所需要的时间时间。

```cpp
PollSensor:
  PULSOUT 15, 5
  PULSIN 15, 1, time
  cmDistance = cmConstant ** time
RETURN
```

每个传感器的 RetrieveInterval 函数都是相同的。 此函数从 WPD 驱动程序检索新的间隔数据包 (如果) 发送了该驱动程序，然后在固件中相应地更新 interval 属性。 如果未收到驱动程序的间隔，则 RetrieveInterval 函数将调用默认超时函数。 此函数将传感器数据传输回 WPD 驱动程序。

```cpp
RetrieveInterval:
    SERIN 16, 16780, Interval, Timeout, [DEC NewInterval]   'Retrieve interval
    IF NewInterval >= 10 AND NewInterval <= 60000 THEN
      Interval = NewInterval
    ENDIF
RETURN
```

Timeout 函数的格式如下：

```cpp
Timeout:
  SEROUT 16, 16780, [DEC1 SensorID, DEC1 ElementSize, DEC1 ElementCount, DEC5 cmDistance, DEC5 Interval]
GOTO Main
```

请注意，Timeout 函数返回到调用 PollSensor 的主例程。

```cpp
Main:
  GOSUB PollSensor                   'Determine distance
  GOSUB RetrieveInterval             'Retrieve interval data
```

下面是 ultrasonic 距离传感器的完整源代码：

```cpp
' Smart Sensors and Applications - PingMeasureCmAndIn.bs2
' Measure distance with Ping))) sensor and display in both in & cm
' {$STAMP BS2}
' {$PBASIC 2.5}
' Conversion constants for room temperature measurements.
CmConstant CON 2260
'InConstant CON 890
cmDistance VAR Word
'inDistance VAR Word
time VAR Word
SensorID  VAR   Byte  'Sensor identifier = 5 for PIR
ElementSize VAR Byte  'Size (in bytes) of each element
ElementCount  VAR   Byte  'Count of elements in packet
Padding VAR Byte      'Padding for the 8-byte element

SensorID = 4
ElementSize = 1
ElementCount = 5      '5bytes for distance data

NewInterval VAR  Word  'New interval requested by user
Interval  VAR   Word   'Interval value utlized by firmware

Interval = 2000
NewInterval = 2000


Main:
  GOSUB PollSensor                  'Was motion detected?
  GOSUB RetrieveInterval            'Retrieve units data

Timeout:
  SEROUT 16, 16780, [DEC1 SensorID, DEC1 ElementSize, DEC1 ElementCount, DEC5 cmDistance, DEC5 Interval]
GOTO Main

PollSensor:
  PULSOUT 15, 5
  PULSIN 15, 1, time
  cmDistance = cmConstant ** time
RETURN

RetrieveInterval:
    SERIN 16, 16780, Interval, Timeout, [DEC NewInterval]   'Retrieve interval
    IF NewInterval >= 10 AND NewInterval <= 60000 THEN
      Interval = NewInterval
    ENDIF
RETURN
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





