---
title: 计步器数据字段
description: 本主题提供有关特定于 pedometer 的数据字段的信息。
ms.assetid: 35E52085-9727-465D-B6EF-D95974423CD5
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1a32a75e46f8bbbfdc821111aea411c375c80488
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732779"
---
# <a name="pedometer-data-fields"></a>计步器数据字段


本主题提供有关特定于 pedometer 的数据字段的信息。

下表显示了数据字段。 有关 " **类型** " 列中显示的数据类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|说明|
|--|--|--|--|
|PKEY_SensorData_PedometerStepType|VT_UI4|必须|步骤类型，表示为 [PEDOMETER_STEP_TYPE](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type) 值。|
|PKEY_SensorData_PedometerStepCount|VT_UI4|必须|检测到的步骤数。|
|PKEY_SensorData_PedometerStepDuration_Ms|VT_I8|必须|Pedometer 计数步骤的持续时间。 此值以毫秒表示。|
|PKEY_SensorData_PedometerReset|VT_BOOL|必须|指示 pedometer 已重置。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)

[**PEDOMETER \_ 步骤 \_ 类型**](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type)

