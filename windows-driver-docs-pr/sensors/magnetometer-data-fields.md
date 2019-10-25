---
title: 磁力计数据字段
description: 本主题提供有关特定于磁力仪的数据字段的信息。
ms.assetid: 5DA5566A-FECA-47ED-8338-686A548687CC
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9441bfd565bbbcce208d5b5f920e38cdb1c72248
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842453"
---
# <a name="magnetometer-data-fields"></a>磁力计数据字段


本主题提供有关特定于磁力仪的数据字段的信息。

下表显示了数据字段。 有关 "类型" 列中显示的类型的详细信息，请参阅[MSDN PROPVARIANT structure](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必需|Microteslas 中的 x 轴磁性字段。 校准此设备是为了考虑设备机箱的磁性效果。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必需|Microteslas 中的 y 轴磁性字段。 校准此设备是为了考虑设备机箱的磁性效果。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必需|Microteslas 中的 z 轴磁性字段。 校准此设备是为了考虑设备机箱的磁性效果。|
|PKEY_SensorData_MagnetometerAccuracy|VT_UI4|必需|磁力仪传感器的准确性。 有关有效值的详细信息，请参阅[<strong>MAGNETOMETER_ACCURACY</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-magnetometer_accuracy)。|

 

## <a name="related-topics"></a>相关主题


[**磁力仪\_准确性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-magnetometer_accuracy)

[MSDN PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






