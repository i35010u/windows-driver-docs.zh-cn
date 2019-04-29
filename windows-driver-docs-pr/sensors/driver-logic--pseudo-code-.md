---
title: 传感器驱动程序逻辑
description: 本部分介绍关键驱动程序逻辑或任务形式的伪代码。
ms.assetid: 4B14C515-1B79-4B67-BA9A-365B2D6C0F07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c36e299afa4e7d9480b7eee9c16e795ad3543e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377817"
---
# <a name="sensor-driver-logic"></a>传感器驱动程序逻辑


本部分介绍关键驱动程序逻辑或任务形式的伪代码。 这些任务包括以下客户端操作的驱动程序的支持：

-   客户端连接
-   客户端订阅的事件
-   客户端取消订阅事件
-   客户端断开连接

客户端连接时的桌面应用程序调用**ISensorCollection::GetAt**方法。 此方法返回**ISensor**所需的传感器的接口。 当应用程序发布后此接口时，它可断开客户端。

客户端订阅的事件时的桌面应用程序调用**ISensorManager:SetEventSink**方法。 当应用程序释放此方法返回的事件接收器时，客户端取消事件订阅。

## <a name="abbreviations-and-variables"></a>缩写和变量


在本部分中的伪代码使用下面的缩写形式。

| 缩写 | 说明                                                                                               |
|--------------|-----------------------------------------------------------------------------------------------------------|
| CRI          | 当前报表时间间隔内 （以毫秒为单位指定）                                                       |
| CS           | 更改的敏感度 （值都依赖于传感器类型）                                                  |
| CS\[\]       | 所有数据字段的更改区分大小的数组 （例如，3 轴加速感应器有三个条目） |
| LDA          | （适用于仅位置） 的位置所需的准确性                                                      |
| RS           | 报告的状态 （指示是启用还是禁用事件处理）                                       |
| PS           | （可以是 off 低，或高） 的电源状态                                                                    |



伪代码包含以下变量。

| 变量    | 描述                                                                          |
|-------------|--------------------------------------------------------------------------------------|
| sensorID    | 对于给定的传感器的唯一标识符                                                 |
| clientID    | 指定客户端的唯一标识符                                                 |
| flagCRI     | 如果至少一个客户端指定当前报表时间间隔内，则设置为 True         |
| flagCS      | 如果至少一个客户端指定用于设备的更改敏感度，则设置为 True |
| flagLDA     | 如果至少一个客户端指定的位置所需的准确性，则设置为 True       |
| deviceState | 指示该驱动程序连接到设备                                      |



## <a name="driver-methods"></a>驱动程序的方法


传感器驱动程序必须支持客户端和设备的初始化。 伪代码演示了这可以通过使用以下方法：

-   DriverClientInitialize
-   DeviceSensorInitialize

传感器驱动程序支持平台的设备驱动程序接口 (DDI)。 伪代码演示了这可以通过使用以下方法：

-   DDIOnClientConnect
-   DDIOnClientDisconnect
-   DDIOnClientSubscribeToEvents
-   DDIOnClientUnsubscribeFromEvents
-   DDIOnSetCRI
-   DDIOnSetCS
-   DDIOnSetLDA
-   DDIOnGetProperties
-   DDIOnGetDatafields
-   DDIHandleAsyncDataEvent

传感器驱动程序支持内部方法处理更新到当前报告间隔、 更改敏感度，等等。 伪代码演示了这可以通过使用以下方法：

-   DriverUpdateCRI
-   DriverUpdateCS
-   DriverUpdateLDA
-   DriverUpdateSensorState
-   DriverUpdateDatafields

传感器驱动程序支持更新传感器设备的方法。 伪代码演示了这可以通过使用以下方法：

-   DriverUpdateDeviceCRI
-   DriverUpdateDeviceCS
-   DriverUpdateDeviceLDA
-   DriverUpdateDeviceRS
-   DriverUpdateDevicePS

传感器驱动程序支持与包含多个传感器的设备进行交互的方法。 伪代码演示了这可以通过使用以下方法：

-   DriverUpdateDeviceState

如果传感器驱动程序支持 HID 传感器，它可以支持以下方法：

-   HIDSensorPollData
-   HIDSensorDeviceEvent
-   HIDSensorSetProperties
-   HIDSensorGetProperties

如果传感器驱动程序支持 HID 传感器，它可能包含多个传感器的设备支持以下方法：

-   HIDDeviceManagePower

如果传感器驱动程序支持简单传感器 （例如，I2C 或 SPI），它可以支持以下方法：

-   SpbSensorPollData
-   SpbSensorDeviceEvent

## <a name="driver-structures-and-enumerations"></a>驱动程序结构和枚举


HID 驱动程序支持输入的报表。 伪代码使用以下数据结构来表示报表。

```cpp
struct _inputReport
{
    reportID
    senstate
    eventType
    sensorData //this varies from sensor to sensor

} buffer, pbuffer
```

传感器驱动程序将保存客户端数据。 伪代码使用以下数据结构来保存客户端数据。

```cpp
struct clientEntry
{
    clientCRI
    clientCS[]
    clientLDA
    clientSubscribed
}
```

传感器驱动程序所需表示设备状态。 伪代码使用以下枚举来表示设备状态。

```cpp
enum deviceState
{
    deviceStateDisconnected // driver is disconnected from the device
    deviceStateConnected //driver is connected to the device
}
```

传感器驱动程序所需表示设备状态。 伪代码使用以下枚举来表示设备状态。

```cpp
enum deviceState
{
    deviceStateDisconnected // driver is disconnected from the device
    deviceStateConnected //driver is connected to the device
}
```

## <a name="related-topics"></a>相关主题
[传感器驱动程序开发的基础知识](sensor-driver-development-basics.md)



