---
title: 传感器类型
description: 通用的传感器类型 Guid
ms.assetid: AD1112ED-4EA8-429D-82E6-D1878447D5E3
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9133ccddc7afcef70e4b80c841b5a9e65226fb88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546466"
---
# <a name="sensor-types"></a>传感器类型

本部分提供有关每种类型的传感器与关联的 Guid 的传感器类型的信息。 传感器类型表示特定类型的传感器。 每个传感器类型可以根据需要适合于特定类别。

传感器类型 Guid Sensorsdef.h 中定义。

| 名称 | 描述 |
| --- | --- |
| GUID_SensorType_Accelerometer3D | 此 GUID 标识加速感应器。 |
| GUID_SensorType_ActivityDetection | 此 GUID 标识活动检测传感器。 |
| GUID_SensorType_AmbientLight | 此 GUID 标识环境光线传感器。 |
| GUID_SensorType_Barometer | 此 GUID 标识计量仪 |
| GUID_SensorType_Custom | 此 GUID 标识的自定义传感器。 |
| GUID_SensorType_GeomagneticOrientation | 此 GUID 标识 geomagnetic 方向。 |
| GUID_SensorType_GravityVector | 此 GUID 标识的重力向量。 |
| GUID_SensorType_Gyrometer3D | 此 GUID 标识陀螺测试仪。 |
| GUID_SensorType_Humidity | 此 GUID 标识湿度传感器。 |
| GUID_SensorType_LinearAccelerometer | 此 GUID 标识线性加速感应器。 |
| GUID_SensorType_Magnetometer3D | 此 GUID 标识磁力仪。 |
| GUID_SensorType_Orientation | 此 GUID 标识方向传感器。 |
| GUID_SensorType_Pedometer | 此 GUID 标识计步器。 |
| GUID_SensorType_Proximity | 此 GUID 标识邻近感应传感器。 |
| GUID_SensorType_RelativeOrientation | 此 GUID 标识 RelativeOrientation 传感器。 |
| GUID_SensorType_SimpleDeviceOrientation | 此 GUID 标识的简单设备方向传感器。 |
| GUID_SensorType_Temperature | 此 GUID 标识温度传感器。 |

>[!NOTE]
> 指南针和倾斜仪传感器不直接通过 Windows 通用传感器 DDI 中公开。 相反，这两个传感器是自动通过传感器堆栈之上 GUID_SensorType_Orientation 传感器构造。
> 指南针和倾斜仪，都会对 WinRT 应用程序可见 GUID_SensorType_Orientation 传感器是系统上存在。 同样，altimeter 传感器系统会自动构建由传感器堆栈之上 GUID_SensorType_Barometer 传感器。


