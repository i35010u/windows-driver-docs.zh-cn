---
title: 方向传感器数据字段
description: 本主题提供有关特定于方向传感器的数据字段的信息。
ms.assetid: 4B1FA56E-6956-4BC9-B929-3D78EF933057
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 80a84e47de6a5e48d76e34ea413d6b03e9f71ffc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533098"
---
# <a name="orientation-sensor-data-fields"></a>方向传感器数据字段


本主题提供有关特定于方向传感器的数据字段的信息。

下表显示数据字段。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|说明/评论|
|---|---|---|---|
|PKEY_SensorData_QuaternionW|VT_R4|必需|旋转轴向量的 （而不是复数的虚部部分） 的真实系数。|
|PKEY_SensorData_QuaternionX|VT_R4|必需|旋转轴向量的 X 分量。|
|PKEY_SensorData_QuaternionY|VT_R4|必需|旋转轴向量的 Y 分量。|
|PKEY_SensorData_QuaternionZ|VT_R4|必需|旋转轴向量的 Z 分量。|
|PKEY_SensorData_MagnetometerAccuracy|VT_UI4|必需|磁力仪传感器的准确性。 有关有效值的详细信息，请参阅[MAGNETOMETER_ACCURACY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-magnetometer_accuracy)。|
|PKEY_SensorData_DeclinationAngle_Degrees|VT_R4|可选|用于推断从地球的地方，磁北真北的地方，磁赤纬角度。 如果不支持，此类扩展会计算此值。|
|PKEY_SensorData_LinearAccelerationX_Gs|VT_R4|可选|X 轴 g's 线性加速实现|
|PKEY_SensorData_LinearAccelerationY_Gs|VT_R4|可选|Y 轴中 g's 线性加速|
|PKEY_SensorData_LinearAccelerationZ_Gs|VT_R4|可选|Z 轴中 g's 线性加速|
|PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond|VT_R4|可选|Gyrometric x 轴方向的速度，以度为单位每秒。|
|PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond|VT_R4|可选|Gyrometric y 轴方向的速度，以度为单位每秒。|
|PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond|VT_R4|可选|Gyrometric z 轴方向的速度，以度为单位每秒。|


## <a name="related-topics"></a>相关主题


[MSDN PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)






