---
title: 内部帮助器方法
description: 传感器驱动程序支持多个内部帮助器方法，这些方法可执行轮询数据、设置属性、检索属性、更新设备状态和支持事件等任务。
ms.assetid: BF5956FE-E1B6-476A-9B6E-86B400DE0A20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 488f506dacdc475a60ddd7e5dbaec29273f880e3
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355997"
---
# <a name="internal-helper-methods"></a>内部帮助器方法

传感器驱动程序支持多个内部帮助器方法，这些方法可执行轮询数据、设置属性、检索属性、更新设备状态和支持事件等任务。

## <a name="supporting-device-state-updates-for-multi-sensor-devices"></a>支持多传感器设备的设备状态更新

传感器驱动程序支持为包含多个传感器的单个设备设置设备状态的方法。 伪代码使用 **DriverUpdateDeviceState** 方法对此进行演示。

```cpp
DriverUpdateDeviceState()
{
    if ((sensor device is intelligent (e.g. HID) ||
        (sensor device is simple (e.g. SPB))
    {

        // if no client is connected to any of the sensors on this device
        // then disconnect from the device
        flagConnected = false
        for (all sensors on device)
        {
            if (clientCount > 0)
            {
                flagConnected = true
            }
        }

        if (false == flagConnected)
        {
            Disconnect from device
            deviceState = deviceStateDisconnected
        }
        else
        {
            Connect to device
            deviceState = deviceStateConnected
        }
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
```

## <a name="internal-methods-for-intelligent-sensors"></a>智能传感器的内部方法

如果传感器驱动程序支持智能传感器 (如 HID) ，则可能包括对轮询数据、处理事件、检索属性、设置属性和管理电源的方法的支持。 伪代码使用 **HIDSensorPollData**、 **HIDSensorSetProperties**和 **HIDSensorGetProperties** 方法演示了这些任务。

```cpp
HIDSensorPollData(sensorID) // Driver issues USB/HID “GET_INPUT” command to the sensor device
{
    // the driver is making a request for polled data
    // if the sensor is in a READY state respond by sending
    // the data for this sensor asynchronously to the driver
    if (true == sensorReady)
    {
        sensorState = sensorStateReady
        sensorEvent = eventTypeDataPoll
    }
    else
    {
        Set sensorState = sensorStateNoData //or failure, or initializing, or not available as appropriate
        Set sensorEvent = eventTypeStateChange
    }

    Send async data to driver //received in driver by DDIHandleAsyncDataEvent()
}
```

```cpp
HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) //SET_FEATURE
{
    if (requestedRS == reportingStateAllEvents) //reporting state
    {
        Set effectiveRS = reportingStateAllEvents
    }
    else
    {
        Set effectiveRS = reportingStateNoEvents
    }

    if (requestedPS == powerStateFullPower) //power state
    {
        Set effectivePS = powerStateFullPower
    }
    else if (requestedPS == powerStateLowPower)
    {
        Set effectivePS = powerStateLowPower
    }
    else
    {
        Set effectivePS = powerStatePowerOff
    }

    if (can support requestedCRI)
    {
        Set effectiveCRI = requestedCRI
    }
    else
    {
        Set effectiveCRI = value that can be supported
    }

    if (can support requestedCS[])
    {
        Set effectiveCS[] = requestedCS[]
    }
    else
    {
        Set effectiveCS[] = values that can be supported
    }

    if (requestedLDA == locDesiredAccuracyHigh) //location desired accuracy
    {
        Set effectiveLDA = locDesiredAccuracyHigh
    }
    else
    {
        Set effectiveLDA = locDesiredAccuracyDefault
    }


}
```

```cpp
HIDSensorGetProperties(sensorID, RS, PS, CRI, CS[], LDA) //Driver issues USB/HID “GET_FEATURE” command to the sensor
{
    buffer.effectiveRS
    buffer.effectivePS
    buffer.effectiveCRI
    buffer.effectiveCS[]
    buffer.effectiveLDA

    // The sensor device can optionally also override the following properties
    buffer.sensorCategory
    buffer.sensorType
    buffer.minCRI
    buffer.persistentUniqueID
    buffer.sensorManufacturer
    buffer.sensorModel
    buffer.serialNumber
    buffer.friendlyName
    buffer.sensorDescription
    buffer.connectionType

    Send buffer to Driver
}
```

## <a name="internal-methods-for-simple-sensors"></a>简单传感器的内部方法

如果传感器驱动程序支持简单传感器 (如 SPB) ，则可能包括对轮询数据的方法的支持。 伪代码使用 **SpbSensorPollData** 方法演示了此任务。

```cpp
datafields[] SpbSensorPollData(sensorID)
{
    // the driver is making a request for polled data, respond
    // by returning the data for this sensor synchronously to the driver

    Query newDatafields[] synchronously from the device via SPB

    return newDatafields[]
}
```

## <a name="related-topics"></a>相关主题

[Windows 中的传感器和位置平台简介](/windows-hardware/drivers/sensors/)

[传感器驱动程序逻辑](/windows-hardware/drivers/sensors/driver-logic--pseudo-code-)
