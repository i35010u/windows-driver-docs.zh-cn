---
Description: 创建传感器设备
title: 创建传感器设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 741968915d47f5ef980e7b2327c2b9e3cba77c15
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349788"
---
# <a name="creating-the-sensor-devices"></a>创建传感器设备


传感器线路基于在其传感器数据工作表中提供的示例线路。 这些线路设计为与视差 BS2 可编程微控制器的每个传感器。

例如，以下线路关系图和图像显示了 Ultrasonic 距离传感器数据表：

![ultrasonic 距离传感器](images/ping_datasheet.png)

在此图中，Pin 15 BS2 上接收的传感器数据。 为每个传感器的固件是非常相似。 它包含两个主要功能：PollSensor 和 RetrieveInterval。

PollSensor 函数中找到的代码各不相同传感器传感器。 对于 Ultrasonic 距离传感器 PollSensor 函数与 ultrasonic transducer 发出 pulse，侦听的响应，然后测量要发生的响应所花费的时间。

```cpp
PollSensor:
  PULSOUT 15, 5
  PULSIN 15, 1, time
  cmDistance = cmConstant ** time
RETURN
```

RetrieveInterval 函数是完全相同的每个传感器。 此函数检索新的时间间隔数据包从 WPD 驱动程序 （如果其中一个已发送），然后相应地更新间隔属性在固件中。 如果没有时间间隔已收到来自驱动程序，RetrieveInterval 函数将调用默认超时值函数。 此函数将传送回 WPD 驱动程序的传感器数据。

```cpp
RetrieveInterval:
    SERIN 16, 16780, Interval, Timeout, [DEC NewInterval]   'Retrieve interval
    IF NewInterval >= 10 AND NewInterval <= 60000 THEN
      Interval = NewInterval
    ENDIF
RETURN
```

超时函数具有以下格式：

```cpp
Timeout:
  SEROUT 16, 16780, [DEC1 SensorID, DEC1 ElementSize, DEC1 ElementCount, DEC5 cmDistance, DEC5 Interval]
GOTO Main
```

请注意，超时函数会返回到主例程，调用 PollSensor。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





