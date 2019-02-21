---
title: 传感器类别
description: 传感器类别
ms.assetid: 609C57BA-1C3E-435B-BAAE-C01C3669D59D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1ef5a02034cbe1b8fa11c7a25321e959efdd72e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526155"
---
# <a name="sensor-categories"></a>传感器类别

传感器类别表示传感器设备的广泛类。 类别提供组传感器可能能够提供类似类型的信息，或以某种方式无关的方式。 每个类别均由 GUID 常量表示。 不同类型的两个传感器可以属于同一类别或两个不同的类别。 例如，加速感应器和陀螺仪可能同时进行分类 GUID_SensorCategory_Motion 类别下虽然环境光线传感器会归类 GUID_SensorCategory_Light 类别下。 每个传感器类别由 GUID 常量表示。

传感器类别 Guid SensorsDef.h 中定义

| 名称 | 描述 |
| --- | --- |
| GUID_SensorCategory_All| 此 GUID 标识的所有传感器。 传感器类扩展将传感器添加到此类别，除非驱动程序显式提供了以下类别之一。 |
| GUID_SensorCategory_Biometric | 此 GUID 标识的生物识别传感器类别。 |
| GUID_SensorCategory_Electrical | 此 GUID 标识电源传感器类别。 |
| GUID_SensorCategory_Environmental| 此 GUID 标识的环境的传感器类别。 |
| GUID_SensorCategory_Light| 此 GUID 标识光线传感器类别。 |
| GUID_SensorCategory_Location | 此 GUID 标识位置传感器类别。 |
| GUID_SensorCategory_Mechanical| 此 GUID 标识的机械的传感器类别。 |
| GUID_SensorCategory_Motion| 此 GUID 标识的运动传感器类别。 |
| GUID_SensorCategory_Orientation | 此 GUID 标识方向传感器类别。 |
| GUID_SensorCategory_Other | 此 GUID 标识的传感器的支持，但不是符合任何预定义的类别的类别。 |
| GUID_SensorCategory_Scanner| 此 GUID 标识的扫描程序传感器类别。 |
| GUID_SensorCategory_Unsupported| 此 GUID 标识是不受支持的传感器的类别。 |

