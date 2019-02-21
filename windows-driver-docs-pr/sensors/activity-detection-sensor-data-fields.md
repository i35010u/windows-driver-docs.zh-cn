---
title: 活动检测传感器数据字段
description: 本主题提供有关特定于活动检测传感器的数据字段的信息。
ms.assetid: D123C082-9E20-44C2-A9F2-DAC0E09F61B7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b05f8f13c86323edc699cc9a33a7ef6485ea3771
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523191"
---
# <a name="activity-detection-sensor-data-fields"></a>活动检测传感器数据字段


本主题提供有关特定于活动检测传感器的数据字段的信息。

下表显示数据字段。 有关详细信息中所示的数据类型**类型**列中，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
| --- | --- | --- | --- |
|PKEY_SensorData_CurrentActivityState|VT_UI4|必需|当前活动状态，表示为类型的值指示[ <strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-activity_state)。|
|PKEY_SensorData_CurrentActivityStateConfidence_Percentage|VT_UI2|必需|置信度级别中，该值指示当前的活动状态的传感器。|
|PKEY_SensorData_SubscribedActivityStates|VT_UI4|必需|已订阅的活动状态，表示为类型的值的相对值[ <strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-activity_state)。|
|PKEY_SensorData_ActivityStream|VT_BOOL|必需|活动流设置为，则为 TRUE 的布尔值为可用。|
|PKEY_SensorData_ConfidenceThreshold_Percentage|VT_UI2|必需|传感器的置信度阈值。|
 

## <a name="related-topics"></a>相关主题


[**ACTIVITY\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-activity_state)

[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






