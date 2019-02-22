---
title: 设备方法
description: 传感器固件支持执行任务，例如支持事件和管理电源的几个帮助器方法。
ms.assetid: 4F1463B0-A307-4C70-A660-18AD876B3363
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d505461c005775b77f2055ff4aafd994245ad8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542200"
---
# <a name="device-methods"></a>设备方法


传感器固件支持执行任务，例如支持事件和管理电源的几个帮助器方法。

## <a name="device-methods-for-intelligent-sensors"></a>智能传感器的设备方法


对于智能传感器 （如 HID) 固件包括支持处理事件和管理能力的方法。 伪代码演示如何使用这些任务**HIDSensorDeviceEvent**并**HIDDeviceManagePower**方法。

```cpp
HIDSensorDeviceEvent(sensorID) // Driver issues USB/HID “SEND_INPUT” command to the sensor
{
    // an event has occurred on the sensor device
    // this could be one of several things, not only just a data update event
    if (event == eventData) //ex data change exceeded effectiveCS[]
    {
        if (effectiveRS = reportingStateAllEvents)
        {
            Set sensorState = sensorStateReady
            Set sensorEvent = eventTypeCS (or data update as appropriate)
            Send async data to driver //received in driver by DDIHandleAsyncDataEvent()
        }
        else
        {
            //do nothing
        }
    }
    else if (event == eventStateChange)
    {
        // if this event is not a data update event
        // then no matter what the reporting state and
        // power state (as long as power is on)
        // of the device then send the event
        // to the driver
        Set sensorState = current sensor state
        Set sensorEvent = type for this event
        Send async data to driver //received in driver by DDIHandleAsyncDataEvent()
    }
}
```

```cpp
HIDDeviceManagePower(powerState)
{
    if (powerstate for all sensors is == powerStatePowerOff)
    {
        Turn the power off to all sensors
        Turn off power to the device
    }
    else if (powerState for any sensor is >= powerStateLowPower)
    {
        Turn on power to the device
        Turn on power to the sensor
        sensorState = sensorStateInitializing
        Send sensor state to sensor asynchronously using SEND_INPUT USB/HID command

        Initialize the sensor
        if (sensor is ready)
        {
            Set sensorState = sensorStateReady
            Send sensorState to sensor asynchronously using SEND_INPUT USB/HID command
        }
        else if (sensor is never is initialized and becomes ready)
        {
            Set sensorState = sensorStateError
            Send sensorstate to sensor asynchronously using SEND_INPUT USB/HID command
        }
    }
}
```

## <a name="device-methods-for-simple-sensors"></a>简单的传感器的设备方法


对于简单传感器 （如存储） 固件包括处理事件的方法的支持。 伪代码演示了如何在此任务使用**SpbSensorDeviceEvent**。

```cpp
SpbSensorDeviceEvent(sensorID)
{
    // an interrupt has occurred on the sensor device
    // this could be one of several things, not only just a data update event
    if (event == eventData) //ex data change exceeded effectiveCS[]
    {
        if (effectiveRS = reportingStateAllEvents)
        {
            Acknowledge device interrupt
            Query data synchronously from the device via SPB

            Set sensorState = sensorStateReady
            Set sensorEvent = eventTypeCS (or data update as appropriate)

            Invoke DDIHandleAsyncDataEvent(sensorID)
        }
        else
        {
            //do nothing
        }
    }
    else if (event == eventStateChange)
    {
        // if this event is not a data update event
        // then no matter what the reporting state and
        // power state (as long as power is on)
        // of the device then send the event
        // to the driver. Note not all simple devices
        // will support state change eventing.

        Acknowledge device interrupt
        Query state synchronously from the device via SPB

        Set sensorState = current sensor state
        Set sensorEvent = type for this event
    }
}
```

 

 




