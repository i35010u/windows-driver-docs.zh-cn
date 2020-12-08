---
title: 计步器数据字段
description: 本主题提供有关特定于 pedometer 的数据字段的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 733f053d78f1725869f3c1af55f6165e76038dc4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812273"
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

