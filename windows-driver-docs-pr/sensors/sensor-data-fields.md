---
title: 传感器数据字段
description: 传感器驱动程序设置可以通过使用 ReadFile 函数来获取有关传感器驱动程序信息的应用程序读取的数据字段。
ms.assetid: E430AC59-34AC-4F8E-9A42-350C7A42BBA8
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ac26975bef9eb3025021585d5d9902d8b646cd8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522890"
---
# <a name="sensor-data-fields"></a>传感器数据字段

*传感器数据字段*表示特定类型的传感器可以提供的信息。 在报告数据，值被认为是要包含在*数据字段*。 相关的数据字段的集合构成*数据报表*。 在 SENSOR_COLLECTION_LIST 结构一起打包数据报表。 数据的每个报表必须包含至少一个有效的数据字段和一个时间戳，标识创建了数据报表的时间。 由 PKEY_SensorData_Timestamp 属性键表示时间戳。 数据字段的示例包括 x、 y、 z 加速加速感应器值。 每个数据字段由**PROPERTYKEY**常量。

## <a name="in-this-section"></a>本部分内容

|主题|描述|
|---|---|
|[常见的数据字段](common-data-fields.md)|本主题说明在所有特定于传感器的数据字段中包含的常见数据字段。|
|[加速感应器数据字段](accelerometer-data-fields.md)|本主题提供有关特定于加速感应器数据字段的信息。|
|[线性加速感应器数据字段](linear-accelerometer-data-fields.md)|本主题提供有关特定于线性加速感应器数据字段的信息。|
|[磁力仪数据字段](magnetometer-data-fields.md)|本主题提供有关特定于磁力仪数据字段的信息。|
|[Geomagnetic 方向](geomagnetic-orientation.md)|> 本主题提供有关特定于 geomagnetic 方向传感器的数据字段的信息。|
|[重力矢量数据字段](gravity-vector-data-fields.md)|> 本主题提供有关特定于重力矢量数据字段的信息。|
|[陀螺仪数据字段](gyroscope-data-fields.md)|本主题提供有关特定于陀螺仪数据字段的信息。|
|[光线传感器数据字段](light-sensor-data-fields.md)|本主题提供有关特定于光线传感器的数据字段的信息。|
|[方向传感器数据字段](device-orientation-sensor-data-fields.md)|本主题提供有关特定于设备方向传感器的数据字段的信息。|
|[邻近传感器数据字段](proximity-sensor-data-fields.md)|本主题提供有关特定于邻近感应传感器的数据字段的信息。|
|[计量仪数据字段](barometer-sensor-data-fields.md)|本主题提供有关特定于计量仪传感器的数据字段的信息。|
|[简单的设备方向传感器数据字段](simple-device-orientation-sensor-data-fields.md)|本主题提供有关特定于简单的设备方向传感器的数据字段的信息。|
|[活动检测传感器数据字段](activity-detection-sensor-data-fields.md)|本主题提供有关特定于活动检测传感器的数据字段的信息。|
|[计步器数据字段](pedometer-data-fields.md)|本主题提供有关特定于计步器数据字段的信息。|
|[相对方向传感器数据字段](relative-orientation-data-fields.md)|本主题提供有关特定于相对方向传感器的数据字段的信息。|
|[自定义传感器数据字段](custom-sensor-data-fields.md)|本主题提供有关可由自定义传感器的数据字段的信息。|

 

 

 





