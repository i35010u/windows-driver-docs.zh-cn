---
title: 计步器数据字段
description: 本主题提供有关特定于 pedometer 的数据字段的信息。
ms.assetid: 35E52085-9727-465D-B6EF-D95974423CD5
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 77fc66643f0573c7cc3791ac0a8fb90608e9ae50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845503"
---
# <a name="pedometer-data-fields"></a>计步器数据字段


本主题提供有关特定于 pedometer 的数据字段的信息。

下表显示了数据字段。 有关 "**类型**" 列中显示的数据类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_PedometerStepType|VT_UI4|必需|步骤类型，表示为[PEDOMETER_STEP_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type)值。|
|PKEY_SensorData_PedometerStepCount|VT_UI4|必需|检测到的步骤数。|
|PKEY_SensorData_PedometerStepDuration_Ms|VT_I8|必需|Pedometer 计数步骤的持续时间。 此值以毫秒表示。|
|PKEY_SensorData_PedometerReset|VT_BOOL|必需|指示 pedometer 已重置。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**PEDOMETER\_单步执行\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type)

 

 






