---
title: 设备更新方法
ms.assetid: EB5158D7-6ACA-42BB-89E2-0937EAB94BA2
description: 支持的传感器驱动程序，以更新传感器设备的方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d20b4d4e9dfe740e9a22c22c80a1d3921568435
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362285"
---
# <a name="device-update-methods"></a>设备更新方法


传感器驱动程序支持更新传感器设备的方法。 伪代码演示了这可以通过使用以下方法：

-   DriverUpdateDeviceCRI
-   DriverUpdateDeviceCS
-   DriverUpdateDeviceLDA
-   DriverUpdateDeviceRS
-   DriverUpdateDevicePS

## <a name="device-reporting-reporting-updates"></a>Reporting 报告更新的设备


**DriverUpdateDeviceCRI**， **DriverUpdateDeviceCS**，并**DriverUpdateDeviceLDA**方法演示如何将驱动程序更新当前报告间隔，更改敏感度，并在设备上的位置数据准确性字段。

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


**DriverUpdateDeviceRS**方法演示了如何将驱动程序启用或禁用设备上的中断。

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


**DriverUpdateDevicePS**方法演示了如何将驱动程序设置设备上的电源状态。

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
[传感器驱动程序开发的基础知识](sensor-driver-development-basics.md)



