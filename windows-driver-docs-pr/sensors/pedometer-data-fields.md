---
title: 计步器数据字段
description: 本主题提供有关特定于计步器数据字段的信息。
ms.assetid: 35E52085-9727-465D-B6EF-D95974423CD5
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f270cda0552421c0d71efedf490e8c833c7ce12e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547246"
---
# <a name="pedometer-data-fields"></a>计步器数据字段


本主题提供有关特定于计步器数据字段的信息。

下表显示数据字段。 有关详细信息中所示的数据类型**类型**列中，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_PedometerStepType|VT_UI4|必需|步骤类型，表示为[PEDOMETER_STEP_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-pedometer_step_type)值。|
|PKEY_SensorData_PedometerStepCount|VT_UI4|必需|检测到的步骤数。|
|PKEY_SensorData_PedometerStepDuration_Ms|VT_I8|必需|持续时间对其计步器计数的步骤。 此值表示以毫秒为单位。|
|PKEY_SensorData_PedometerReset|VT_BOOL|必需|指示计步器已重置。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**计步器\_步骤\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-pedometer_step_type)

 

 






