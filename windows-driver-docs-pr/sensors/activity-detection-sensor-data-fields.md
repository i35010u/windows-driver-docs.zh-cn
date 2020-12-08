---
title: 活动检测传感器数据字段
description: 本主题提供有关特定于活动检测传感器的数据字段的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 65f6e8937bc9e456c6beaa150e0487df9cee6525
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831075"
---
# <a name="activity-detection-sensor-data-fields"></a>活动检测传感器数据字段


本主题提供有关特定于活动检测传感器的数据字段的信息。

下表显示了数据字段。 有关 " **类型** " 列中显示的数据类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|说明|
| --- | --- | --- | --- |
|PKEY_SensorData_CurrentActivityState|VT_UI4|必须|当前活动状态的指示，表示为类型 [<strong>ACTIVITY_STATE</strong>](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)的值。|
|PKEY_SensorData_CurrentActivityStateConfidence_Percentage|VT_UI2|必须|指示当前活动状态的传感器的置信度级别。|
|PKEY_SensorData_SubscribedActivityStates|VT_UI4|必须|指示已订阅活动状态，表示为类型 [<strong>ACTIVITY_STATE</strong>](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)的值。|
|PKEY_SensorData_ActivityStream|VT_BOOL|必须|如果活动流可用，则设置为 TRUE 的布尔值。|
|PKEY_SensorData_ConfidenceThreshold_Percentage|VT_UI2|必须|传感器置信度的阈值。|
 

## <a name="related-topics"></a>相关主题


[**活动 \_ 状态**](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)

[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)

