---
title: 计步器数据字段
description: 本主题提供有关特定于 pedometer 的数据字段的信息。
ms.assetid: 35E52085-9727-465D-B6EF-D95974423CD5
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 64d4303c5cbb0f59f4d0896ea12e91814005f82a
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010377"
---
# <a name="pedometer-data-fields"></a>计步器数据字段


本主题提供有关特定于 pedometer 的数据字段的信息。

下表显示了数据字段。 有关 " **类型** " 列中显示的数据类型的详细信息，请参阅 [PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|类型|必需/可选|说明|
|--|--|--|--|
|PKEY_SensorData_PedometerStepType|VT_UI4|必需|步骤类型，表示为 [PEDOMETER_STEP_TYPE](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type) 值。|
|PKEY_SensorData_PedometerStepCount|VT_UI4|必需|检测到的步骤数。|
|PKEY_SensorData_PedometerStepDuration_Ms|VT_I8|必需|Pedometer 计数步骤的持续时间。 此值以毫秒表示。|
|PKEY_SensorData_PedometerReset|VT_BOOL|必需|指示 pedometer 已重置。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**PEDOMETER \_ 步骤 \_ 类型**](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type)

 

