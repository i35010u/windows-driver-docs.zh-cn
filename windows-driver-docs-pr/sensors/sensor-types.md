---
title: 传感器类型
description: 通用传感器类型 Guid
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19f1d29dd27bddd82b5d35ec4f962bf40ae93d80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812159"
---
# <a name="sensor-types"></a>传感器类型

本部分提供有关与每种传感器相关联的传感器类型 Guid 的信息。 传感器类型表示特定类型的传感器。 每个传感器类型可以选择性地适合特定类别。

传感器类型 Guid 在 Sensorsdef 中定义。

| “属性” | 描述 |
| --- | --- |
| GUID_SensorType_Accelerometer3D | 此 GUID 标识加速感应。 |
| GUID_SensorType_ActivityDetection | 此 GUID 标识活动检测传感器。 |
| GUID_SensorType_AmbientLight | 此 GUID 标识环境光线传感器。 |
| GUID_SensorType_Barometer | 此 GUID 标识 barometer |
| GUID_SensorType_Custom | 此 GUID 标识自定义传感器。 |
| GUID_SensorType_GeomagneticOrientation | 此 GUID 标识磁场方向。 |
| GUID_SensorType_GravityVector | 此 GUID 标识重力矢量。 |
| GUID_SensorType_Gyrometer3D | 此 GUID 标识陀螺测试仪。 |
| GUID_SensorType_Humidity | 此 GUID 标识湿度传感器。 |
| GUID_SensorType_LinearAccelerometer | 此 GUID 标识线性加速感应。 |
| GUID_SensorType_Magnetometer3D | 此 GUID 标识磁力仪。 |
| GUID_SensorType_Orientation | 此 GUID 标识传感器的方向。 |
| GUID_SensorType_Pedometer | 此 GUID 标识 pedometer。 |
| GUID_SensorType_Proximity | 此 GUID 标识近程传感器。 |
| GUID_SensorType_RelativeOrientation | 此 GUID 标识 RelativeOrientation 传感器。 |
| GUID_SensorType_SimpleDeviceOrientation | 此 GUID 标识简单的设备方向传感器。 |
| GUID_SensorType_Temperature | 此 GUID 标识温度传感器。 |

>[!NOTE]
> 指南针和倾斜仪传感器不会通过 Windows 通用传感器 DDI 直接公开。 相反，这两个传感器会由传感器堆栈根据 GUID_SensorType_Orientation 传感器自动构造。
> 当系统上有 GUID_SensorType_Orientation 传感器时，将对 WinRT 应用程序显示罗盘和倾斜仪。 同样，altimeter 传感器会根据 GUID_SensorType_Barometer 传感器上的传感器堆栈自动构造。


