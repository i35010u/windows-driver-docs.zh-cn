---
title: 驱动程序更新方法
description: 更新传感器驱动程序支持的方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa6f209775ef6fc3220d2f995b58221d0308c07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830971"
---
# <a name="driver-update-methods"></a>驱动程序更新方法

传感器驱动程序支持内部方法，这些方法可处理当前报表间隔的更新、更改敏感度等。 伪代码使用以下方法演示这一点：

- DriverUpdateCRI (sensorID) 
- DriverUpdateCS (sensorID) 
- DriverUpdateLDA (sensorID) 
- DriverUpdateSensorState (sensorID、state、events) 
- DriverUpdateDatafields (sensorID) 

## <a name="sensor-reporting-field-updates"></a>传感器报告-现场更新

**DriverUpdateCRI**、 **DriverUpdateCS** 和 **DriverUpdateLDA** 方法演示了驱动程序如何更新当前报表间隔、更改敏感度和位置数据准确性字段。

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

**DriverUpdateSensorState** 方法演示了驱动程序如何更新传感器事件报告和电源状态。

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

**DriverUpdateDatafields** 方法演示了驱动程序如何更新其数据字段。

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

[Windows 中的传感器和位置平台简介](./index.md)

[传感器驱动程序逻辑](./driver-logic--pseudo-code-.md)
