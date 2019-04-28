---
title: 磁力计数据字段
description: 本主题提供有关特定于磁力仪数据字段的信息。
ms.assetid: 5DA5566A-FECA-47ED-8338-686A548687CC
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d6022f46e2b7a9a57adbd9aff785ee61a1b0b30e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345124"
---
# <a name="magnetometer-data-fields"></a>磁力计数据字段


本主题提供有关特定于磁力仪数据字段的信息。

下表显示数据字段。 有关类型列中显示的类型的详细信息，请参阅[MSDN PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必需|X 轴磁场 microteslas 中。 这被校准到设备的机箱的磁性效果的帐户。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必需|Y 轴磁场 microteslas 中。 这被校准到设备的机箱的磁性效果的帐户。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必需|Z 轴磁场 microteslas 中。 这被校准到设备的机箱的磁性效果的帐户。|
|PKEY_SensorData_MagnetometerAccuracy|VT_UI4|必需|磁力仪传感器的准确性。 有关有效值的详细信息，请参阅[ <strong>MAGNETOMETER_ACCURACY</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-magnetometer_accuracy)。|

 

## <a name="related-topics"></a>相关主题


[**磁力仪\_准确性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-magnetometer_accuracy)

[MSDN PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






