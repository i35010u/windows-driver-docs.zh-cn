---
title: 传感器类别
description: 传感器类别
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a99b6b2b71e29a77cbbb9b1b1bb03654991ce497
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812233"
---
# <a name="sensor-categories"></a>传感器类别

传感器类别表示传感器设备的广泛类别。 类别提供了一种将可能提供相似类型的信息或以某种方式相关的传感器组合在一起的方法。 每个类别都由一个 GUID 常量表示。 不同类型的两个传感器可以属于同一类别或两个不同的类别。 例如，加速感应器和陀螺仪可能会分类到 GUID_SensorCategory_Motion 类别下，而环境光线传感器可能会分类到 GUID_SensorCategory_Light 类别下。 每个传感器类别由一个 GUID 常量表示。

传感器类别 Guid 是在 SensorsDef 中定义的

| “属性” | 描述 |
| --- | --- |
| GUID_SensorCategory_All| 此 GUID 标识所有传感器。 传感器类扩展将传感器添加到此类别，除非驱动程序显式提供以下类别之一。 |
| GUID_SensorCategory_Biometric | 此 GUID 标识生物识别传感器类别。 |
| GUID_SensorCategory_Electrical | 此 GUID 标识电源传感器类别。 |
| GUID_SensorCategory_Environmental| 此 GUID 标识环境传感器类别。 |
| GUID_SensorCategory_Light| 此 GUID 标识轻型传感器类别。 |
| GUID_SensorCategory_Location | 此 GUID 标识位置传感器类别。 |
| GUID_SensorCategory_Mechanical| 此 GUID 标识机械传感器类别。 |
| GUID_SensorCategory_Motion| 此 GUID 标识运动传感器类别。 |
| GUID_SensorCategory_Orientation | 此 GUID 标识 "方向" 传感器类别。 |
| GUID_SensorCategory_Other | 此 GUID 标识受支持的传感器的类别，但不符合任何预定义的类别。 |
| GUID_SensorCategory_Scanner| 此 GUID 标识扫描器传感器类别。 |
| GUID_SensorCategory_Unsupported| 此 GUID 标识不受支持的传感器的类别。 |

