---
title: 驱动程序更新方法
ms.assetid: F809BCE4-9176-4503-9EC7-B80AC229ABB5
description: 更新传感器驱动程序支持的方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c6b99dea76757168550bb276174d27be532e4d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524116"
---
# <a name="driver-update-methods"></a>驱动程序更新方法


传感器驱动程序支持内部方法处理更新到当前报告间隔、 更改敏感度，等等。 伪代码演示了这可以通过使用以下方法：

-   DriverUpdateCRI(sensorID)
-   DriverUpdateCS(sensorID)
-   DriverUpdateLDA(sensorID)
-   DriverUpdateSensorState （sensorID、 状态、 事件）
-   DriverUpdateDatafields(sensorID)

## <a name="sensor-reporting-field-updates"></a>传感器报告字段更新


**DriverUpdateCRI**， **DriverUpdateCS**，并**DriverUpdateLDA**方法演示如何将驱动程序更新当前报告间隔、 变化敏感度和位置数据准确性字段。

```cpp
DriverUpdateCRI(sensorID)
{
    if (true == flagCRI)
    {
        // Note that only the clients that have specified a CRI are considered
        // when determining which client has the lowest requested CRI
        Set selectedCRI of sensorID device to lowest of clientCRIs

        if (selectedCRI < effectiveMinCRI)
        {
            selectedCRI = effectiveMinCRI
        }
    }
    else //no client has specified a CRI
    {
        selectedCRI = defaultCRI
    }

    effectiveCRI = DriverUpdateSensorDeviceCRI(sensorID, selectedCRI)
}
```

```cpp
DriverUpdateCS(sensorID)
{
    for (each datafield supported by sensorID)
    {
        if (true == flagCS)
        {
            // Note that only the clients that have specified a CS are considered
            // when determining which client has the lowest requested CS
            Set selectedCS[n] of sensorID device to lowest of clientCS[n]
        }
        else //no client has specified a CS
        {
            selectedCS[n] = defaultCS[n]
        }
    }

    effectiveCS[] = DriverUpdateSensorDeviceCS(sensorID, selectedCS[])
}
```

```cpp
DriverUpdateLDA(sensorID)
{
    if (true == flagLDA)
    {
        // Note that only the clients that have specified an LDAare considered
        // when determining which client has the lowest (most accurate) requested LDA
        Set selectedLDA of sensorID device to lowest (most accurate) of clientLDAs
    }
    else //no client has specified a LDA
    {
        selectedLDA = defaultLDA
    }

    effectiveLDA = DriverUpdateSensorDeviceLDA(sensorID, selectedLDA)
}
```

## <a name="sensor-state-updates"></a>传感器状态更新


**DriverUpdateSensorState**方法演示如何将驱动程序更新传感器事件报告和电源状态。

```cpp
DriverUpdateSensorState(sensorID)
{
    if (clientCount == 0) // no clients
    {
        if (subscriberCount == 0) //no subscribers
        {
            selectedRS = reportingStateNoEvents
            selectedPS = powerStatePowerOff
        }
        else //has subscribers
        {
            //illegal state
            selectedRS = reportingStateNoEvents
            selectedPS = powerStatePowerOff
        }
    }
    else //has clients
    {
        if (subscriberCount == 0) //no subscribers
        {
            if (true == flagCRI)
            {
                selectedRS = reportingStateAllEvents
                selectedPS = powerStateFullPower
            }
            else
            {
                selectedRS = reportingStateNoEvents
                selectedPS = powerStateLowPower
            }
            else

        }
        else //has subscribers
        {
            selectedRS = reportingStateAllEvents
            selectedPS = powerStateFullPower
        }
    }

    effectiveRS = DriverUpdateSensorDeviceRS(sensorID, selectedRS)
    effectivePS = DriverUpdateSensorDevicePS(sensorID, selectedPS)
}
```

## <a name="data-field-updates"></a>数据字段更新


**DriverUpdateDatafields**方法演示了一个驱动程序更新其数据字段的方式。

```cpp
DriverUpdateDatafields(sensorID)
{
    if (effectiveRS == eventsOff)
    {
        if (sensor device is intelligent (ex. HID))
        {
            HIDSensorPollData(sensorID)

            // a poll response by the sensor device will happen asynchronously
            // the sensor device responds to this poll request by sending an
            // input packed, and this is received in the
            // DriverHandleAsyncDataEvent() just as any other data packet
            // is received
        }
        else if (sensor device is simple (ex. SPB))
        {
            currentDatafields[] = SpbSensorPollData(sensorID)

            // ** TODO: Data is not updated asynchronously when polled
            // ** via SPB. Datafields[] must be assigned similarly to
            // ** DDIHandleAsyncDataEvent() when that logic has been
            // ** finalized. A shared helper method is likely best.
        }
        else if (sensor device is fusion)
        {
            //handle fusion sensor
        }
        else //is some other kind of sensor
        {
            //special action
        }
    }
    else
    {
        // datafields are being updated by events
        // (i.e. DDIHandleAsyncDataEvent)
    }
}
```

## <a name="related-topics"></a>相关主题
[传感器驱动程序开发的基础知识](sensor-driver-development-basics.md)



