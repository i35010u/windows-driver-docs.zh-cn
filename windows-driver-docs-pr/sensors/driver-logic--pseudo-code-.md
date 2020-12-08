---
title: 传感器驱动程序逻辑
description: 本部分将关键驱动程序逻辑或任务描述为伪代码。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6fa77933d186cd6b25090915895984fa573d5ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812329"
---
# <a name="sensor-driver-logic"></a>传感器驱动程序逻辑

本部分将关键驱动程序逻辑或任务描述为伪代码。 这些任务包括驱动程序对以下客户端操作的支持：

- 客户端连接
- 客户端订阅事件
- 客户端取消订阅事件
- 客户端断开连接

当桌面应用程序调用 **ISensorCollection：： GetAt** 方法时，客户端将连接。 此方法为所需的传感器返回 **ISensor** 接口。 当应用程序释放此接口时，它会断开客户端连接。

当桌面应用程序调用 **ISensorManager： SetEventSink** 方法时，客户端会订阅事件。 当应用程序释放由该方法返回的事件接收器时，客户端将从事件中取消订阅。

## <a name="abbreviations-and-variables"></a>缩写和变量

本部分中的伪代码使用以下缩写形式。

| 缩写 | 说明                                                                                               |
|--------------|-----------------------------------------------------------------------------------------------------------|
| CRI          | 指定的当前报表间隔 (以毫秒为单位)                                                        |
| CS           | 更改敏感度 (值依赖于传感器类型)                                                   |
| 站\[\]       | 区分的所有数据字段的 change 数组的数组 (例如，3轴加速度具有三个条目)  |
| LDA          | 定位所需准确性 (仅适用于位置)                                                       |
| RS           | 报告状态 (指示是启用还是禁用事件)                                        |
| PS           | 电源状态 (可以为 "关"、"低" 或 "高")                                                                     |

伪代码包含以下变量。

| 变量    | 描述                                                                          |
|-------------|--------------------------------------------------------------------------------------|
| sensorID    | 给定传感器的唯一标识符                                                 |
| clientID    | 给定客户端的唯一标识符                                                 |
| flagCRI     | 如果至少有一个客户端指定了当前报表间隔，则设置为 True         |
| flagCS      | 如果至少有一个客户端指定了设备的更改敏感度，则设置为 True |
| flagLDA     | 如果至少有一个客户端指定了所需的位置准确性，则设置为 True       |
| deviceState | 指示驱动程序已连接到设备                                      |

## <a name="driver-methods"></a>驱动程序方法

传感器驱动程序必须支持客户端和设备初始化。 伪代码使用以下方法演示这一点：

- DriverClientInitialize
- DeviceSensorInitialize

传感器驱动程序支持平台的设备驱动程序接口 (DDI) 。 伪代码使用以下方法演示这一点：

- DDIOnClientConnect
- DDIOnClientDisconnect
- DDIOnClientSubscribeToEvents
- DDIOnClientUnsubscribeFromEvents
- DDIOnSetCRI
- DDIOnSetCS
- DDIOnSetLDA
- DDIOnGetProperties
- DDIOnGetDatafields
- DDIHandleAsyncDataEvent

传感器驱动程序支持内部方法，这些方法可处理当前报表间隔的更新、更改敏感度等。 伪代码使用以下方法演示这一点：

- DriverUpdateCRI
- DriverUpdateCS
- DriverUpdateLDA
- DriverUpdateSensorState
- DriverUpdateDatafields

传感器驱动程序支持更新传感器设备的方法。 伪代码使用以下方法演示这一点：

- DriverUpdateDeviceCRI
- DriverUpdateDeviceCS
- DriverUpdateDeviceLDA
- DriverUpdateDeviceRS
- DriverUpdateDevicePS

传感器驱动程序支持与包含多个传感器的设备进行交互的方法。 伪代码使用以下方法演示这一点：

- DriverUpdateDeviceState

如果传感器驱动程序支持 HID 传感器，则它可能支持以下方法：

- HIDSensorPollData
- HIDSensorDeviceEvent
- HIDSensorSetProperties
- HIDSensorGetProperties

如果传感器驱动程序支持 HID 传感器，则它可能支持包含多个传感器的设备的以下方法：

- HIDDeviceManagePower

如果传感器驱动程序支持简单传感器 (例如，I2C 或 SPI) ，则它可能支持以下方法：

- SpbSensorPollData
- SpbSensorDeviceEvent

## <a name="driver-structures-and-enumerations"></a>驱动程序结构和枚举

HID 驱动程序支持输入报告。 伪代码使用以下数据结构来表示报表。

```cpp
struct _inputReport
{
    reportID
    senstate
    eventType
    sensorData //this varies from sensor to sensor

} buffer, pbuffer
```

传感器驱动程序保存客户端数据。 伪代码使用以下数据结构保存客户端数据。

```cpp
struct clientEntry
{
    clientCRI
    clientCS[]
    clientLDA
    clientSubscribed
}
```

传感器驱动程序需要表示设备状态。 伪代码使用以下枚举来表示设备状态。

```cpp
enum deviceState
{
    deviceStateDisconnected // driver is disconnected from the device
    deviceStateConnected //driver is connected to the device
}
```

传感器驱动程序需要表示设备状态。 伪代码使用以下枚举来表示设备状态。

```cpp
enum deviceState
{
    deviceStateDisconnected // driver is disconnected from the device
    deviceStateConnected //driver is connected to the device
}
```

## <a name="related-topics"></a>相关主题

[Windows 中的传感器和位置平台简介](./index.md)
