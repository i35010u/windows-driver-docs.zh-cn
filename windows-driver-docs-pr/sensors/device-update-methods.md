---
title: 设备更新方法
ms.assetid: EB5158D7-6ACA-42BB-89E2-0937EAB94BA2
description: 传感器驱动程序支持的用于更新传感器设备的方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da81b2731b4ca99cc8886e8ccf6178f80b680b54
ms.sourcegitcommit: b75e9940d49410e2b952e96f325df67a039cd571
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92336963"
---
# <a name="device-update-methods"></a>设备更新方法

传感器驱动程序支持更新传感器设备的方法。 伪代码使用以下方法演示这一点：

- DriverUpdateDeviceCRI
- DriverUpdateDeviceCS
- DriverUpdateDeviceLDA
- DriverUpdateDeviceRS
- DriverUpdateDevicePS

## <a name="device-reporting-reporting-updates"></a>设备报表报表更新

**DriverUpdateDeviceCRI**、 **DriverUpdateDeviceCS**和**DriverUpdateDeviceLDA**方法演示了驱动程序如何更新设备上的当前报表间隔、更改敏感度和位置数据准确性字段。

```cpp
effectiveCRI DriverUpdateDeviceCRI(sensorID, requestedCRI)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) //Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set CRI via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectiveCRI
}
```

```cpp
effectiveCS[] DriverUpdateDeviceCS(sensorID, requestedCSs)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set CS via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectiveCS[]
}
```

```cpp
effectiveLDA DriverUpdateDeviceLDA(sensorID, requestedLDA)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set LDA via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectiveLDA
}
```

## <a name="device-interrupt-updates"></a>设备中断更新

**DriverUpdateDeviceRS**方法演示驱动程序如何启用或禁用设备上的中断。

```cpp
effectiveRS DriverUpdateDeviceRS(sensorID, requestedRS)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        if (requestedRS == quiescent)
        {
            Disable SPB device interrupts
        }
        else if (requestedRS == eventing)
        {
            Enable SPB device interrupts for eventing
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

    return effectiveRS
}
```

## <a name="device-power-state-updates"></a>设备电源状态更新

**DriverUpdateDevicePS**方法演示驱动程序如何设置设备的电源状态。

```cpp
effectivePS DriverUpdateDevicePS(sensorID, requestedPS)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set power state via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectivePS
}
```

## <a name="related-topics"></a>相关主题

[传感器驱动程序逻辑](/windows-hardware/drivers/sensors/driver-logic--pseudo-code-)
